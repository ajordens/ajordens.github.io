---
title: Guice and Spring JavaConfig
author: ajordens
layout: post
permalink: /2007/08/guice-and-spring-javaconfig/
categories:
  - General Discussions
  - Open Source Software
---
I&#8217;ve been on vacation for the past week or so and took a couple hours to play around with [Guice][1].

Guice **!=** Spring Framework. 

For those that don&#8217;t know, Guice is a light-weight dependency injection framework. What separates it from a few other frameworks is its reliance on annotations and code-based constructs for wiring together dependencies. There is no XML-based approach to configuration. If you&#8217;re one that takes to reading code over xml files, you&#8217;ll have no problem adjusting. It took all of a single page of the first tutorial I found for me to get the jist of it and start implementing a simple app. 

It&#8217;s light-weight in the sense that it does dependency injection and little more. Ensure that the jar is on your classpath and you&#8217;re set. If you want web services, advanced AOP, etc. than you&#8217;ll most likely be the one having to locate and wire in suitable service implementations. 

There&#8217;s a good [Google Tech Talk][2] that covers Guice in more detail.

Having worked with a couple of Spring projects of various sizes, I can attest to the belief that there is overhead in maintaining configuations in various XML files. However, that&#8217;s not to say that a strictly code-based approach would be preferred in all cases, it&#8217;s merely an alternative. Having worked with Spring for a couple years now, I&#8217;d probably go back and take what I&#8217;ve learned and improve existing configurations before considering a more drastic change in configuration strategies. I should mention that *Spring JavaConfig* does allow you to mix & match code-based and xml-based configurations.

There was a decent post a few months back over on [SpringLoaded][3] that did a simple side-by-side comparison of Guice and Spring JavaConfig. *JavaConfig* is basically an extension to the core Spring framework that allows you to create an annotation-backed ApplicationContext. 

Both JavaConfig and Guice do make fairly heavy use of Java5 annotations. Guice is arguably more intrusive as it&#8217;s annotations must be inserted into your application code. For example, if you wanted to use setter injection on a class, you would actually add an @Inject annotation on the setXXX() method. Likewise, if you wanted to apply an AOP interceptor to a method, you&#8217;d annotate the method and setup the appropriate binding call. 

In Guice, you configure an Injector (a quasi-service locator class responsible for providing populated object instances) with an appropriate configuration Module. The Module contains all (or a subset in the event that you&#8217;re using multiple Modules) object binding configurations. A binding is essentially a simple mapping of interface to implementation (ie. bind(SomeInterface.class).to(SomeInterfaceImpl.class)) with an optional context.

You also have a central configuration class in JavaConfig but gone is the instrusiveness associated with changing existing application code. The JavaConfig Configuration class implements each required bean as a method (ie. public SomeBean bean1();). It&#8217;s up to the implementor of these methods to ensure that appropriate dependencies have been injected. There&#8217;s an important trade-off to be aware of here between what&#8217;s provided by the framework and what&#8217;s expected of the implementation. I must admit that I prefer JavaConfig&#8217;s handling of interceptors via a Spring AOP point cut expression to Guice&#8217;s annotation. 

In the end, I do more or less agree with Craig&#8217;s [conclusions][3]. There&#8217;s some interesting commentary from both Colin (Spring) and Bob Lee (Guice) that is also worth checking out. Given how widespread the use of Spring is, it&#8217;ll be interesting to see how the JavaConfig extension plays out (currently it&#8217;s 1.0m3).

If I were starting a personal project today, I&#8217;d seriously consider using Guice if I needed a dependency injection framework. It&#8217;s simple and certaintly fits the bill. Plus, it&#8217;s already available in a public maven repository (although JavaConfig is also available via. the Spring Framework&#8217;s own repository).

Mmmm new and shiny frameworks!

 [1]: http://code.google.com/p/google-guice/
 [2]: http://video.google.com/videoplay?docid=6068447410873108038&q=guice
 [3]: http://www.jroller.com/habuma/entry/guice_vs_spring_javaconfig_a