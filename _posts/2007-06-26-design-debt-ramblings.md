---
title: 'Design Debt: Ramblings'
author: ajordens
layout: post
permalink: /2007/06/design-debt-ramblings/
categories:
  - citations
---
Just reading Chris Sterlings recent post titled [*Clean Up, Clean Up, Everybody, Do Your Share*][1]* *and the following snippet on design debt caught my eye.

*Have you ever been part of a legacy project where it seemed almost impossible to add the feature asked for because you weren’t sure what will break once it is added?*

> A resounding yes and it&#8217;s a tricky situation to work your way out of. You&#8217;re often without any substantial unit or regression tests and are left fighting an up-hill battle on two fronts. On one hand, you&#8217;re trying to devise a design that&#8217;s going to have the least impact on pre-existing code (*perhaps through a facade if you have enough knowledge about expected behaviour to be able to pull a suitable abstraction*) while on the other your level of frustration has reached the point of wanting to go down the rabbit hole of gutting and *re-writing* (emphasis on re-writing and not refactoring) components. It&#8217;s situational about which approach is the right one to take but there&#8217;s a definite time and place for fairly serious refactorings. You can only cart around technical and design debt for so long.

*This does not mean that we no longer conduct design sessions to determine a design direction for implementing a feature but these sessions should produce just sufficient enough design to get started. Also, as a team we should decide if an artifact needs to be captured from our design session.*

> The context for this note is around the need to hold design sessions/reviews even when working in an environment that encourages continous refactorings. On a similar vain you don&#8217;t want the very notion of a design session or review to forbid or discourage refactorings during the course of an implementation. I strongly agree that design sessions are means to influence a direction, not dictate one. If as an implementor you come across a snag in your initial design, please don&#8217;t leave it and use the excuse of &#8216;*oh it was in the original design and it was approved*&#8216; when someone calls you on it. That excuse worked in University but certainly doesn&#8217;t fly in any environment I&#8217;ve seen.

Chris talks in more detail about various forms of [accumlated debt][1] and some strategies for dealing with it in agile environments, I just picked out the pieces that particularly struck home.

So, there you have it. Dealing with legacy components is often difficult but necessary, design at an appropriate level of abstraction to influence (*and not dictate*) direction and lastly&#8230; don&#8217;t make excuses <img src="http://littlesquare.com/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

 [1]: http://chrissterling.gettingagile.com/2007/04/08/clean-up-clean-up-everybody-do-your-share/