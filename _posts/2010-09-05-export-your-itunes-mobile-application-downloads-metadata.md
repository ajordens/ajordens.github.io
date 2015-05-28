---
title: Export the metadata for your downloaded iTunes mobile applications
author: ajordens
layout: post
permalink: /2010/09/export-your-itunes-mobile-application-downloads-metadata/
categories:
  - General Discussions
---
Put together a bit of Groovy code that will traverse your iTunes Mobile Applications directory and extract the metadata for each download. The aggregated metadata is exported to a csv.

Lots of interesting stuff in there. Looks like I currently have 60 applications downloaded (*I tend to delete apps from iTunes that I&#8217;m not interested in*) and have spent about $60. Most of the applications are free with a few larger ticket iPad application purchases.

The code has been posted to <a target=_new href="http://gist.github.com/566344">gist</a>. 

Unfortunately it does need to be run on an OS X machine right now in order to get around some conversion issues between binary and text metadata formats. That may change at some point.