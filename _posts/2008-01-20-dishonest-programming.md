---
title: Dishonest Programming
author: ajordens
layout: post
permalink: /2008/01/dishonest-programming/
categories:
  - General Discussions
  - Java
---
There was an interesting post (by [David Brady][1]) included in the most recent [dzone.com][2] email that discussed the notion of <span style="font-style: italic;">Dishonest Programming</span>.

The last sentence does a decent job of summarizing the author&#8217;s thoughts:

<p style="margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Helvetica">
  <blockquote>
    <p>
      Any time you feel yourself being clever, ask yourself a key question: are you being deceptively simple, or simply deceptive?
    </p>
  </blockquote>
  
  <p>
    In my mind it boils down to a matter of transparency. As a developer we should be striving towards writing transparent code. It&#8217;s easier to test, easier to maintain, and most importantly we&#8217;ll be setting a good example for others to follow.
  </p>
  
  <ol>
    <li>
      <span style="font-style: italic;"><strong>Ensure that implementation artifacts (interfaces, classes, methods and variables) are named for what they actually do</strong>.</span> Simple enough.
    </li>
    <li>
      <strong><span style="font-style: italic;">Ensure side-effects are known and documented.</span> <span style="font-weight: normal;">Pay attention to state and how it&#8217;s being maintained and manipulated. Prefer a stateless business tier and avoid <span style="font-style: italic;">undocumented data caches</span>. The latter are trivially introduced and a pain to eliminate.</span></strong>
    </li>
    <li>
      <span style="font-style: italic; font-weight: bold;">Immutability is good.</span> Final classes, final methods and final variables. Pay attention to the mutability of return types as well.
    </li>
  </ol>
  
  <p>
    Keep It Simple &#8230; and save the complexity for the kitchen.
  </p>
  
  <p>
    As a developer, it&#8217;s amazing the difference in motivation you have when you&#8217;re working in a coherent and well-structure code base. It&#8217;s a difficult stage to get to (and maintain) but it must always remain a goal.
  </p>
  
  <p>
    Adhering to a few simple rules will not only make you a better developer but will also improve the overall efficiency of your team.
  </p>

 [1]: http://chalain.livejournal.com/
 [2]: http://www.dzone.com