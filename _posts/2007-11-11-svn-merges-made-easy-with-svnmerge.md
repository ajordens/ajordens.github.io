---
title: 'SVN merges made easy with &#8216;svnmerge&#8217;'
author: ajordens
layout: post
permalink: /2007/11/svn-merges-made-easy-with-svnmerge/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
Branching and merging has always been one of the development gotchas regardless of the particular source control system.

Take a typical scenario where you&#8217;ve found yourself working on a private branch that has forked off of a release branch which was forked off of the trunk.  In an ideal world, the private branch can rather easily pull up any changes made in the release branch and push down after work has been completed.  Further to that, it&#8217;d be great if the push from release branch to trunk was also a relatively painless operation (the painful part being any real conflicts which no tool can fully automate away from you).

With most SCMs this isn&#8217;t that difficult of a problem to solve (I&#8217;ve been using subversion for the past couple of years and it&#8217;s certainly doable).  Complications do arise when you begin having to worry about pulling and pushing certain revisions and tracking change logs between them (ie. what has and has not been merged).

What you don&#8217;t want to see happen is an avoidance of branching because of a fear of merges.  

If you happen to be using subversion, there&#8217;s a nifty python script that makes merge operations (both push and pull) quite painless.  It&#8217;s called [svnmerge.py][1] and it has <span style="text-decoration:underline">excellent documentation</span>!

> *svnmerge.py* is a tool for automatic branch management. It allows branch maintainers to merge changes from and to their branch very easily, and automatically records which changes were already merged. This allows displaying an always updated list of changes yet to be merged, and totally prevents merge mistakes (such as merging the same change twice).

A few of us having been experimenting with it over the past couple of weeks with a lot of success.  We&#8217;ll be rolling it out across our development team in the coming week and early indications are that it&#8217;s going to make everyone&#8217;s lives a bit easier.  The ultimate test will be how developers that may have shied away from merging in the past respond to the tool.

Thanks to Shea for the original pointer to *svnmerge.py*.

 [1]: http://www.orcaware.com/svn/wiki/Svnmerge.py