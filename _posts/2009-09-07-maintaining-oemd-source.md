---
title: Maintaining OEM’d Source
author: ajordens
layout: post
permalink: /2009/09/maintaining-oemd-source/
categories:
  - General Discussions
  - Java
---
**Background**

The company I work for made the decision to OEM a product from a partner, rather than invest valuable development time to build something that has essentially been commoditized.

Development resources are at a premium and we consciously don’t want to spend any more time on this code base than we have to, we’re **much better** at adding value in other areas.

&#160;

Not necessarily a bad or the wrong decision, we’ve just reached the point in time where we need to make functional changes to the OEM’d code base.&#160; 

&#160;

**Due Diligence**

Obviously, before you entertain the outright purchase or license of a third party product/code base, there’s a few questions you ought to ask yourself:

*&#8211; Is the technology stack compatible with our existing products?&#160; *(A member of the development staff should provide the answer)

&#8211;* Does the product do significantly less/more than we will ever need it to? *(The later is an important question, do you really want to maintain features that customers will never use? What’s the cost of re-implementing just the features the customer does need?)

&#8211; *What’s the support model look like? *(Who is fixing bugs, you or the source company? How are patches exchanged, or are they?)

&#160;

**Maintenance**

During the course of our due diligence, we did send a couple developers on site to become familiar with not only the code base but in particular the build process around it.

This did pay dividends as we were able to setup Bamboo builds capable of automatically creating installation packages and running unit tests.

*Significant win in my books*.&#160; Test coverage may not be the greatest, but if you can build a complete candidate release in 7 minutes, manual testing/verification remains a possibility.

&#160;

That’s it for now.&#160; 

I’ll admit that I was a skeptic when the idea of adopting a 3rd party code base was first brought up.&#160; Fortunately the changes we’ve been required to make thus far have been minor.&#160; Technology stack is slightly different and anecdotally bug fixes seem to be taking ~3x longer then they would on our primary product, I expect that ratio to more or less even out as we familiarize ourselves with the patterns and structure in the new code base.&#160; 

The verdict&#8217;s still out on whether or not we’ll be able to add any new components of significant functionality while keeping things at all maintainable.

But of course that’s the challenge inherent with any software development activity!