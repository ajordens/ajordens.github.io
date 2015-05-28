---
title: Search Engine Ping Support versus Sitemaps
author: ajordens
layout: post
permalink: /2005/06/search-engine-ping-support-versus-sitemaps/
categories:
  - General Discussions
  - Open Source Software
---
Jeremy Zawodny has a good [writeup][1] where he poses the question, what if search engines listened to pings? or offered a compatible ping API?

I&#8217;m not involved with search but I do agree with his four critical variables about getting search right. Now I&#8217;ve only taken a cursory look at Google Sitemaps and haven&#8217;t yet attempted to roll it out, but from what I&#8217;ve read of the FAQ the concept will improve comprehensiveness and help freshness to the extent that we can provide hints on update frequency, pages to index, etc. Basically it will make the job of the crawler easier and hopefully more relevant. Google does provide ping-like interface for submitting (and re-submitting) sitemaps so functionality-wise, it isn&#8217;t all that different from weblog pinging, just a lack of support by existing tools.

I&#8217;m also not convinced that by opening a public weblog-like ping service that the amount of bunk requests (from spammers or otherwise) would pose an unsurmountable problem to a company like Google (or Yahoo or Microsoft for that matter). I agree with Jeremy&#8217;s comment that with an installed base of several million ping generators, does it really make sense to re-invent the wheel.

I see support for sitemaps as a step along the evolutionary trail towards more comprehensive indexing, improved ping support might come next, who knows? Some might consider Google Sitemaps to be a step sideways in implementation, but I&#8217;ll wait and see what kind of value it presents before passing judgement.

 [1]: http://jeremy.zawodny.com/blog/archives/004759.html