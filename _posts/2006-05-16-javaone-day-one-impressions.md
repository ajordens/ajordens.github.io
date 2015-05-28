---
title: 'JavaOne &#8211; Day One Impressions'
author: ajordens
layout: post
permalink: /2006/05/javaone-day-one-impressions/
categories:
  - General Discussions
  - Java
---
So, JavaOne 2006 officially kicked off today.

I attended the following first day sessions:

[Desktop Java™ Technology Today: Deep Dive][1]

[Essential Lessons of Distributed Caching][2]

[What Is Happening With SOA in Open Source?][3]

[Service Component Architecture: Approach to Security, Transactions, and Policy][4]

[Java™ EE 5 Platform: Even Easier With Tools][5]

The first two sessions were quite good, the last couple were not so good. It&#8217;s important to not only take the topic into consideration, but also the speakers and their respective employers. I found some of the presentations to be a little to close to spec reviews. Although I am looking forward to some of the BoF&#8217;s that are scheduled for tonight and we got an invitation to the JBoss party on Wednesday night.  
Cameron Purdy presented on the do&#8217;s and don&#8217;ts of distributed caching, mentioning Coherence only once. The talk consisted of a series of lesson&#8217;s regarding how best to partition your distributed cache (and under what circumstances), the driving motivations for caching, the drawbacks of one strategy versus another, and some of the potential pitfalls you&#8217;ll most likely run into. One of the lessons actually struck home (caching of the hashCode() method). We recently made optimizations in that area and it&#8217;s amazing the number of times your hashCode() and equals() get invoked over the course of normal program execution (let alone stress testing).

The first session of the day was actually an overview/deep-dive on some of the new Java 6.0 aka. Mustang changes. There&#8217;s been numerous updates and improvements to the core AWT/Swing hierarchies. The SwingWorker has been brought up to date with annotations and requested functionalities. Vast performance improvements have been made to the OpenGL rendering pipeline as well as general L&#038;F improvements to WebStart security dialogs (!!). There&#8217;s been an emphasis on professionalizing desktop java. The Java 6.0 renderings will be back-ported to Java 5.0 (platform-specific component painting using native calls) so that both Windows and GTK+ platforms will have pixel-perfect native component renderings.

There were also substantial performance improvements made to the ImageIO framework on the order of 100-200%. Some of the JDIC components have also been folded into the JDK (TrayIcon, SplashScreen and the Desktop classes). Although it was unfortunate to hear that the support hasn&#8217;t really expanded past Windows &#038; Gnome. I&#8217;ve had to work around numerous problems with Desktop.open() on the Mac and I guess those hacks (?) will have to persist.

Time for dinner and than a couple of BoF sessions.

 [1]: javascript:newWnd('session_details.jsp?isid=278593&#038;ilocation_id=124-1&#038;ilanguage=english');
 [2]: javascript:newWnd('session_details.jsp?isid=278402&#038;ilocation_id=124-1&#038;ilanguage=english');
 [3]: javascript:newWnd('session_details.jsp?isid=279002&#038;ilocation_id=124-1&#038;ilanguage=english');
 [4]: javascript:newWnd('session_details.jsp?isid=277765&#038;ilocation_id=124-1&#038;ilanguage=english');
 [5]: javascript:newWnd('session_details.jsp?isid=278361&#038;ilocation_id=124-1&#038;ilanguage=english');