---
title: Introducing JDBCSpy
author: ajordens
layout: post
permalink: /2007/11/introducing-jdbcspy/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
More for personal interest than anything else but I&#8217;ve decided to re-write and open-source part of what I worked on for the last hack day.

I&#8217;ve called it JDBCSpy and it&#8217;s available over on [Google Code][1].  It&#8217;s worth noting that there are a couple of other projects that also aim to accomplish more or less similar things, notably [P6Spy][2] and [JAMon][3].  Unfortunately it doesn&#8217;t look like P6Spy has had any active development done on it in the past 3 or 4 years.  The last time I checked it also had a rather cryptic set of dependencies (that had to be downloaded separately and put on the compilation classpath) and an overly complicated build.  Essentially, JDBCSpy aims to provide similar functionality but in an easily packaged driver that exposes information via JMX.  There will also be a standalone viewer that can visualize the information as it&#8217;s being gathered.

**Objective**

JDBCSpy aims to provide a lightweight means to obtain statistics at the JDBC driver level.

**Status  
**  
It currently provides minimal statistics around JDBC Statements and PreparedStatements but functionality is expected to improve over time.

JDBCSpy has been tested using PostgreSQL and hsqldb but should more or less work with any configurable JDBC data source.

**Dependencies  
**  
There are no run-time dependencies. JDBCSpy has test-time dependencies on TestNG and hsqldb.

**Future Plans  
**  
* Support for more Statement/PreparedStatement? methods (currently only tracks executeQuery())  
* Provide a nice UI for statistics visualization (Currently in progress, a Queries per Second chart has now been committed)

All in all, pretty basic stuff but it&#8217;s given me an opportunity to play a bit more with Maven and learn more about JDBC internals.  It&#8217;s far from production right now but should provide useful foundation for future enhancements.

**Note to self: ** Maven makes life so much simplier.  There&#8217;s nothing better than:  *mvn idea:idea*

 [1]: http://code.google.com/p/jordens-jdbcspy/
 [2]: http://www.p6spy.com/
 [3]: http://jamonapi.sourceforge.net/