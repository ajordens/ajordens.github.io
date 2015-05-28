---
title: 'OS X + Java6: java.lang.UnsatisfiedLinkError: /usr/lib/java/libObjCJava.A.dylib'
author: ajordens
layout: post
permalink: /2008/06/os-x-java6-javalangunsatisfiedlinkerror-usrlibjavalibobjcjavaadylib/
categories:
  - General Discussions
  - Java
---
We recently finished migrating our product from Java5 to Java6. The software migration itself went quite smoothly with only a couple unanticipated problems.

However we do have a number of developers on MacBook Pro&#8217;s (*myself included*) that began having problems with other Java-based applications after making Java6 their default JVM.

One such problem was with the popular [Spark][1] IM client. After upgrading to Java6 we started getting the following exception:

> **macos:/Applications/Spark.app/Contents/MacOS ajordens**$ ./JavaApplicationStub 

> *NSRuntime.loadLibrary(/usr/lib/java/libObjCJava.dylib) error.* 

> *java.lang.UnsatisfiedLinkError: /usr/lib/java/libObjCJava.A.dylib:  
> at java.lang.ClassLoader$NativeLibrary.load(Native Method)  
> at java.lang.ClassLoader.loadLibrary0(ClassLoader.java:1822)  
> at java.lang.ClassLoader.loadLibrary(ClassLoader.java:1702)  
> at java.lang.Runtime.load0(Runtime.java:770)  
> at java.lang.System.load(System.java:1005)  
> at com.apple.cocoa.foundation.NSRuntime.loadLibrary(NSRuntime.java:127)* 

Revert back to Java6 and the problems disappeared.

**Solution:**

Reverting back to Java5 for a particular application was about the only suggestion I&#8217;ve seen that has actually worked.

Fortunately, you should be able to apply the change directly to the problem application&#8217;s **Info.plist** and not system-wide. Best of both worlds in a way.

*  
*

*Using the Spark example:*

Edit **/Applications/Spark.app/Contents/Info.plist** and change the value associated with the **JVMVersion key** to be **1.5** instead of **1.5+**.

Similar to a JNLP file, this will result in the runtime falling back to 1.5.0.

 [1]: http://www.igniterealtime.org/projects/spark/index.jsp