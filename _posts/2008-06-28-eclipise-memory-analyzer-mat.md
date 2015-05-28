---
title: Eclipise Memory Analyzer (MAT)
author: ajordens
layout: post
permalink: /2008/06/eclipise-memory-analyzer-mat/
categories:
  - citations
  - Java
  - Open Source Software
---
I must say the [Eclipse Memory Analyzer][1] looks pretty slick. There is some pretty good material over on the [developers blog][2]. Lastly, there was a talk on it at JavaOne 2008 titled &#8216;*Automated Heap Dump Analysis for Developers, Testers, and Support Employees*&#8216; ([multimedia recording][3]).

> The Eclipse Memory Analyzer is a fast and feature-rich Java heap analyzer that helps you find memory leaks and reduce memory consumption.
> 
> The Memory Analyzer was developed to analyze productive heap dumps with hundreds of millions of objects. Once the heap dump is parsed, you can re-open it instantly, immediately get the retained size of single objects and quickly approximate the retained size of a set of objects. The reference chain to the Garbage Collection Roots then details why the object is not garbage collected.
> 
> Using these features, a report automatically extracts leak suspects. It includes details about the objects accumulated, the path to the GC Roots, plus general information like system properties.

The tool was actually contributed by SAP and is currently an incubation project over at Eclipse. It&#8217;s available as both an *eclipse feature* and a standalone ***eclipse RCP*** application.

Kudos to the team for taking the time to provide a standalone package!

 [1]: http://www.eclipse.org/mat/
 [2]: http://dev.eclipse.org/blogs/memoryanalyzer/
 [3]: http://developers.sun.com/learning/javaoneonline/j1sessn.jsp?sessn=TS-5729&yr=2008&track=tools