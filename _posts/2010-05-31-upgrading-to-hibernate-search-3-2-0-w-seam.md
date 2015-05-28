---
title: Upgrading to Hibernate Search 3.2.0 (w/ Seam)
author: ajordens
layout: post
permalink: /2010/05/upgrading-to-hibernate-search-3-2-0-w-seam/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
A couple weeks back I set out to upgrade the version of Hibernate Search that one of our applications was using. 

The boys at JBoss had recently [released][1] Hibernate Search 3.2.0 and it looked pretty sweet. The possibility of performance improvements around indexing was enough to make me upgrade.

Unfortunately, like most software frameworks, Hibernate Search introduced/forced some new dependencies on us. We had previously been using Seam 2.2.0 and Hibernate 3.3.0 (*both JPA1*), neither of which were compatible with Hibernate Search 3.2.0.

We&#8217;re using Maven, so I&#8217;ll quickly outline the dependency changes I had to make (*all dependences are available via the *[*JBoss Nexus Repository*][2]):

> <font size="2" face="Verdana"><dependency> <br />&#160;&#160;&#160; <groupId>javax.persistence</groupId> <br />&#160;&#160;&#160; <artifactId>persistence-api</artifactId> <br />&#160;&#160;&#160; <!&#8211; bit of a hack to make sure we aren&#8217;t transitively pulling in the persistence api (should be referencing hibernate-jpa-2.0-api now) –-> <br />&#160;&#160;&#160; <version>explicitly-fail</version> <br /></dependency></font>

javax.persistence:persistence-api is the JPA1 API and is no longer relevant and should never be included as a dependency. The *explicitly-fail* version will trigger a build failure if it ever manages to sneak in.

> <font size="2" face="Verdana"><dependency> <br /> <groupId>org.hibernate.javax.persistence</groupId> <br /> <artifactId>hibernate-jpa-2.0-api</artifactId> <br /> <version>1.0.0.Final</version> <br /></dependency></font> 

org.hibernate.javax.persistence:hibernate-jpa-2.0-api is the new JPA2 API published by Hibernate.&#160; 

All previous hibernate dependencies had to be upgraded to **3.5.2.Final**, and Hibernate Search bumped up to** 3.2.0.Final**.

If you&#8217;re using Seam, you&#8217;ll also need to upgrade it to **2.2.1.CR1**.&#160; Note that this is not yet a final release but is necessary in order to support JPA2.

Unfortunately, Seam **2.2.1.CR1** lacks a complete Hibernate Search integration.&#160; I could no longer able properly inject a FullTextEntityManager (*via @In*).

Instead I was forced to obtain a FullTextSession programmatically:

> <font face="Verdana">private FullTextSession getFullTextSession() <br />{ <br />&#160;&#160;&#160; Session session = (Session) entityManager.getDelegate(); <br />&#160;&#160;&#160; return Search.getFullTextSession&#160; (session.getSessionFactory().getCurrentSession()); <br />}</font>

Seam also enhanced it&#8217;s EntityManager so that it now returns a JDK proxy when getDelegate() is called.&#160; 

That would be fine and dandy, but unfortunately the proxy does not implement org.hibernate.classic.Session, as required by the FullTextSession in Hibernate Search.&#160; 

Session.getSessionFactory().getCurrentSession() will return an org.hibernate.classic.Session and does allow you to move forward.&#160; 

A bit annoying and hopefully something that will get corrected in the near future.&#160; I’m hoping that either Hibernate Search will be upgraded to not require a classic session, or Seam will provide an EntityManager delegate implementing the classic session interface. Better yet, Seam should just provide a fully supported integration with Hibernate Search 3.2.0. 

Honestly, that was about it as far as the upgrade went.&#160; We were able to index using either the new MassIndexer API or the old suggested best practice from Hibernate Search 3.1.&#160; 

It&#8217;s interesting to note that on my test system, the MassIndexer API was slower than the previous indexing code. The documentation does cover many different tuning possibilities so it’s entirely possible the situation could be improved.

Also, the MassIndexer API runs in a series of transactions and unless your timeout is set sufficiently high (*ie. higher than the default JBoss 5 minutes*), you will see transaction timeouts. 

I didn&#8217;t attempt to work around this and opt&#8217;d to stick with existing indexing code that already runs in a separate Seam @Asynchronous method (*thus avoiding timeouts*).

Somewhat less than ideal, but if you&#8217;re keen on running Hibernate Search 3.2.0 w/ Seam in JBoss 4.2.3, it **is possible* ***and not too much work.

 [1]: http://in.relation.to/Bloggers/HibernateSearch32ReleasedMappingMassIndexingClustering
 [2]: http://relation.to/Bloggers/JBossMavenRepositoryChanges