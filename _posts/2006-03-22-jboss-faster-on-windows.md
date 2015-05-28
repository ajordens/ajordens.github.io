---
title: JBoss faster on Windows
author: ajordens
layout: post
permalink: /2006/03/jboss-faster-on-windows/
categories:
  - Java
---
On a whim I decided to migrate our development environment from being Linux-based to at least being usable on a Windows machine.

My original intentions were to package everything together with cygwin and attempt to keep things self contained.  It probably would have worked but I soon realized that it was just as easy if not easier to install the native equivalents (PostgreSQL, ant, JBoss, etc).

To make a long story short, it took a couple hours but I&#8217;ve pretty much got everything running with 95% of the unit tests passing (the unit tests that aren&#8217;t have hard coded unix paths in them).  I couldn&#8217;t get rid of cygwin completely but I&#8217;m only using it as an sftp daemon.

I haven&#8217;t done a lot of Java development lately on Windows but I had heard that it was pretty fast compared to similar Linux operating environments.

After the migration, the first thing I noticed was that an initial JBoss load and deploy of the application took ~20-30s whereas on my Linux machine (actually a dualboot on this laptop so the hardware is equivalent @ 2.00ghz/2GB) it would take ~1m40s.  Even the application seemed to run substantially faster but I haven&#8217;t had time to do much in the way of timing.  Either way, I&#8217;m pretty impressed.  Originally I did this because its an inconvience to ahve to dualboot when I&#8217;m at home and want to work, but after seeing these numbers I might actually try it out for awhile in the office.

Perhaps there&#8217;s something I can tune in the Linux environments to get the same sorts of performance improvements.