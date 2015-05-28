---
title: Do You OpenGrok?
author: ajordens
layout: post
permalink: /2008/04/do-you-opengrok/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
Today was our first [hack day][1] of 2008. I&#8217;ve been helping coordinate these events for the past year and a half and they&#8217;ve proven to be a solid source of inspiration and motivation for all participants.

Unfortunately for me, today was more or less a day of false starts. Like always, I had a number of ideas but quickly realized most of them were too much work or simply not interesting enough to devote time to. I was contemplating playing around with GWT or Android but couldn&#8217;t think of an interesting enough problem to warrant the effort setting up the development environment. I just couldn&#8217;t bring myself to install Eclipse.

On the Eclipse front, it&#8217;s a constant struggle. I think the community support it gets is great but wish other IDEs would get the same love (<span style="font-style: italic;">obviously it&#8217;s a matter of user demand</span>). I&#8217;m an IntelliJ fan and find its lack of serious plugins for many of the popular open-source frameworks a bit disappointing. It&#8217;s Groovy support is top notch, things are definitely lacking when it comes to other popular frameworks (<span style="font-style: italic;">like Seam which has JBoss Tools for Eclipse but not much for IntelliJ</span>).

I&#8217;ll leave the topic of Maven artifacts for another day. Needless to say that some of the more popular frameworks and libraries are starting to come around to it.

The day was not a complete loss and I did manage to make progress on a couple of things. The first involved some UI work that could eventually replace our current excel-based way of doing expenses. I&#8217;ve been seeing more and more references to [Ext JS][2] and wanted to check it out. I mocked up a bit of a GUI using some of their components but didn&#8217;t get much farther than that. I was quite impressed with their [examples][3] ([Feed Viewer][4] and [Web Desktop][5]). If you&#8217;re a web developer, I&#8217;d be interesting in hearing your thoughts on the library. I don&#8217;t do a lot of web-centric development but I have played a bit with [Prototype][6], [JQuery][7] and [Mochikit][8] previously in conjunction with Rails and Django.

The more interesting thing I played around with today was [OpenGrok][9].

> OpenGrok is a fast and usable source code search and cross reference engine. It helps you search, cross-reference and navigate your source tree. It can understand various program file formats and version control histories like Mercurial, SCCS, RCS, CVS, Subversion, Teamware and Bazaar. In other words it lets you grok (profoundly understand) the open source, hence the name OpenGrok. It is written in Java.
> 
> OpenGrok is the tool used for the OpenSolaris source browser and search.

It&#8217;s actually pretty cool. I installed on to a Ubuntu 7.10 virtual machine without too many problems. There are a few gotchas (<span style="font-style: italic;">documented and undocumented</span>) when it came to indexing our source code (<span style="font-style: italic;">from subversion</span>) but in the end it worked pretty well. OpenGrok uses [Lucene][10] behind the scenes and provides a nice simplistic web application for searching and navigating the source code (<span style="font-style: italic;">there are also command-line and Swing interfaces</span>).

Performance was very good. Indexing a checkout consisting of ~1.1G (lots of libraries and test data) didn&#8217;t take much longer than a couple minutes. Indexing the 11,000 change sets from subversion only added about a minute. <span style="font-style: italic;">This is on a VM w/ 512M on a MacBook Pro</span>. Searches are instantaneous.

I haven&#8217;t played around with too many other source code x-referencers so I&#8217;m not sure I fully understand it&#8217;s potential or how it compares to it&#8217;s commercial and OSS competitors. That being said, I love the speed and if the OpenSolaris guys are using it, it can&#8217;t be that bad right?

 [1]: http://www.theglobeandmail.com/servlet/story/RTGAM.20070719.wgthackday19/BNStory/Technology/home
 [2]: http://extjs.com/
 [3]: http://extjs.com/deploy/dev/examples/
 [4]: http://extjs.com/deploy/dev/examples/feed-viewer/view.html
 [5]: http://extjs.com/deploy/dev/examples/desktop/desktop.html
 [6]: http://www.prototypejs.org/
 [7]: http://jquery.com/
 [8]: http://mochikit.com/
 [9]: http://opensolaris.org/os/project/opengrok/
 [10]: http://lucene.apache.org/