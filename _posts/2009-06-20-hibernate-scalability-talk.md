---
title: Hibernate Scalability Talk
author: ajordens
layout: post
permalink: /2009/06/hibernate-scalability-talk/
categories:
  - General Discussions
  - Java
  - Open Source Software
tags:
  - qcon hibernate
---
Good [talk][1] from Emmanuel Bernard and Max Ross on the subject over at InfoQ. Both Hibernate Core and Shards are covered, as well as Hibernate Search.

Particularly interesting for me was his overview of the different mechanisms by which you can support multiple customer schemas securely and with decent performance.&#160; The product I’m actively working on is likely headed in this direction, looks like Oracle VPD is Emmanuel’s preferred solution.&#160; A quick search has turned up an add-on for Postgres called [Veil][2] which aims to provide row/column-level security similar to Oracle VPD.&#160; Good to at least have a choice, but I imagine that when push comes to shove, Oracle will win out.

Shards has always looked interesting, will be nice when it finally hits GA and supports the JPA API.&#160; Would make it slightly easier to incorporate and play around with.

Interesting thoughts on clustering Lucene/Hibernate Search.&#160; We’re currently running it asynchronously (*ie. @Asynchronous in Seam*) on a single node but will likely need to look at pushing it to a second box and trying to get indexes in near real time without noticeable degradation to the front-end.

 [1]: http://www.infoq.com/presentations/Scaling-Hibernate-Emmanuel-Bernard-Max-Ross
 [2]: http://veil.projects.postgresql.org/curdocs/index.html