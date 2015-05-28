---
title: 'JDIC and OS X : Revisited'
author: ajordens
layout: post
permalink: /2006/02/jdic-and-os-x-revisited/
categories:
  - Java
  - Open Source Software
---
I <a target="_blank" href="http://www.jordens.org/?p=151">blogged</a> a few days ago about an exception that was cropping up when doing a Desktop.open() on OS X.

Tonight I hacked out a simple solution.

Instead of

> Desktop.open(file);

I do:

> if (OSUtils.isMacintosh())  
> {  
> Runtime.getRuntime().exec(&#8220;open&#8221;, file);  
> }  
> else  
> {  
> Desktop.open(file)  
> }

OSUtils.isMacintosh() just does a check against &#8216;os.name&#8217; to see if it matches the signature of a macintosh.

Pretty simple. I haven&#8217;t actually tried it out in the application yet, but a simple test had it launching the native text editor so it *appears* to work as expected.