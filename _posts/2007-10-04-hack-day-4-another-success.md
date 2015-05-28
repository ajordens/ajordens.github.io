---
title: 'Hack Day #4 &#8211; Another Success'
author: ajordens
layout: post
permalink: /2007/10/hack-day-4-another-success/
categories:
  - General Discussions
  - Java
---
Just wanted to report that [we][1] had our 4th hack day today and by all accounts it was another rousing success.

It&#8217;s been almost a year since our first hack day and it&#8217;s been interesting to see the idea transition from a personal project to a company-wide event.  Today was probably the best in terms of involvement with some very interesting submissions coming from the likes of Marketing, Customer Service and Product Management.

There was a bit of twist this time around, everyone was *encouraged* to work in a pair.  We&#8217;ve increased headcount recently so it was a good way to bring new hires into the mix.  Not to mention give everyone a chance to innovate on problems they wouldn&#8217;t normally get to in a work day.

Prior to Hack Day #4, I generally focused on various web technologies (rails, django, etc.).  About as far from J2EE/Swing as you can get.  Today was the first time I took on a problem in Java.  

The problem we set out to solve this time around involved making improvements to the monitoring capabilities of our platform, specifically focusing on gathering statistics around four usage areas:  JDBC, Hibernate, the JVM and JMS.

We started out by implementing a basic proxying JDBC driver that exposed some basic statistics via JMX (statements executed, cumulative times, etc.).  Quite similar to what P6spy did or does (that project is pretty much dead these days).  

Developing the JDBC driver wasn&#8217;t as challenging (or at least didn&#8217;t as long) as I expected.  It basically involved implementing a new SQL Driver and Connection.  The new driver essentially wrapped a PostgreSQL driver.  The Connection created dynamic proxies Statements and PreparedStatements (that themselves delegated to their PostgreSQL-specific equivalents).  The proxies didn&#8217;t do much other than intercept and log calls to executeQuery().  This information was then exposed via JMX.  If I have time to clean things up a bit, this may be something worth open-sourcing now that P6spy is more or less dead (although [JAmon][2] likely provides a more functional solution). 

Next up, Hibernate statistics.  Fortunately, Hibernate ships with a StatisticsServiceMBean that just needs to be registered in the appropriate MBean server.  The StatisticsService provides a lot of useful information (slightly more coarsely grained compared w/ the JDBC statistics).  If you&#8217;re using Hibernate, investigate the StatisticsServiceMBean. 

The JVM itself exposes a variety of information via JMX, everything from memory usage to thread contention.  It&#8217;s easily accessed so I won&#8217;t dig into it.

Lastly, our application makes heavy use of JMS messages for client synchronization.  It currently takes Developers a fair bit of effort to determine exactly what messages are generated and what client-side components actually require them.  Aside from complexity issues, it&#8217;s not uncommon to see significant overhead coming from the sending and receiving of these JMS messages.  Definitely something we want to address moving forward.  Fortunately, it wasn&#8217;t that difficult to make our existing JMS receivers expose subscription and throughput statistics.

Once the statistics were gathered all that was left was finding an appropriate way to visualize them.  In the end we took a hybrid approach, choosing to build both Swing and web components.  The Swing component made use of [JFreeChart][3] and [Orson][4].  It could be run standalone or embedded in our existing desktop application. The web component used the commercial [Fusion][5] charting components (*Flash-based*) and was deployed as a web app in JBoss.

In the end, I had a lot of fun doing this hack.  I suspect they&#8217;ll be a lot of uptake on the development team around improved monitoring and diagnostics which can only be a good thing.

I look forward to the next quarter&#8217;s hack day!

 [1]: http://www.genologics.com
 [2]: http://jamonapi.sourceforge.net/
 [3]: http://www.jfree.org/jfreechart/
 [4]: http://www.jfree.org/orson/
 [5]: http://www.fusioncharts.com/