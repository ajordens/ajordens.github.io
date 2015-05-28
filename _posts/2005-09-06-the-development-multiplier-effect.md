---
title: The development multiplier effect
author: ajordens
layout: post
permalink: /2005/09/the-development-multiplier-effect/
categories:
  - General Discussions
---
I tend to agree with Marty over at [The Wry Tradesman][1].

> Most software development projects have developers as the largest group of people within it, and they are engaged for the longest time on the project. They also tend to do the same things over and over again many times every day. Write a test, write some code, update from source control, run a build, check in. Rinse. Repeat. Good developers will do this up to tens of times per day.
> 
> All of these things mean that minute changes in productivity on a single task for your average developer on the project can have dramatic impacts across the project as a whole. On a project with 10 developers that do 10 builds a day each, improving the build speed from 5 minutes to 4 minutes saves over [8] hours every week.
> 
> For these reasons, I&#8217;m very wary of compromising on even the finest details around productivity for developers, and aggressively seek out improvements where possible. The biggest culprits that I see are in the IDE, source control system, and automated build. Be proactive about constantly improving these things and you&#8217;ll be well on the way to a productive environment. 

Combine that with a streamlined development process (ie. no unnecessary meetings and phone calls) and you&#8217;ll probably be productive and have happy developers.

I must admit that we suffer from a bit of a slow build process as well. We have a thick client and an J2EE-based backend complete with all the CMP EntityBean goodness you could imagine. Building the desktop client is trivial, and for the most part it&#8217;s compiled incrementally and debug&#8217;d through eclipse. Our backend, however, relies on xdoclet to generate deployment descriptors and home/remote interfaces. This generation is slow but is only necessary when we make database changes or modifications to the exposed public api.

The real kicker for us is the OutOfMemoryException we get from JBoss after we deploy/re-deploy 6 or 7 times. Figure out the cause of that and we&#8217;d be laughing. 

On the productivity note, I&#8217;m looking at the potential integration of PMD/Checkstyle/Findbugs into our development process.

 [1]: http://www.wrytradesman.com/blog/archives/000034.html