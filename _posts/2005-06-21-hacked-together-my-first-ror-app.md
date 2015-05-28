---
title: Hacked together my first RoR App
author: ajordens
layout: post
permalink: /2005/06/hacked-together-my-first-ror-app/
categories:
  - General Discussions
  - Open Source Software
---
Well tonight I finished hacking together my first attempt at a Ruby on Rails-based application.

Basically what I built was a clone of the *wars (ala [kittenwars][1]) site where you put images head to head and allow the viewer to vote. Not to be shy about ripping off ideas, I also borrowed the CC-licenced theme for wordpress.

It&#8217;s called FlickrWars! and the twist is that it uses Flickr as the image store allowing me to change the photosets/tags/user photos on the fly. Could be interesting if it ever goes live but it is really just a simple proof of concept.

What it supports:  
&#8211; voting  
&#8211; viewing of last X photos  
&#8211; list of top ranked photos  
&#8211; list of bottom ranked photos  
&#8211; most viewed photos

Images are currently randomly placed against each other. Could easily just grab photos from a particular tag. Already thinking about a tag interface where the user could add tags to the system and a new tag would be chosen every X minutes.

All in all the project satisfied my short-term goal of building something with RoR and briefly touching the Flickr API. I didn&#8217;t really have much exposure to Ruby previously but I&#8217;ll be digging into it more moving forward. 

I&#8217;ll attach a couple of screenshots to this post. The code is pretty rough and I&#8217;ll be cleaning it up over the next few days. Perhaps when its a little more polished I&#8217;ll find somewhere to put it online.

[<img src="http://photos15.flickr.com/20855342_e8a9c98ee9_m.jpg" width="240" height="150" alt="FlickrWars01" />][2]

[<img src="http://photos17.flickr.com/20855353_469f2d10c3_m.jpg" width="240" height="150" alt="FlickrWars02" />][3]

 [1]: http://www.kittenwars.com/
 [2]: http://www.flickr.com/photos/adamjordens/20855342/ "Photo Sharing"
 [3]: http://www.flickr.com/photos/adamjordens/20855353/ "Photo Sharing"