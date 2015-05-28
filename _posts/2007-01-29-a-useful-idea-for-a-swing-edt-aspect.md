---
title: A Useful Idea for a Swing EDT Aspect?
author: ajordens
layout: post
permalink: /2007/01/a-useful-idea-for-a-swing-edt-aspect/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
I spent most of today debugging some performance problems we&#8217;re having in our application. It&#8217;s fun stuff, I really enjoy it. Lately it&#8217;s been a lot of threading work with Swing which is a fairly interesting area to play in. It&#8217;s amazing what kind of perceived performance improvements you can make by simply making appropriate use of background threads and obeying Swings threading rules.

The product in question is a swing-based desktop application that retrieves data from a remote application server, manipulates it and renders it on-screen. Pretty simple, right?

It really should be but being developers we like to make our lives difficult, especially if there&#8217;s nothing there to tell or warn us that perhaps our approach needs a second look.

I came across a little nugget this morning that involved a sort routine being called on a collection immediately after an item was added to it. Forget the fact that it was a List instead of a SortedSet (perhaps the biggest gotcha assuming we actually wanted a sorted collection), but to compound the problem (or perhaps make it more noticeable) the custom Comparator being used was expensive. It performed various substrings in order to perform a lexicographically correct sort. The problem was that this addItemToCollection() method was being invoked many hundreds and hundreds of times in succession, to the point where it was taking ~30-35s just to sort and insert items.

What made this difficult to track down was that it was functionality happening solely on the client-side and on the event dispatch thread. We&#8217;ve got logging in place so that we (the developers) will be notified when we&#8217;re doing something stupid like calling an expensive server call and blocking the EDT. However, we didn&#8217;t and still don&#8217;t have anything in place that will notify when we&#8217;re performing expensive business logic on the EDT and blocking it for a non-trivial length of time.

What I was thinking would be nice, is if you could write an aspect that would execute around various methods in the system (perhaps ones that you knew were potentially troublesome) and would trigger a notification in the event that the time spent executing (on the EDT) within the scope of the method was greater than some predetermined amount of time&#8230; say 10ms but even that is perhaps generous.

I&#8217;m not sure if the overhead of apply an aspect like this would completely through performance for a loop or if it&#8217;s even possible to do. I expect it is possible but I honestly haven&#8217;t done enough AOP to be certain. Regardless, I think it would make our lives as developers simpler and less error prone. Alternatively, perhaps there are some static code analysis tools that would be able to catch similar errors?