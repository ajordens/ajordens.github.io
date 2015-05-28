---
title: 'Mix &#038; Match : Open Source Software in a Commercial World'
author: ajordens
layout: post
permalink: /2003/11/mix-match-open-source-software-in-a-commercial-world/
categories:
  - Open Source Software
---
Ok, maybe its not totally a commercial world but heres the situation&#8230;

I&#8217;m involved in the development of a grid computing project with the primary goal of facilitating the sharing of data.

Choosing to go with the globus toolkit was pretty much a no brainer, its seemingly far along, has a fair number of users, and is easily deployable within t  
he open-source world.

The Globus Toolkit integrates rather seemlessly with tomcat but also comes with its own web services container which for this particular project was ideal.  
We&#8217;re running a JDK1.4.2 environment and all is well&#8230;

Introduce **Websphere**

Now I used to consider IBM a good company, but after getting down and dirty with their app server, portal server and eclipse-based development environment,  
I&#8217;d put my trust in their software at about the same level as Sun and iPlanet. My biggest peeve is the lack of support, by the major players, for anything  
beyond JDK1.3 and old GLIBC&#8217;s. Listen all you commercial application server (and DB for that matter), I don&#8217;t want to have to radically modify my developm  
ent environment to fit in with your world, and I shouldn&#8217;t have to. I don&#8217;t even want to get into the costs of these servers and development licenses, but  
for what its worth, one would expect these companies to at least make an effort to support a JDK that has been released for over a year or updated operatin  
g systems that were released over a year ago (notably RedHat 9.0, which is still unsupported by many pieces of IBM&#8217;s enterprise software).

Note to companies: If you&#8217;re expecting developers to do cutting edge things with your tool sets, make an effort to ensure that you&#8217;re going to make sure th  
ey have the proper support. I don&#8217;t want to bombarded with press about how great and easily it would be to develop grid apps in your environment, only to f  
ind out that I have to re-invent the wheel because existing solutions won&#8217;t run b/c simple library conflicts.

Thats enough of a rant for today. I will credit IBM with providing a relatively decent management interface for Websphere Application Server. If only they  
could get their act together on their messy Partnerworld download site.