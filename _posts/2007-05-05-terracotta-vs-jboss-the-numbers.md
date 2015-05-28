---
title: 'Terracotta vs. JBoss &#8211; The Numbers'
author: ajordens
layout: post
permalink: /2007/05/terracotta-vs-jboss-the-numbers/
categories:
  - General Discussions
---
Interested post over on the [Terracotta blog][1] (actual pdf available [here][2]) concerning performance between Terracotta&#8217;s caching mechanism and the JBoss TreeCache.

If you&#8217;re in a situation where scalability (and reliability) are a chief concern, you should definitely check the *open source* Terracotta offering out. 

Even if you don&#8217;t necessarily live in a high-throughput environment, the paper does present an interesting argument towards moving clustering from the application to the JVM. 

One of the problems we commonly face at work (w/ a thick client/j2ee server application) involves the synchronization of different client states and data (ClientA changes data, ClientB, ClientC, ClientD *may* need to know about it). I&#8217;ve yet to really work on a project that has required scalability to the extent that Terracotta (or even JBoss TreeCache) would provide but I have come to realize the significant performance problems associated with shipping (and responding to) high-volume synchronization messages across the wire. 

Might just have to play a bit more with Terracotta during our next [Hack Day][3].

If you&#8217;re attending JavaOne this year, there&#8217;s a couple Terracotta [clustering clinics][4] planned.

 [1]: http://blog.terracottatech.com/2007/05/jboss_versus_terracotta_revisi_1.html
 [2]: http://www.terracotta.org/confluence/download/attachments/12545/TerracottaTreeCache.pdf?version=1
 [3]: http://www.jordens.org/?p=205
 [4]: http://www.terracotta.org/confluence/display/orgsite/JavaOne+2007#JavaOne2007-clusteringclinic