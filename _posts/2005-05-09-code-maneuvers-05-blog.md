---
title: Code Maneuvers 05 Blog
author: ajordens
layout: post
permalink: /2005/05/code-maneuvers-05-blog/
categories:
  - Java
---
Went to Sun&#8217;s Code Maneuvers 05 Session last Monday in Vancouver, B.C.

I&#8217;ve included notes on some of the talks below. It was alright, nothing too spectular or ground breaking for me but the overviews provided were beneficial  
to others in my group.

The following notes are unfiltered. I didn&#8217;t have my laptop on at all times nor was I present for all presentations. 

==============================

Keynote

Missed the keynote but the buffet on the ferry was good. Supposedly it was about J2ME and looked cool.

J2SE 5.0

Missed the first half of this presentation but it was a good overview of whats  
new in tiger. New foreach, generics and annotations look worthwhile. Missed the comments on the new concurrency utilities.

Java Web Services

Personally I don&#8217;t have an interest in web services so I pretty much just zzz&#8217;d through this presentation. Was a little bit overly focused on Sun&#8217;s spec f  
or JBI. The whole service oriented architecture sounds plausible but also just makes sense when developing. They showed a before and after picture of goi  
ng from a &#8216;traditional&#8217; system to a SOA system. Sure SOA painted a prettier picture but in reality, you&#8217;re going to be re-using components either way. Ta  
king a web services would make hooking up a distributed system easier but I&#8217;m of the belief that SOA is more marketing than true breakthrough.

J2EE Persistence

Nothing new here. Touched on CMP, JDO, Hibernate, etc. Was 45 minutes long and didn&#8217;t touch on anything I didn&#8217;t already know. We had 2 coops with us so  
it was valuable for them.

Java Studio Creator

I&#8217;m an eclipse user. Not too interested in switching ide&#8217;s at this point. Started talking about java server faces and got into how Java Studio Creator ca  
n make your life easier.

CodeCamp: J2SE &#038; J2EE Performance

Use StringBuilder instead of StringBuffer for unsynchronized cases. Performance improvement in JDK 5.0. New smart tuning techniques should do as good a j  
ob as hand tuning (eliminates the need for setting heap sizes, etc). GC mechanisms are different between client/server configurations (server has parallel  
gc&#8217;s, client has serial).

Use ArrayList vs. Vector for unsynchronized cases (Vector&#8217;s methods are synchornized). 

JDK 5.0 has native threading support. 

Server class machine > 2 CPUs, 2GB Ram  
Heap initially 1/64th physical memory, max 1/4 physical mem (up to 1gb). User is able to specify throughput and JVM will try and reach it.

NetBeans sets XX:PermSize to 20MB, XX:MaxPermSize (added performance??)

General Tuning Advice:  
1. Continue profiling. Look for bottlenecks and adjust parameters to optimize performance (GC tuning, etc).  
2. Allocate more memory to JVM (64MB is default)  
3. Set -Xms and -Xmx to be the same (increases predictability, improves startup time)

&#8216;GC Portal&#8217; can be used to analyze &#8216;verbose:gc&#8217; output (not sure if JDK 5.0 only???)  
Use Jconsole to connect to local and remote applications (JDK 5.0 only feature but looks cool)  
Could also use visualgc to visual gc

http://java.sun.com/developer/technicalArticles/Programming/GCPortal

J2EE  
Cache EJB references to avoid JNDI lookups  
Cache bean specific resources in setSessionContext() or ejbCreate() (release resources in ejbRemove())  
Remove stateful session beans when not needed

Caching is used when number of concurrent users of beans exceeds that of maximum allowable number of bean instances.  
Avoid passivation (modify pool sizes, etc.)

Ensure initial and max values of pool size are representative of normal and peak loads. Incorrect values could leave to unnecessary object creation and GC  
.

Cache too big, longer and more frequent full GCs. Application server might run out of memory.  
Cache too small, lots of passivation and activation, serialization and de-serialization. 

Bigger cache for frequently used beans.  
Entity bean caches larger than session bean caches.  
Mark entity beans as read-only or read-mostly.

Commit option B avoids ejbActivate()/ejbPassivate() (usually better performance)  
Commit option C better if beans in cache are rarely used.

To determine what to use, look at the cache-hits value using ejb server monitoring tools. 

Misc Tuning: Avoid excessive directories in server classpath (affects class loading times).

sridhar.reddy@sun.com about getting notes