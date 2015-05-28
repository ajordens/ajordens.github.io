---
title: Refactoring tools are fantastic and overrated
author: ajordens
layout: post
permalink: /2005/11/refactoring-tools-are-fantastic-and-overrated/
categories:
  - Java
  - Open Source Software
---
> Refactoring tools are fantastic. I am an IDEA fan, and I think their refactoring support is second to none.
> 
> However, as great as it all seems, I think that refactoring tools can be overrated compared to other important factors.
> 
> For example, I was watching someone on a typical Java project with a particular stack, and watching their deploy cycle was making me cringe.
> 
> Sure they tried to do a lot out of the container, blah blah, but at some point they had to keep testing in the browser, which meant rebuilds of their project, and tomcat doing reloads for non-trivial changes.
> 
> The project was a medium size, and the cycle was painful to watch.
> 
> As I was watching this happen for a period of days, I compared to another current project where I would make changes and hit reload in the browser to see test.
> 
> I am saving time consistently, on a minute by minute basis.
> 
> On the other hand, it is quite infrequent for me to sit there and wish that I had &#8220;insert name of fancy refactoring&#8221;. When this happens it can be a pain, that is for sure. I hope that tools get better and better for non Java/static languages.
> 
> However, the more I thought about the comparison, the more I realised the the theoretical in me &#8220;man i love those refactorings. I just need them!&#8221; was dwarfed by the pragmatic reality of &#8220;man it is so painful to work in that stack, having these slowdowns CONSTANTLY&#8221;. 

I tend to agree with [Dion][1]. 

I&#8217;m currently working on a fairly large enterprise java project (Client: Thick=Swing, Thin=Struts, Server: Session/Entity Beans with a partial migration to Hibernate/Spring). It&#8217;s gotten to the point where a full deploy (meaning dropping the tables, deploying the ear which will re-create the db, and populating a few reference records) was taking > 6 minutes. This was without any sort of automated per-build unit testing that would normally occur.

Don&#8217;t get me wrong, I love refactorings but as long as my editor doesn&#8217;t mess up my explicit/implicit structures during a refactoring, I&#8217;m quite content with the current state of things. 

I&#8217;m a big proponent of frequent deploys, tests, and commits. Where this falls down is when each iteration takes minutes to execute (in my early example, JBoss took 45s to start&#038;deploy with JRockit, and a build/deploy would take on the order of 4 minutes provided the database was not re-created).

Luckily we&#8217;re going through a fairly substantial re-architecture of our backend and a nice side-effect is that the build/deploy/test turn-around times appear to be going down. I&#8217;ve migrated to TestNG, Subversion, Hibernate, Spring and Java5. We&#8217;re still using JBoss as our application container but only serving a single EJB 3.0 stateless session bean facading a cleanly defined Spring-based infrastructure.

I was skeptical at first but I&#8217;m quite happy with the relative (compared to xdoclet) simplicity that JBoss&#8217; EJB 3.0 implementation offers. One class, one remote (pre-existing) interface and we&#8217;re done. 

The application of Spring on the client and server sides allow us to easily unit test inside and outside of the container. The in-server infrastructure is quite thin and easily tested. The re-architecting effort is still underway so I don&#8217;t have firm numbers on the efficiency savings (in terms of development/deployment time) but I would expect it to be at least an order of magnitude less.

 [1]: http://www.almaer.com/blog/archives/001102.html