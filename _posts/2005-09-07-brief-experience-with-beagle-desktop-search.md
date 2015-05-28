---
title: 'Brief Experience with &#8216;Beagle&#8217; Desktop Search'
author: ajordens
layout: post
permalink: /2005/09/brief-experience-with-beagle-desktop-search/
categories:
  - General Discussions
---
For some time I&#8217;ve been wanting to try out the &#8216;[Beagle][1]&#8216; desktop searching engine on my linux desktop. 

There&#8217;s an article/review of it over on [LinuxForums][2].

**What is Beagle?**

Beagle is a desktop search engine written by Nat Friedman (of Gnome/Ximian) fame. It is written in C# using [Mono][3] and [Gtk#][4]. The indexing is handled by [DotLucene][5] a C# port of the Lucene indexer.

A [FAQ][6] is available on their [wiki][1].

It was quite trival to install on my Debian unstable box.

> apt-get update  
> apt-get install beagle
> 
> beagle-settings  
> searchomatic

I haven&#8217;t really done anything beyond some simple email searches, but more or less it returned the results I would expect. 

Surely, a step in the right direction.

 [1]: http://beaglewiki.org/Main_Page
 [2]: http://www.linuxforums.org/news/article-54153.html
 [3]: http://mono-project.com
 [4]: http://gtk-sharp.sourceforge.net/
 [5]: http://www.dotlucene.net/
 [6]: http://http://beaglewiki.org/FAQ