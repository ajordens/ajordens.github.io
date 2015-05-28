---
title: Seagate announces encrypted laptop drives
author: ajordens
layout: post
permalink: /2005/06/seagate-announces-encrypted-laptop-drives/
categories:
  - General Discussions
---
I was actually chatting with a co-worker today about the threat posed by one of us (or for that matter, anyone travelling) losing a laptop. Just getting caught up on my blog reading duties and came across this [ArsTechnica post][1] on the subject. 

Sounds like Seagate will start shipping drives next year with native hardware-level Triple DES encryption. There is no performance penalty for this at-the-core encryption which could help address the problem, at least it&#8217;s better than nothing. I&#8217;m not really a security buff so I won&#8217;t comment on the actual viability of preventing access to 3DES-encrypted data from a very determined individual. It does have a 168bit key length which should prevent a strictly bruteforce attack.

Recently I wrote a little encryption utility that used AES (actually supported all standard encryption mechanisms but AES was the default) which [WikiPedia ][2]mentions as being the successor to 3DES (as determined after a public competition). AES has a fairly efficiently algorithm implementable in software that offers the same or better encryption strength than triple des. The same article goes on to say that 3DES has not yet been broken but suffers from algorithm slowness when implemented in software. The Seagate solution will implement it in hardware which should negate this drawback.

 [1]: http://arstechnica.com/news.ars/post/20050621-5019.html
 [2]: http://en.wikipedia.org/wiki/Triple_DES