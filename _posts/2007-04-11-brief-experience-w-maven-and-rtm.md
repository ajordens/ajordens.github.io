---
title: Brief Experience w/ Maven and RTM
author: ajordens
layout: post
permalink: /2007/04/brief-experience-w-maven-and-rtm/
categories:
  - General Discussions
---
I&#8217;ve spent a bit of time lately working with the Facebook API.

As part of learning the API, I was going to write a utility that would synchronize my Twitter status with my Facebook status. No brainer. Vice-versa would be nice as well but Facebook&#8217;s API is primarily read-only.

It really was, the only kicker was Facebook&#8217;s rather lame authentication process. Basically, if you&#8217;re a desktop application, you&#8217;re forced to open a browser window to validate a token and have the user authenticate directly with Facebook. Essentially, there&#8217;s no purely programmatic way to authenticate with Facebook. It&#8217;s well documented in this [thread][1] on the developers group. Attempting to circumvent the process is a violation of the ToS.

Rather than fight with it any longer, I moved on to play with another API. I&#8217;ve recently started using [Remember the Milk][2] for tracking tasks, etc. Rather than use python or ruby, I decided to build a Java-based API for their exposed REST services. The plan eventually will be to pull some statistics from the service.

It&#8217;s still a work in progress but it&#8217;s fairly straight forward so far. The most interesting part of the exercise is actually using Maven for managing is that I decided to use Maven for managing the project. Having never used Maven it was nice to see something just work out of the box. The only configuration required was to add a few extra dependencies to the pom.xml and force the maven compiler to *-source 1.5*. I use IntelliJ IDEA so generating project files was as simple as *mvn idea:idea*. A minor tweak of *pom* downloaded and linked the source for dependent libraries.

I&#8217;m impressed.

I just wish we could replace our existing *ant-*based build system at work with Maven. I&#8217;m not the only one who would love to have a sane and deterministic build process. It sure would make easier to say, *No, you really can&#8217;t do that.*

 [1]: http://developers.facebook.com/topic.php?uid=2205007948&topic=1663
 [2]: http://www.rememberthemilk.com