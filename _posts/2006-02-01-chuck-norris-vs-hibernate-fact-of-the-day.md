---
title: 'Chuck Norris vs Hibernate : Fact of the Day'
author: ajordens
layout: post
permalink: /2006/02/chuck-norris-vs-hibernate-fact-of-the-day/
categories:
  - General Discussions
---
For some reason <a href="http://www.jordens.org/wp-admin/chucknorrisfacts.com" target="_blank">chucknorrisfacts.com</a> has been spreading like wildfire throughout the office.  After dealing with some Hibernate lameness today, I thought I&#8217;d add a new fact. 

> If Chuck Norris were to re-write Hibernate, he&#8217;d have it done yesterday without any bugs.

The issue I was having with Hibernate today was some nasty logger usage occuring within a catch{} block.  I&#8217;m sure Gavin had his reasons, but I generally consider this type of explicit logging before re-throwing inside of a try/catch to be an annoying practice.  It popped up today as we were writing unit tests that expected the exception to get thrown minus the annoying ERROR messages filling up our console.  My less-than-ideal solution was to bump the logging level up for the AbstractBatcher to FATAL.

> BatchingBatcher.java
> 
> try  
> {  
>     if (batchSize!=0)  
>     {  
>         // do something  
>     }  
> }  
> catch (RuntimeException re)  
> {  
>     log.error(&#8220;Exception executing batch: &#8220;, re);  
>     throw re;  
> }  
> finally  
> {  
>     // cleanup  
> }

I did a quick check and noticed the same usage existed in 3.1.1 (we&#8217;re still using 3.0).  Also noticed that there were a few other cases where logging was occuring from within the scope of a try/catch.

Is there a reason?