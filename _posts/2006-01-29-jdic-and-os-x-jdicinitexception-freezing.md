---
title: 'JDIC and OS X : JdicInitException &#038; Freezing'
author: ajordens
layout: post
permalink: /2006/01/jdic-and-os-x-jdicinitexception-freezing/
categories:
  - General Discussions
---
One of our customers (a mac user) has recently reported an issue that appears to stem from somewhere in execution trace of a JDIC/native Desktop call.

The issue we&#8217;re having is exactly similar to this <a target="_blank" href="http://www.javadesktop.org/forums/thread.jspa?forumID=52&#038;threadID=13871&#038;messageID=95953#95953">thread</a> in the JDIC forum which unfortunately hasn&#8217;t been answered.

Our code is doing the following:

> try  
> {  
> Desktop.open(localFile);  
> }  
> catch (Exception e)  
> {  
> // some generic exception handling  
> }

It looks like the JdicInitException is happening on the first call to Desktop.open, but the call actually succeeds and the document is opened. I&#8217;ve actually been able to make 6 or 7 calls to Desktop.open() without a problem. However, eventually the application does lockup (without dumping another exception stacktrace).

The stack trace is as follows:

> org.jdesktop.jdic.init.JdicInitException: java.lang.UnsatisfiedLinkError: getEnv  
> at org.jdesktop.jdic.init.JdicManager.initShareNative(Unknown Source)  
> at org.jdesktop.jdic.desktop.internal.ServiceManager.(Unknown Source)  
> at org.jdesktop.jdic.desktop.Desktop.open(Unknown Source)  
> at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)  
> at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:39)  
> at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)

Anyone else run into a similar issue and have a solution? The client is running JDK 1.4.2_09. Also, does anyone have an OS X binary for JDIC newer than 0.8.6.x ?