---
title: Code Ownership vs. Technical Debt
author: ajordens
layout: post
permalink: /2013/04/code-ownership-vs-technical-debt/
categories:
  - General Discussions
---
<!--?xml version="1.0" encoding="UTF-8" standalone="no"?-->

<span ><span style="">Lately I&#8217;ve been thinking about technical debt and how it&#8217;s accumulated over the course of a company. </span></span>

<span ><span style="">Thinking back upon many a software project, it&#8217;s becoming clear that a lack of decisive ownership can be a </span><span style="">significant</span><span style=""> contributor to technical debt and frustration amongst teams. </span></span>

<span style=" ">Ownership goes far beyond just writing a design doc, or doing the odd code review. It&#8217;s holding oneself accountable for everything that happens within a codebase, from now until such time that it&#8217;s been handed off to someone else (</span><em style=" ">who equally understands the role and responsibilities</em><span style=" ">). </span>

<span style=" ">You&#8217;re expected to work with contributors, maintain the quality bar, resist unnecessary complexity or features (</span><em style=" ">the inevitable &#8220;we don&#8217;t know where else to put this feature, lets put it in this artifact&#8221;</em><span style=" ">), and otherwise keep things moving forward. There&#8217;s nothing to say that ownership can be spread across a team, </span><strong style=" ">but</strong><span style=" "> </span><strong style=" ">everyone needs to be on the same page</strong><span style=" ">. </span>

<span style="">If what I&#8217;ve described sounds </span><span style="">like</span><span style=""> an open-source project, that&#8217;s by intention. I think there&#8217;s a lot that can be borrowed from successful open-source projects and applied within corporate environments. </span>

<span style="">Over time, codebases without ownership have a tendency to be labeled as &#8220;legacy&#8221;. In the open-source world, they would likely be abandoned but in corporate america, they almost always live on. </span><span style="">The valiant few will jump right in and try to affect change within, but more often than not, these efforts merely chip away at the surface leaving systemic issues below. To the business, this is working and (</span><em style="">hopefully</em><span style="">) revenue generating code. For most teams, there is </span><span style="">little</span><span style=""> patience or motivation for maintenance when far more exciting nuts to crack are looming on the horizon. Unfortunately, there is almost always something more important than investing in your existing code.</span>

<span style="">Every so often, things get bad enough that</span><span style=""> an organization might attempt wide-scale refactoring or perhaps even small (or large)-scale rewrites. </span>

<span style=" ">A cautionary tale. If you&#8217;re going to refactor your codebase, don&#8217;t just shuffle bits around. Refactor it such that you can </span><strong style=" ">assign ownership amongst pieces with very clear delineation</strong><span style=" ">. </span>
