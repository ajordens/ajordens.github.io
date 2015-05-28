---
title: 'Building Better Software: It starts with a philosophy.'
author: ajordens
layout: post
permalink: /2012/12/building-better-software-it-starts-with-a-philosophy/
bfa_virtual_template:
  - hierarchy
categories:
  - General Discussions
---
<div class="ennote" style="word-wrap: break-word; -webkit-nbsp-mode: space; -webkit-line-break: after-white-space;">
  <div style="font-family: Arial;">
    <span style="font-size: 14px; font-family: Arial;"><span style="font-family: Arial;"><!--?xml version="1.0" encoding="UTF-8" standalone="no"?-->

    <span style="font-size: 14px;">The process through which software is built and shipped varies widely between companies, and even teams within any one company.</span></span></span>
  </div>

  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>

  <div style="font-family: Arial;">
    <span style="font-size: 14px;">As a student of software leadership and an active participant on many development teams, I&#8217;m going to share a few thoughts on how I believe we can collectively build better software.  </span>
  </div>

  <div style="font-family: Arial;">
    <div>
      <span style="font-size: 14px;"><br /></span>
    </div>

    <div>
      <span style="font-size: 14px;">Follow me on Twitter: <a href="http://twitter.com/ajordens">@ajordens</a></span>
    </div>

    <div>
       
    </div>

    <div>
      <span style="font-size: 14px;"> </span>
    </div>

    <div>
      <span style="font-size: 14px;"><strong>Small Teams, Individual Ownership.</strong></span>
    </div>

    <div>
      <span style="font-size: 14px;"><strong><br /></strong></span>
    </div>

    <div>
      <span style="font-size: 14px;">In my opinion, teams <em>should be</em> no bigger than 5 people and they <strong>must be</strong> capable of owning what is built from inception to production.  </span>
    </div>

    <div>
      <span style="font-size: 14px;"> </span>
    </div>

    <div>
      <span style="font-size: 14px;">Scalability comes from a focus on not repeating yourself and building tools to abstract away grunt work. Want an architecture like Netflix? You must iterate relentlessly and never settle on <em><strong>good enough</strong></em>.</span>
    </div>

    <div>
      <span style="font-size: 14px;"> </span>
    </div>

    <div>
      <span style="font-size: 14px;"><span style="font-family: Arial;">We must focus on getting good at going from an initial idea or concept to implementation. </span>Speed and efficiency come from reusing common patterns and techniques (<em>and technologies</em>), not reinventing the wheel.  </span>
    </div>

    <div>
      <span style="font-size: 14px;"> </span>
    </div>

    <div>
      <span style="font-size: 14px;">Case in point, here&#8217;s my (<em>current</em>) set of preferred frameworks and tools:  </span>
    </div>

    <div>
      <ul>
        <li>
          <span style="font-size: 14px;">Dropwizard (<em>for simple RESTful APIs</em>)</span>
        </li>
        <li>
          <span style="font-size: 14px;">AngularJS (<em>for client-side JS</em>)</span>
        </li>
        <li>
          <span style="font-size: 14px;">Compass/SASS (<em>for client-side CSS management</em>)</span>
        </li>
        <li>
          <span style="font-size: 14px;">Fabric (<em>for programmatic deployment</em>)</span>
        </li>
        <li>
          <span style="font-size: 14px;">AWS (<em>for relational and non-relational data stores, etc.</em>)</span>
        </li>
      </ul>
    </div>

    <div>
      <span style="font-size: 14px;">Just as every carpenter carriers a hammer, every developer must aim to master a set of tools and ever-changing frameworks.  <strong>What are yours?</strong></span>
    </div>

    <div>
      <span style="font-size: 14px;"> </span>
    </div>

    <div>
      <span style="font-size: 14px;"><strong><br /></strong></span>
    </div>

    <div>
      <span style="font-size: 14px;"><strong>Be Goal</strong> <strong>Oriented, not Task Focused.</strong></span>
    </div>

    <div>
      <span style="font-size: 14px;"> </span>
    </div>

    <div>
      <span style="font-size: 14px;">Just because you broke an idea, goal or user story down into a series of tasks does not mean that you&#8217;ve captured the essence of what needs to be delivered.  </span>
    </div>

    <div>
      <span style="font-size: 14px;"> </span>
    </div>

    <div>
      <span style="font-size: 14px;">All too often it&#8217;s easy to get lost in the details of crossing items off an implementation checklist and losing site of the fact that what is being built is a piece of <em>crap</em>.  Focus on the customer and if the original breakdown is not aligned with your actual progress, adjust accordingly and talk with your team or stakeholders.</span>
    </div>

    <div>
      <span style="font-size: 14px;"> </span>
    </div>

    <div>
      <span style="font-size: 14px;">Personal rule of thumb, <strong>never go longer than a day</strong> without committing code and getting feedback from a peer, even if it&#8217;s just bouncing your progress off them for a quick sanity check.  Always talk about what has  already been done before discussing what will be tackled next.  </span>
    </div>

    <div>
      <span style="font-size: 14px;"> </span>
    </div>

    <div>
      <span style="font-size: 14px;">A tool like JIRA, used incorrectly and without oversight, can make it easy to head off in the wrong direction.  Put another way, JIRA will let you create all the sub-tasks and record as much time as you&#8217;d like against them, but it will never tell you you&#8217;re doing the right, or wrong, thing.  </span>
    </div>

    <div>
      <div style="font-family: Arial;">
        <span style="font-size: 14px;"> </span>
      </div>

      <div style="font-family: Arial;">
        <span style="font-size: 14px;"> </span>
      </div>

      <div style="font-family: Arial;">
        <span style="font-size: 14px;"><strong>You don&#8217;t always get what you want.</strong></span>
      </div>

      <div style="font-family: Arial;">
        <span style="font-size: 14px;"><strong><br /></strong></span>
      </div>

      <div style="font-family: Arial;">
        <div>
          <span style="font-size: 14px;">As engineers, it can be rare to find an environment that day in and day out is going to push you to improve. I feel that we owe it to ourselves to find outlets outside of the office that offer rewarding technical challenges, be it taking Martin Odersky&#8217;s Scala course or working on a side-project.  </span>
        </div>

        <div>
          <span style="font-size: 14px;"> </span>
        </div>

        <div>
          <span style="font-size: 14px;">On a personal note, I <em>self-funded*</em> my own 20% time last year and invested in personal experimentation. Learning to quickly take ideas from concept to implementation, and getting knee deep in Python, MongoDB, the App Store and much much more along the way.  </span>
        </div>

        <div>
          <span style="font-size: 14px;"> </span>
        </div>

        <div>
          <span style="font-size: 14px;">Looking back, this was probably one of the best decisions I could have made.  </span>
        </div>

        <div>
          <span style="font-size: 14px;"> </span>
        </div>

        <div>
          <span style="font-size: 14px;">* <em>self-funded, in this case, meant taking an unpaid day off each week for a year from my regular job to focus on personal projects.</em></span>
        </div>

        <div>
          <span style="font-size: 14px;"><em><br /></em></span>
        </div>
      </div>
    </div>
  </div>

  <div style="font-family: Arial;">
    <span style="font-size: 14px; font-family: Arial;"><em><br /></em></span>
  </div>

  <div style="font-family: Arial;">
    <span style="font-size: 14px; font-family: Arial;">That&#8217;s it for now.  Stay tuned!</span>
  </div>
</div>
