---
title: When Good is Enough (and when it isn’t)
author: ajordens
layout: post
permalink: /2009/12/when-good-is-enough-and-when-it-isnt/
categories:
  - General Discussions
---
It’s a constant debate that we fight on a daily basis, is the work we’ve completed good enough, or is important enough to spend an extra half day or day(s) perfecting.

Often times we’re forced to make sacrifices, but when is it the right time to push back or accept defeat?

Obviously what follows here are my own opinions but I’m a firm believer that a well executed plan only 80% complete, is worth leaps and bounds more than a flawed plan 100% complete. 

&#160;

A few questions I commonly ask myself:

  * *<u>Is what I’m working on tied to a software release</u>.&#160; *We release on a month basis in two 2 week iterations.&#160; I know that if I want to make it into a release, I need to have it done sufficiently ahead of time in order to ensure adequate testing.&#160; **This may mean cutting scope.&#160; **Cutting scope is fine IMO, just do so in a way that you avoid silly shortcuts that create headaches for yourself when you inevitably have to come back and add functionality. 
  * *<u>Who is the consumer</u>*. Is it a paying customer (*ie. they have already paid)*? Is it for a demo? Is it for another developer? If its a customer, what are they actually trying to accomplish? Often times, we get caught up in our own expectations of how something should look or behave, and lose sight of what the customer is actually trying to do.&#160; If the customer is currently using pen & paper to track something, a simple (*ugly?) *web form may be perfectly acceptable. **Don’t overcomplify. **With good feedback, you can always come back and do a better job. Focus on the present, don’t get distracted on what you **\*might\*** need to do in the future. 
  * *<u>How often is the functionality used</u>. *If the feature or function being worked on is used by a handful of backend administrators, you may not need to go over the top on day one.&#160; If they come back and tell you that they absolutely cannot use the system without A, B or C.&#160; Make sure you understand what A, B and C are and get cracking.&#160; **Quick turnaround built loyalty and trust.&#160; You need both as early in the customer relationship as possible.&#160; **If the feature is public facing and used by a large percentage of the audience, by all means, perfect it. 
  * *<u>Do I need to modify the database</u>*. From a technical perspective, this has always been a killer.&#160; Make a flub manipulating the database, and you’ll cause yourself countless hours of time trying to correct customer datasets. **Get representational datasets, migrate them automatically and test test test!**&#160; Speaking from experience, do not cut corners testing or working with your database migrations. 
  * *<u>Have I been burnt in this area before</u>*. Maybe the work you’re doing is in direct response to a filed bug.&#160; Either way, if you’re working a particularly risky area of the codebase, it’s worth going that extra step to ensure you’ve got solid code coverage (*unit, regression, selenium tests, etc.*).&#160; **Fool me once… Fool me twice…** 

&#160;

There are plenty more, but in general, I err on the side of trying to get releases out the door.&#160; If we spend 20 calendar days in a release (4 work weeks), **up to 6** of those will be spent either performing non-automated regression tests (*don’t worry, we have automated tests as well*) or fixing post code-complete deficiencies.&#160; 

Test cases are a given.&#160; If you’re working Java or any other programming language with tooling like JUnit or TestNG, I really see no excuse not to use it.&#160; If nothing else, it’s a good safety net if you ever need to refactor a particular area of the code base.&#160; 

&#160;

If I had to pick a guiding principle, it would be:&#160; ***Get it in, Make it right, Make it fast.***&#160; 

******

***Get it in **because you need the feedback.*

***Make it right **because that’s what we’re paid to do and stakeholders expect it.*

***Make it fast **because it’s no fun staying up until 2:00am trying to debug performance problems on a customers live system.*