---
title: 'DeveloperForce.com : Initial Thoughts and Experiences using the Platform'
author: ajordens
layout: post
permalink: /2009/07/developerforce-com-initial-thoughts-and-experiences-using-the-platform/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
The team and I have recently kicked off a rather ambitious [project][1].&#160; In an attempt to help accelerate the early development activities, we’ve made a decision to build a series of one-off implementations using the *DeveloperForce.com* platform (*salesforce.com sans the sales CRM portions*).

The objective is to learn enough about the platform during these initial largely custom implementations, to be in a position to hopefully create and deliver a largely standalone solutions faster than we would using the typical Java technology stack.

The jury is still out, but what follows are some initial thoughts after working with the platform.&#160; The team in question are a group of 3 senior developers working collectively on an application deployed in a single Salesforce Organization.&#160; **

*Forgive my use or miss-use of Salesforce/DeveloperForce terminology.&#160; **It can get confusing at times <img src="http://littlesquare.com/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />*

****

**Version Control**

Like any good development shop, we store all code and build artifacts in source control.&#160; Subversion is our poison of choice.

Salesforce development is a bit different in that a lot of the configuration and development activities can occur in either the browser or their Eclipse-based IDE.&#160; 

Our strategy for getting code and configurations under source control was to use Eclipse and regularly sync with our development organizations (*Salesforce jargon for a development space or area*).&#160; 

Unbeknownst to us at the onset, there are certain configurations you can make using the browser that are not possible to make with the IDE.&#160; It’s important that these configurations (*user/queue creation, etc.*) are documented externally (*ie. in a spreadsheet*).

Code and configurations are moved between developers using Subversion and the Eclipse synchronization capabilities (or the Salesforce migration tool).&#160; By storing these artifacts in Subversion, we’re also able to do code reviews on them via Crucible.

Your mileage may vary with this approach, as we found the current Salesforce tooling to be quite poor at conflict resolution when it came to structural changes.&#160; Moreover, we frequently had to fall back to manually making changes via the web browser.&#160; ****

**Very annoying**.&#160; 

I think it’s safe to assume that despite all the redeeming qualities of the DeveloperForce platform, some significant gaps remain when it comes to the expectations of traditional software developers.&#160; By traditional, I mean those of us that are used to using source control, doing code reviews, etc.&#160; **I guess Salesforce considers us a dying breed <img src="http://littlesquare.com/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />**

&#160;

Would I choose the platform to build a product I expected to maintain in the long-term and derive significant value from? **No**.&#160; 

Would I use it in the short-term as a RAD environment to build a prototype? **Possibly**, but not without first considering some of the more traditional alternatives (*there are a number of schema-less data storage products available these days, combine that with a Grails, Seam, Rails or Django and you may very well be off to the races*).

&#160;

That’s enough for one night.&#160; I plan on doing a follow-up once the team has more experience maintaining and migrating code after it’s been deployed to DeveloperForce.

 [1]: http://www.genologics.com/translational-research