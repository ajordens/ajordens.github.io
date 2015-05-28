---
title: Custom AuthenticationProvider w/ Grails + Spring Security
author: ajordens
layout: post
permalink: /2010/09/custom-authenticationprovider-w-grails-spring-security/
categories:
  - General Discussions
---
For the past couple of weeks, we&#8217;ve been putting some work into a new integration platform and a series of user persona-specific applications built on top of it.

Currently, the integration platform is largely plumbing with the eventual goal of supporting numerous pluggable services (*think new APIs*). Platform developers will have access to common messaging and asynchronous task execution services, and be able to write their components in a variety of JVM languages (Java, Groovy and Scala).

I&#8217;d love to standardize on Scala but it&#8217;s a bit early to draw that line in the sand.

To properly exercise this new platform, we&#8217;ve been working on a couple proof of concept applications. Today&#8217;s task was to investigate mechanisms for authentication and authorization. These applications are deployed independently from the core integration platform and will communicate primarily over REST APIs or asynchronous message passing.

The first proof of concept application was built using Grails and setup to use Spring Security for managing authentication. In contrast to a few other unnamed Grails plugins, the integration w/ Spring Security is quite well documented.

Our plan of attack was to replace the default AuthenticationProvider in Spring Security with one capable of hitting a platform API. This platform API would handle both authentication of the username/password (*probably basic auth to start*) and authorization. The later accomplished by returning a list of user roles that the application can use to secure individual controller/services.

Simple enough.

**Replace the daoAuthenticationProvider**

*<u>resources.groovy</u>*

[java]  
// Place your Spring DSL code here

beans = {

platformAuthenticationProvider(org.jordens.PlatformAuthenticationProvider) {

// no attribute

}

}  
[/java]

*<u>Config.groovy</u>*

[java]  
grails.plugins.springsecurity.providerNames = [&#8216;platformAuthenticationProvider&#8217;,

&#8216;anonymousAuthenticationProvider&#8217;,

&#8216;rememberMeAuthenticationProvider&#8217;]

[/java] 

It&#8217;s important that the same bean id (*platformAuthenticationProvider in this case*) is specified in both **resources.groovy** and **Config.groovy**.

*<u>src/main/org/jordens/PlatformAuthenticationProvider</u>*

[java]  
class PlatformAuthenticationProvider implements AuthenticationProvider  
{  
public static final String API_ROOT = "http://localhost:8080/platform/api/"

Authentication authenticate(Authentication authentication)  
{  
if (authentication instanceof UsernamePasswordAuthenticationToken)  
{  
UsernamePasswordAuthenticationToken token = (UsernamePasswordAuthenticationToken) authentication

String username = token.getPrincipal()  
String password = token.getCredentials()

def roles = []  
RESTClient client = new RESTClient(API_ROOT, ContentType.JSON)  
try  
{  
HttpResponseDecorator r = (HttpResponseDecorator) client.get(  
path: "users/${username}/roles",  
query: [&#8216;app-id': &#8216;user-management&#8217;])

JSONArray json = (JSONArray) r.data  
json.each { String roleName ->  
roles < < new GrantedAuthorityImpl(roleName)  
}  
}  
catch (HttpResponseException e)  
{  
e.printStackTrace()  
}

if (roles)  
{  
return new UsernamePasswordAuthenticationToken(username, password, roles)  
}  
}  
return null  
}

boolean supports(Class<? extends Object> aClass)  
{  
if (aClass.isAssignableFrom(UsernamePasswordAuthenticationToken.class))  
{  
return true  
}

return false  
}  
}  
[/java]

The PlatformAuthenticationProvider only supports username and password tokens (*similar to the daoAuthenticationProvider*). As it stands right now, it&#8217;s quite rudimentary and simply attempts to lookup a user using a platform API. If the user exists, a list of roles will be returned and converted into GrantedAuthorities for integration with Grails/Spring Security. 

**Success**. In a few hours on a Friday afternoon, we satisfied our goal of eliminating built-in credentials from the Grails application in favor of existing platform APIs. Moving forward, this authentication provider will need to be updated and pass credentials to the platform API.