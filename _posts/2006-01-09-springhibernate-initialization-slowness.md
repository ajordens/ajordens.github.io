---
title: Spring/Hibernate Initialization Slowness
author: ajordens
layout: post
permalink: /2006/01/springhibernate-initialization-slowness/
categories:
  - General Discussions
---
As I commented in an earlier post, we&#8217;ve been transitioning our legacy EJB-based system to a new platform built largely on Spring and leverging hibernate for persistence.

The technology has worked well, I&#8217;ve seen improvements by way of code reduction and ease of implementation in certain areas. Instead of 500 remote methods exposed via 30-odd session beans (and stateful ones at that for a reason I won&#8217;t get into now), I&#8217;ve implemented a fairly straight forward command pattern variation that combines a metadata layer with EJB/MDB and Spring execution end-points. Persistence is easier, and a custom DSL built-on top of HQL has allowed us to replace nearly all of our EJBQL and CMP-code generically.

However, all is not bliss. We&#8217;re suffering from a bit of technical debt. We attempted somewhat of a model-driven approach with effort put into developing a UML model of our existing schema (and some sequence/class diagrams). The original goal was to use andromda tags to annotate our model and produce useful hibernate mapping files. It sounded good in practice, but of course it didn&#8217;t work as expected (and really wasn&#8217;t that big of a surprise either). We&#8217;ve annotated a lot of the model, but there are a number of hibernate features not supported by andromda that required some post-processing tweaking in Perl. 

The other significant drawback I&#8217;ve noticed is slowness at initialization time. I know that we&#8217;ve introduced a lot of overhead in the parsing and interpretation of our own metadata layer, but there appears to be sufficient overhead in the initialization and preparation of the 130-odd Hibernate mapping files and 40-50 Spring beans. Disabling cglib has not shown much in the way of improvement, but we&#8217;re still investigating and profiling.

The last problem is one that was faced even in the old legacy system. Every 5 or 6 deploys we get an out of memory exception in JBoss. In the legacy system it was a regular OutOfMemoryException, in the new hibernate/spring platform (still deployed to JBoss with an EJB3 SLSB and MDB) we get out of memory problems in the Permgen space. I&#8217;m not the only one with this [problem][1] and it&#8217;s affecting all of our developers. I&#8217;ve bumped up the memory allocated to permgen to 128MB but that only delays the problem. 

If anyone has any suggestions or ideas, feel free to comment.

 [1]: http://www.google.ca/search?hl=en&#038;q=permgen+outofmemory&#038;btnG=Google+Search&#038;meta=