---
title: 'JDBCSpy &#8211; What&#8217;s been happening.'
author: ajordens
layout: post
permalink: /2008/03/jdbcspy-whats-been-happening/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
So I&#8217;ve been working off and on over the past 6 months on a little side project, [JDBCSpy][1]. I&#8217;ve mentioned it previously so this post is just a little update.

It&#8217;s far from my day job and really just serves as a bit of an outlet. You&#8217;re free to argue about whether it&#8217;s a creative outlet or not <img src="http://littlesquare.com/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" /> The project stemmed from code written during one of hack days and has grown organically from there.

Essentially the goals of the project are as follows:

  * **Provide an interface to easily gather statistics from a JDBC connection.** Currently this is accomplishable in two ways.</p> 
      * The delegating JDBC driver will write all executing queries to a log file alongside some basic statistical information (ie. <span style="font-style: italic;">how long it spent executing</span>).
      * More interestingly, the delegating JDBC driver also registers an MBean that exposes a slightly more comprehensive set of statistics (ie. <span style="font-style: italic;">how much time has been spent executing sql, # of queries executed, etc.</span>)
      * There&#8217;s also an example implementation of a TestNG listener that will track JDBC statistics on a per-test method basis.
  * **Provide a means of visualizing the gathered statistics.**</p> 
      * **<span style="font-weight: normal;">There is a JDBCSpy Viewer under development. It has the ability to connect real-time to the JDBCSpy MBean and visualize activity. It can also reply a previously logged session by loading the JDBCSpy log file. It makes use of a bunch of the Orson and JFreeChart work so things don&#8217;t look half bad.</span>**

I&#8217;ve been using Maven for all build activities which satisfies one of the non-functional objectives.

If pressed, I&#8217;d say things are available in a beta-quality form. The code isn&#8217;t perfect nor particularly tuned. Most of the <span style="font-style: italic;">(recent)</span> time I&#8217;ve spent on the project has been focused towards GUI refactoring. There&#8217;s plenty of more work to do on the JDBC driver side but it&#8217;s more or less taken a back seat right now. Part of the reason for this lies in the fact that there&#8217;s a few other projects that do something similar for JDBC logging.

Click [here][2] for a screenshot of the current viewer.

I&#8217;ll probably be adding some basic Groovy support <span style="font-style: italic;">(to enable user-defined filtering)</span> to the viewer in the next commit or two. More or less just for kicks but it would also provide an opportunity to play a bit more with the language.

Cheers.

 [1]: http://code.google.com/p/jordens-jdbcspy/
 [2]: http://jordens-jdbcspy.googlecode.com/files/JDBCSpy-LogReplay.png