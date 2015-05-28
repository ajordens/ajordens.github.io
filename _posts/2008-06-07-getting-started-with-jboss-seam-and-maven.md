---
title: Getting started with JBoss Seam and Maven
author: ajordens
layout: post
permalink: /2008/06/getting-started-with-jboss-seam-and-maven/
categories:
  - General Discussions
  - Java
---
For the past couple of weeks I&#8217;ve been doing a bit of early development work with Seam, it&#8217;s been fun but not without annoyance.

The project is green field which in one respect is quite nice because of the freedom it presents with regards to technology and architecture choices, but on the flip side you&#8217;ve actually got to investigate these choices and do all the general project plumbing (build management, etc.).

This initial post will deal largely with a couple of build infrastructure issues and solutions.

**1.** **Maven**

Fortunately the Seam Framework guys have been publishing Maven artifacts for awhile now.

Unfortunately, information on suitable project archetypes to use has been scarce. Initial searches turned up a few examples that were a number of years old and quite dated.

I eventually found [JBSEAM-2371][1] which provided a useful starting point project.

I had to download the parent Seam pom and make modifications to the artifact name in order to get <span style="font-style: italic;">mvn site-deploy</span> working appropriately. Something about the site plugin not being able to create directories with spaces in them.

<span style="font-style: italic;">Current Status</span>: Everything is working. SeamTest-based integration tests are working (<span style="font-style: italic;">using embedded-jboss and hsqldb</span>)<span style="font-style: italic;">.</span> Both the Maven site and IntelliJ IDEA plugins create the appropriate output. Artifacts are being deployed into JBoss 4.2.2.GA as part of the <span style="font-style: italic;">install phase</span> using cargo.

<span style="font-style: italic;">The project layout is somewhat like the following</span>:

> <pre>api/app1-api
api/app2-api
seam/app1/app1-web
seam/app1/app1-ejb
seam/app1/app1-ear
seam/app2/app2-web
seam/app2/app2-ejb
seam/app2/app2-ear     
</pre>

**2. Static Analysis**

Nothing too out of the ordinary here.

I&#8217;ve currently setup <span style="font-style: italic;">Checkstyle</span> and <span style="font-style: italic;">FindBugs</span>.

Configuration is stored in a separate top-level <span style="font-style: italic;">build-resources</span> artifact (<span style="font-style: italic;">with xml configurations stored in src/main/resources</span>) and included as a build extension in the project pom.

> <pre>&lt;build&gt;
...
  &lt;extensions&gt;
    &lt;extension&gt;
      &lt;groupId&gt;a.b.c&lt;/groupId&gt;
      &lt;artifactId&gt;build-resources&lt;/artifactId&gt;
      &lt;version&gt;1.0-SNAPSHOT&lt;/version&gt;
    &lt;/extension&gt;
  &lt;/extensions&gt;
&lt;/build&gt;
</pre>

**3. API Development**

One of the key components of this project will be an API.

Rather than go the SOAP web services route, we&#8217;re strongly considering going RESTful with [JAX-RS/JSR 311][2] helping us get there.

Bill Burke, Angry Bill of JBoss fame, has been actively developing [RESTeasy][3], an implementation of JSR 311. It integrates fairly nicely with a Seam deployment (<span style="font-style: italic;">annotate your stateless EJBs and modify your web.xml</span>) and allows you to easily expose a RESTful API backed by stateless session beans.

It should also be possible to go with the reference implementation of the JSR 311, [Jersey][4], although I suspect that the JBoss implementation will eventually have a nicer integration for users of their stack.

JBoss AS doesn&#8217;t currently ship with a JSR 311 implementation so I had to install the jax-rs API and resteasy implementation jars into <span style="font-style: italic;">server/default/lib</span> as part of a separate bootstrap process. This allowed me to mark the dependencies as **<span style="font-style: italic;">provided</span>**.

**Conclusion**

Things are working and most of the grunt project infrastructure work is behind me. It&#8217;s been a good opportunity to get more familiar with Maven but now it&#8217;s time to get cracking on requirements definition and prototyping!

If you&#8217;re interested in working on a Seam-based application in the BioIT/Data management space, leave a comment and we&#8217;ll be in touch.

 [1]: http://jira.jboss.org/jira/browse/JBSEAM-2371
 [2]: https://jsr311.dev.java.net/
 [3]: http://wiki.jboss.org/wiki/RESTeasy
 [4]: https://jersey.dev.java.net/