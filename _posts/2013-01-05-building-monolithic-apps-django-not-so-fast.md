---
title: Building Monolithic Apps (Django?), Not So Fast.
author: ajordens
layout: post
permalink: /2013/01/building-monolithic-apps-django-not-so-fast/
categories:
  - General Discussions
  - Java
---
<!--?xml version="1.0" encoding="UTF-8" standalone="no"?-->

<span style="font-size: 14px;">Over the past few years (<em>in my personal life</em>) I&#8217;ve built a handful and launched a handful of web applications, predominately built using Django.  </span>

<div style="font-family: Arial;">
  <span style="font-size: 14px;"><br /></span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 14px;">Professionally, I&#8217;m a JVM developer who&#8217;s witnessed the shift from Java to alternative JVM languages like Groovy (<em>I&#8217;m a big time fan</em>), and a growing disfavour with full stack frameworks like Spring and Hibernate.  </span></p>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">Don&#8217;t get me wrong, both Spring and Hibernate have massive developer communities, but there&#8217;s a subset of the population looking for simplicity and less magic.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;"><strong><span style="text-decoration: underline;">TL;DR</span></strong> &#8211; Django is nice, monolithic is bad.  I used to love Spring and Hibernate, but nowadays I feel like they&#8217;ve run their course and are no longer the defacto choice like they were in 2005-2010. Currently, my preferred stack includes Dropwizard (micro web service development) + AngularJS, but could just as well include Flask or a combination of both.  Be aware of behind-the-scenes framework magic (such as in Grails, Hibernate, Django, etc.), if you cannot easily reason around what it&#8217;s doing, someone will end up in debug / maintenance hell eventually.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">In the end, do what feels right to you, be agile and put the effort in <strong>to build applications that you&#8217;re proud of</strong>.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">Hit me <a href="http://twitter.com/ajordens">@ajordens</a> to continue this conversation.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <strong style="font-size: 14px;">What&#8217;s my definition of an application?</strong>
  </div>

  <div>
    <strong style="font-size: 14px;"><br /></strong>
  </div>

  <div>
    <span style="font-size: 14px;">An application consists of services, data and user interface.  </span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">Furthermore, most applications I&#8217;ve seen can be sliced into one or more verticals, each slice delivering one or more services and a user interface.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">This slicing provides implementation flexibility, a small team of engineers (or perhaps even just one) can easily own an entire vertical soup to nuts. Verticals are integrated by way of APIs and previously agreed upon URI semantics.  </span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">Deployment flexibility is achieved using a tried and true web proxy like Apache or Nginx that fronts your vertical stacks deployed across a fleet of internal servers (or elastic load balancers in AWS).</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <strong style="font-size: 14px;">Monolithic?</strong>
  </div>

  <div>
    <strong style="font-size: 14px;"><br /></strong>
  </div>

  <div>
    <span style="font-size: 14px;">Contrast the previous definition of an application with the typical monolithic deployment.  </span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">In the monolithic world, we&#8217;d typically build one artifact and deploy it to a number of servers.  A team of engineers would be responsible for the application and must all work in conjunction to ensure successful deployments and uptime.  </span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">The introduction of an error or critical bug by a team member has the potential to wreck a deployment and force a rollback.  This issue is not <em>completely</em> solved by moving to more service-oriented verticals, but is perhaps a little more palatable.  If an issue is discovered in one of the verticals, simply roll that individual slice back and hope that you don&#8217;t have too much coupling between services.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <strong style="font-size: 14px;">What&#8217;s my beef with Django?</strong>
  </div>

  <div>
    <strong style="font-size: 14px;"><br /></strong>
  </div>

  <div>
    <span style="font-size: 14px;">Don&#8217;t get me wrong, Django is nice. It&#8217;s got a great community and is relatively easy to jump in to.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">Probably the biggest issue I had with it, coming from the perspective of a JVM developer, was the lacklustre API frameworks at the time. </span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">I started off with django-piston, and in hindsight, the resulting code was a little ugly (<em>aka. not very pythonic &#8212; blame it on me, the developer if you will</em>).  Subsequently, I moved on to django-tastypie to much more success.  I&#8217;m not sure if there have been improvements this past year on either framework (<em>piston looks dead, tastypie is still somewhat active</em>), but IMO both frameworks pale in comparison to what&#8217;s available w/ JAX-RS on the JVM.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">Templating in Django is passable, although Jinja2 is much better than the default django templates IMO.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">The admin interface is great, and was a good tool to expose a couple management interfaces to non-developers. </span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">The out-of-the-box CRUD stuff worked well.  Some of the more complicated admin operations may have been better served as a dedicated admin service with a hand cranked JS interface.</span>
  </div>

  <div>
    <strong style="font-size: 14px;"><br /></strong>
  </div>

  <div>
    <span style="font-size: 14px;">This <a href="http://jokull.calepin.co/my-flask-to-django-experience.html">blog post</a> does a reasonable job of outlining a few other areas where Django is lacklustre when compared to Flask.</span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <strong style="font-size: 14px;">It&#8217;s not all bad.</strong>
  </div>

  <div>
    <strong style="font-size: 14px;"><br /></strong>
  </div>

  <div>
    <span style="font-size: 14px;">Truthfully, there is no silver bullet architecture that will guarantee a successful business.  </span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">There are millions of applications out there using Spring, Hibernate, Django, etc.  </span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <span style="font-size: 14px;">They run, make money, and require maintenance just as any application would.  </span>
  </div>

  <div>
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div>
    <strong style="font-size: 14px;">Do what feels right to you, be agile and put the effort in to build applications that you&#8217;re proud of.</strong>
  </div>
</div>
