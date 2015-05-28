---
title: Useful Aspects
author: ajordens
layout: post
permalink: /2006/02/useful-aspects/
categories:
  - Java
---
We&#8217;ve recently gone through a migration from 1.4.2 to 5.0.

I haven&#8217;t really had the opportunity to experiment with aspects much beyond the transaction management aspects provided by the Spring framework.

That being said, there were a couple interesting aspects on [clientjava][1] today:

  1. [SyncModel Aspect][2]
  2. [JavaBean Aspect][3]

The SyncModel aspect is basically a method-level annotation that will spin method invocation off of the EDT thread (similar to SwingWorker/Spin/Foxtrot, etc). I haven&#8217;t used it but it looks interesting.

> *With all of that said, I don’t know that AOP can really solve all of your swing threading issues. While the aspect does work rather well, this is not a good solution for tasks that need to be able to be canceled or used in a progress bar. But for short little tasks that can cause brief lockups in the GUI, this could be a reasonable solution.*

I would agree. If nothing else, it&#8217;s a good talking point.

The JavaBean aspect also looks interesting and is a mechanism for annotating a data model class so that it can be used in combination with the JGoodies binding framework. I haven&#8217;t worked much with the JGoodies binding framework so I can&#8217;t really comment any more than that. It definitely looks interesting and when I have some cycles I&#8217;ll start playing with it. A couple years back I did hack out a basic binding framework and its interesting to see the similarities to Karsten&#8217;s work.

 [1]: http://www.clientjava.com
 [2]: http://www.damnhandy.com/?page_id=52
 [3]: http://www.damnhandy.com/?page_id=17