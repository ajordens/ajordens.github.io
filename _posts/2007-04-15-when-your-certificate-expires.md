---
title: When Your Certificate Expires
author: ajordens
layout: post
permalink: /2007/04/when-your-certificate-expires/
categories:
  - General Discussions
---
Funny thing happened at work the other day, turns out the *Personal Email Certificate* we were using to enable SSL communication between client and server expired.

Not a good thing to have happen when you have customers across North America and Europe that are no longer able to run your application.

Fortunately for us, we were able to make quick turnaround and have a minor patch out to customers that involved re-code signing our distribution jars with a proper Verisign certificate and providing an updated keystore containing a new certificate*.*

The saga of the personal email certificate begain a year or two back. Basically we investigating a requirement to code sign and support SSL encryption between client/server (another related requirement involved providing HTTPS access to the web portion of our application). There&#8217;s an interesting [blog][1] about using Thawte email certificates to handle all of this. Two bonuses, they&#8217;re free and Thawte is an actual certificate authority that does exist in java, your browser, etc. (so none of the typical self-signer popups). We were developing and testing a solution so the Thawte *freebie* certificate were handy. The problem for us is that, in production, we only addressed usages of the free certificate that were customer visible, notably the code signing (because you still have a Java Webstart popup w/ Thawte Freemailer as the authority). 

Fortunately for us, we realized the problem internally before any (or most) customers noticed a problem. Our customer support team was on the ball and let customers know they would need an emergency patch. Development had a patch ready within a couple of hours, and we were good to go. Nice team effort. Rather annoying problem, but a good hands-on approach to ensuring customer satisfaction.

Reminder to everyone, certificates don&#8217;t last forever (personal or otherwise) and when they expire, if they&#8217;re being used to support important infrastructure, all hell will break lose.

 [1]: http://developer.blog.com/