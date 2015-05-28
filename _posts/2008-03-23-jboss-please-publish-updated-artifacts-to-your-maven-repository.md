---
title: 'JBoss:  Please publish updated artifacts to your maven repository'
author: ajordens
layout: post
permalink: /2008/03/jboss-please-publish-updated-artifacts-to-your-maven-repository/
categories:
  - citations
---
I started playing around with <span style="font-style: italic;">Hibernate Search</span> this weekend by following the [getting started guide][1].

Being a maven user, I <span style="font-style: italic;">attempted</span> to use the JBoss published artifacts (from the [JBoss repository][2]) to make live a bit easier.

**UPDATE: <span style="font-style: italic;">Emmanuel Bernard has commented and pointed out that the updated artifacts have actually been published.<br /></span>**

It looks like the <span style="font-style: italic;">Getting Started</span> <span style="font-style: italic;">Guide</span> is referencing slightly incorrect artifact versions.

<pre>&lt;dependency&gt;
   &lt;groupId&gt;org.hibernate&lt;/groupId&gt;
   &lt;artifactId&gt;hibernate-search&lt;/artifactId&gt;
   &lt;version&gt;<strong>3.0.0.GA</strong>&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
   &lt;groupId&gt;org.hibernate&lt;/groupId&gt;
   &lt;artifactId&gt;hibernate-annotations&lt;/artifactId&gt;
   &lt;version&gt;3.3.0.ga&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
   &lt;groupId&gt;org.hibernate&lt;/groupId&gt;
   &lt;artifactId&gt;hibernate-entitymanager&lt;/artifactId&gt;
   &lt;version&gt;<strong>3.3.2.GA</strong>&lt;/version&gt;
&lt;/dependency&gt;
</pre>

Seem to work a little bit better. It looks like there&#8217;s only a newer version of the <span style="font-style: italic;">hibernate-entitymanager</span> available and that the <span style="font-style: italic;">hibernate-search</span> artifact has been published with a version of <span style="font-style: italic;">3.0.0.GA</span> and not <span style="font-style: italic;">3.0.0.ga.</span>

In the end, not that big of a deal. Just need to do a bit more digging to locate the correctly labeled artifacts.

Thanks Emmanuel for the comment.

 [1]: http://www.hibernate.org/hib_docs/search/reference/en/html/getting-started.html
 [2]: http://repository.jboss.org/maven2/