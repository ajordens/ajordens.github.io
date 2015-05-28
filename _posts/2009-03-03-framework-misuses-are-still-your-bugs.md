---
title: Framework misuses are still your bugs.
author: ajordens
layout: post
permalink: /2009/03/framework-misuses-are-still-your-bugs/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
I spent a few hours tonight trying to diagnose a problem we were running into tonight with some web application code.

That was on top of the better part of a day that was spent by another developer digging into the code.

Development ain’t easy, and frameworks for all their glory strive to make the easy stuff easier and the difficult stuff… well it’s still difficult.

Take Seam for example, a couple simple @In annotations here and there, and all of a sudden you have an application up and running.&#160; 

But throw transactions and exceptions into the mix and the expected behaviour is up in the air.

Imagine the following scenario:

> Component A calls Component B.update() which in turn calls EntityManager.persist(someEntity).
> 
> someEntity fails a database constraint and an EntityAlreadyExists exception is propagated from Component B.update().&#160; 

Can Component A turn around and update someEntity and call Component B.update() again?

It depends.&#160; In Seam there is a RollbackInterceptor behind the scenes that will rollback any transaction crossing an injection boundary (*it’s slightly more complicated than that but we’ll leave that for another day*).&#160; 

If Component A was a POJO Transactional Seam component, and Component B was a Seam EntityHome component, this wouldn’t work.&#160; In this sitation, Component B throwing an exception would actually rollback the transaction before control was returned to Component A.&#160; Component A could very well handle the exception but the underlying transaction would still be rolled back.

From the looks of the implementation, the EntityHome (*Component B*) is relying on the entity existing in its PersistenceContext when doing an update.&#160; You can update() multiple times as long as the transaction remains open and long-running.

Throw an exception into the mix and that transaction is likely to get rolled back by the RollbackInterceptor and the persistence context reset.

From that point on, calling Component B.update() (*equivalent to EntityHome.update()*) is going to report a success but do nothing but flush an empty persistence context.&#160; 

&#160;

The short term fix was to have Component B.update() re-merge in *someEntity*.&#160; However, rather than perverting the framework, it likely makes sense to dig deeper into the implementations and merge Component A and Component B to prevent the RollbackInterceptor from firing and rolling back the transaction on an exception that is recoverable.

The things you learn!