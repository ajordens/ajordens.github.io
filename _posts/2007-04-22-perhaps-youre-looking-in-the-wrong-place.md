---
title: '&#8220;Perhaps You&#8217;re Looking in the Wrong Place&#8221;'
author: ajordens
layout: post
permalink: /2007/04/perhaps-youre-looking-in-the-wrong-place/
categories:
  - General Discussions
---
Interesting quote from a recent [interview][1] w/ bug fixer Brian Harry.

The quote itself is actually attributed to James Gosling but I like and can appreciate what Brian has added to it.

*&#8220;The place where you find bugs may not be the right place to put a fix in.&#8221;*

* </p> 

</em> 

Simple example of this: Damn, I&#8217;m getting a null pointer in this method, better wrap it in a: if (object != null) doSomething;

Sure, you&#8217;ve fixed a symptom but very rarely (or perhaps not necessarily) have you addressed the problem.

Another situation: Damn, hashCode() is slow, when I&#8217;m calling it 60 million times it&#8217;s taking forever. First thought, hashCode() is inefficient, let&#8217;s re-write them (maybe they&#8217;re using HashCodeBuilder or doing something inefficiently) and save 20%. Perhaps it&#8217;d be more worthwhile to look at why your hashCode() is getting invoked 60 million times, address that, and watch the overall time (total operation, not hashCode()) spent fall from 70s to < 2s.

We all love low hanging fruit, but we shouldn&#8217;t let it become a barrier to digging deeper.</p>

 [1]: http://java.sun.com/developer/technicalArticles/Interviews/community/harry_qa.html