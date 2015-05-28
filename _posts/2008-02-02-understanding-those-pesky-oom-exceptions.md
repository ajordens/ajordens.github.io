---
title: Understanding those pesky OOM exceptions
author: ajordens
layout: post
permalink: /2008/02/understanding-those-pesky-oom-exceptions/
categories:
  - citations
---
[JVM Lies : The OutOfMemory Myth][1]

It&#8217;s also been covered (with even more comments) over on [TSS][2].

It&#8217;s certainly beneficial for a developer to have a basic understanding of Java&#8217;s approach to memory management. This post (and comments) does provide a simple overview and discusses some of the causes and gotchas for those ever annoying OutOfMemory exceptions.

If there&#8217;s one thing to take note of, it&#8217;s that no<span style="font-style: italic;"><span style="font-style: normal;">t</span> <strong>all memory problems can be solved by an increase in the heap allocation</strong></span>. So please don&#8217;t do that and just walk away, it&#8217;s never a one size fits all problem and will almost certainly come back to bite you.

<span style="font-style: italic;">(If you&#8217;re like me, I&#8217;m sure you all love a good PermGen-related OOM&#8230; uhh&#8230; maybe not.)</span>

 [1]: http://www.codingthearchitecture.com/2008/01/14/jvm_lies_the_outofmemory_myth.html
 [2]: http://www.theserverside.com/news/thread.tss?thread_id=48112