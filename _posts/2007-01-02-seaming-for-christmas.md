---
title: 'Seam&#8217;ing for Christmas'
author: ajordens
layout: post
permalink: /2007/01/seaming-for-christmas/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
I had a few days off from work over the holidays and decided to do a bit of an investigation into Gavin King&#8217;s new web framework, Seam.

My recent background has predominantly been in the J2EE space (Spring + Hibernate 3.0/3.2) but fronted with a thick Swing application as opposed to the typical web application. I&#8217;ve played with Ruby on Rails in the recent past and have built a number of Struts-based applications in years passed.

I didn&#8217;t particularly get very deep into the framework in the couple days I spent with it but I did leave with a favourable opinion. If nothing else it strikes as one of the better structured and maintainable application frameworks. I did this initial development stint in IntelliJ IDEA which as far as I could tell didn&#8217;t have much support for Seam (as opposed to Eclipse?). I found Seam&#8217;s Rails-like generators to be a useful starting point but the generated code didn&#8217;t necessarily mesh with what the documentation and tutorials covered. I generated the first few artifacts but quickly fell back to manual generation once I got the hang of the expected layout and structure.

The notions of conversations are interesting and something I&#8217;ll be considering in my day-to-day development. I&#8217;m particularly interested in the caching implications. I&#8217;ve found it difficult to consistently cache data model entities and ensure that they remain up to date across the network. With a conversationally scoped cache you would get some benefits of caching (in our application you may make multiple requests for the same data over the course of a conversation) without having to worry \_as much\_ about overall consistently. Of course it&#8217;s still a concern but your scope is ultimately limited to a shorter time frame.

A Seam-based application is particularly easy to refactor. Unique identifiers are assigned to application artifacts (session beans, entities, etc.) using the @Name annotation. These identifiers act as the point of reference rather than a physical object on the classpath so you&#8217;re free to refactor without a need to update XML files or other such references. A refreshing change from something like Struts.

That&#8217;s it for now. Work has started up and early indications are that 2007 should be an interesting year. Hopefully I&#8217;ll get back to Seam when things calm down a bit.