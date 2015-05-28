---
title: Testing is good, Button pushing is bad.
author: ajordens
layout: post
permalink: /2006/11/testing-is-good-button-pushing-is-bad/
categories:
  - General Discussions
---
Obviously software testing is a good idea. I&#8217;ve been a software developer long enough to realize the benefits of investing in up-front testing of the software. It&#8217;s baked into my development process and I wouldn&#8217;t commit code without at least thinking about the test scenarios, let alone consider writing them up as [unit|integration|regression]-tests.

I started writing this post a couple days ago when I found out that I&#8217;d be tapped to help our QA group with some end of iteration testing this Friday (*today*). My first reaction to GUI regression testing is that it&#8217;s an annoying thing for a developer to have to do. *It* being the act of running through written regression tests and effectively clicking buttons and ensuring that the application behaves accordingly. We&#8217;ve actually done this (successfully) for years but luckily the QA team is starting to get large enough that they don&#8217;t require many testing resources from development. On one hand that&#8217;s good, developers can remain focused and don&#8217;t have to do manual regression testing, but on the other hand, there&#8217;s a lot of potential improvements (automation and other-wise) that could be accomplished rather trivially by properly motivated developers if given the opportunity.

I don&#8217;t think that developer written tests should ever be considered a substitute for end-to-end system regression testing. However, developers should know the in&#8217;s and out&#8217;s of a system and if motivated enough, be able to make the running of these regression tests more efficient.

Here&#8217;s a couple concrete examples:

&#8211; Automating data creation. ex) We&#8217;ve got a process that imports an excel spreadsheet who&#8217;s format is dependent on pre-existing data in the database. The data changes and therefore you&#8217;re forced to make a new spreadsheet for each testing session.

&#8211; Performance testing. If you&#8217;re using a stop watch to gather performance statistics, that&#8217;s gotta be annoying. Invest a few cycles in building an automated test suite that covers enough scenarios to determine trends and problem areas. Run them frequently and without much human intervention.

I don&#8217;t think that developers make good testers and vice-versa. However, there&#8217;s a definite synergy between testers and developers that if you could just let each do what they&#8217;re good at, the overall outcome would be better. If you must have developers help out with testing (assuming they&#8217;re not your only testers), consider giving them the flexibility to improve the process alongside simply ***pushing buttons***.