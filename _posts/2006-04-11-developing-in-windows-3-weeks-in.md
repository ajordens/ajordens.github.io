---
title: Developing in Windows, 3 weeks in.
author: ajordens
layout: post
permalink: /2006/04/developing-in-windows-3-weeks-in/
categories:
  - General Discussions
  - Java
---
So it&#8217;s been ~3 weeks since I switched my primary development environment from Ubuntu to Windows.

I wasn&#8217;t sure how it would turn out (been a Linux user for the better part of the past 12 years), but I&#8217;ve actually been quite happy. All my tools (Eclipse, JRockit, ant, svn, etc.) worked pretty much out of the box. I do have cygwin installed and my terminal of choice is rxvt, so I haven&#8217;t completely abandoned the relative comfort of Unix.

My initial reason for switching to Windows had to do primarily with performance. Sun&#8217;s jdk on Windows was substantially faster than the equivalent on Linux. I don&#8217;t have concrete runtime numbers but JBoss was starting up in 1/3 the time. That did serve as a bit of a catalyst to make the necessary changes to the codebase so that we could run with JRockit (we use xstream for xml [de]serialization and it has a problem with some jre&#8217;s and private final variables). JRockit on Linux did bring the JBoss startup time down, but java on windows still *feels* faster even if it really isn&#8217;t.

I did run into a rather annoying problem today tho. I needed to do some packet sniffing on my localhost but it turns out that the Windows tcp/ip stack doesn&#8217;t have a true loopback (ala Linux) and Ethereal wasn&#8217;t able to pick anything up. A minor inconvience but one nonetheless.

I will return to Linux development (at some point), but it&#8217;s been nice to be able to come home, fire up some rxvt&#8217;s and do a bit of development. Much easier than having to dual-boot everytime I want to look over some code. I haven&#8217;t really looked into it, but perhaps there might be a virtualization alternative using VMware or perhaps even [coLinux][1].

My development machine is a Dell Latitude 2ghz centrino with 2gigs of ram. It&#8217;s been able to handle most everything I&#8217;ve thrown at it and there weren&#8217;t many problems in terms of unsupported hardware in either Linux or Windows. Next on the upgrade path is a dual-core <img src="http://littlesquare.com/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

**Must Haves for Windows Development**

  * Cygwin (and rxvt)
  * EditPlus
  * Ethereal
  * Psi (Jabber client)
  * and the usuals (Eclipse/IntelliJ, JRockit, ant, Apache)

 [1]: http://www.colinux.org