---
title: 'Reflected toString() methods : My Take'
author: ajordens
layout: post
permalink: /2005/02/reflected-tostring-methods-my-take/
categories:
  - General Discussions
---
There was a post [here][1] that advocates using the ReflectiveToStringBuilder from commons-lang t  
o generate your toString()&#8217;s. 

I must admit that I too have thought about doing this. In particular after looking at the common-lang usage in some Matt Raible&#8217;s code. It&#8217;s a neat idea  
but I think its practicality is determined by the architecture and environment you&#8217;re working in. I first attempted to use it in my hibernate-backed appli  
cation as a way to get debug information out of the value objects. Potential problem #1, executing a reflective toString() on an object with lazily loaded  
collections, you could possibly recursively load a lot more data than you anticipated and even create an infinite loop depending on how your data model is  
mapped. Couple this with the lack of tweakability and possibility of security-related exceptions make this a practice I wouldn&#8217;t encourage.

Rumour has it IDEA has a toString() generator that you can tweak, I should look for something equivalent in an Eclipse plug-in.

 [1]: http://www.logemann.org/day/archives/000147.html