---
title: Testing with Unitils
author: ajordens
layout: post
permalink: /2008/08/testing-with-unitils/
categories:
  - Database
  - General Discussions
  - Java
---
I was doing some reading and came across [Unitils][1] (1.1 was just [released][2]).

> Unitils is an open source library aimed at making unit testing easy and maintainable. Unitils builds further on existing libraries like DBUnit and EasyMock and integrates with JUnit and TestNG .
> 
> Unitils provides general asserion utilities, support for database testing, support for testing with mock objects and offers integration with Spring , Hibernate and the Java Persistence API (JPA). It has been designed to offer these services to unit tests in a very configurable and loosely coupled way. As a result, services can be added and extended very easily.

What particularly caught my attention was the support they&#8217;ve included for *transactional* test cases. By transactional, I mean test cases that will automatically cleanup after themselves. Simply include a @Transactional and you&#8217;re rocking.

In the past, we&#8217;ve rolled this capability ourselves with varying degrees of success. It&#8217;s easy to support rolling back of inserts but somewhat difficult to handle rolling back of deletes and other data mutations.

I&#8217;m just in the process of kicking off some new product development (*actually, we&#8217;re one week into it but who&#8217;s counting*) and general infrastructure (*testing included*) is something forefront on our minds.

For starters, we&#8217;ve got *Cobertura* and *Selenium* integrated into our build. General unit is covered with *TestNG* with Seam components integration tested using *SeamTest/Embedded JBoss*. Everything short of the *Selenium* tests are hitting freshly initialized in-memory databases.

It might be worth considering something like Unitils at this stage rather than building out our own tooling to accomplish much the same thing.

 [1]: http://www.unitils.org
 [2]: http://www.theserverside.com/news/thread.tss?thread_id=50487