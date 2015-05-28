---
title: Large-scale Hadoop @ Yahoo! Search
author: ajordens
layout: post
permalink: /2008/02/large-scale-hadoop-yahoo-search/
categories:
  - citations
---
[Jeremy Zadowny][1] has mention of a very large scale Hadoop deployment over at Yahoo! Search.

It makes sense given their previous commitments and investments to the project but it&#8217;s also cool in a way to start seeing some significant migrations to the framework.

> <p style="font: 12.0px Helvetica">
>   <span style="font-style: italic;">Over on the</span> <a href="http://developer.yahoo.com/blogs/hadoop/"><span style="font-style: italic;">Yahoo! Hadoop</span></a> <span style="font-style: italic;">blog, you can read about how the</span> <a href="http://developer.yahoo.com/blogs/hadoop/2008/02/yahoo-worlds-largest-production-hadoop.html"><span style="font-style: italic;">webmap team in Yahoo! Search is using</span></a> <span style="font-style: italic;">the</span> <a href="http://hadoop.apache.org/core/"><span style="font-style: italic;">Apache Hadoop</span></a> <span style="font-style: italic;">distributed computing framework. They&#8217;re using over 10,000 CPU cores to build the map and processing a ton of data to do so. They end up using over 5 petabytes of raw disk storage, eventually outputting over 300 terabytes of compressed data that&#8217;s used to power every single search.</span>
> </p>

Another interesting quote from Eric Baldeschwieler (<span style="font-style: italic;">Senior Director, Grid Computing</span>):

<p style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; margin-left: 0px; font: 12px Helvetica;">
  <blockquote>
    <p>
      <span style="font-style: italic;">This process is not new (see the AltaVista connectivity server). What is new is the use of Hadoop. Hadoop has allowed us to run the identical processing we ran pre-Hadoop on the same cluster in 66% of the time our previous system took. It does that while simplifying administration. Further we believe that as we continue to scale up Hadoop, we will be able to scale up our production jobs as needed to larger cluster sizes.</span>
    </p>
  </blockquote>
  
  <p>
    Pretty impressive.
  </p>
  
  <p>
    As part of this announcement, Jeremy has posted an interview he did with a couple of the <span style="font-style: italic;">webmap</span> and <span style="font-style: italic;">grid computing</span> people. The video feed seems quite slow right now so you&#8217;ll have to be patient.
  </p>
  
  <p>
    <strong>Update: The video feed seems much better now. Check it out.</strong>
  </p>

 [1]: http://jeremy.zawodny.com/blog/archives/009992.html