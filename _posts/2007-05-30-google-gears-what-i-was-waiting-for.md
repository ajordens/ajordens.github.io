---
title: 'Google Gears: What I was waiting for'
author: ajordens
layout: post
permalink: /2007/05/google-gears-what-i-was-waiting-for/
categories:
  - General Discussions
---
Awhile back I blogged about how nice it would be to have offline support built into Google Reader. At the time, I anticipated some form of integration with Google Desktop.

Fortunately, the folk at Google smiled down on me (and many others) today and provided the functionality in part to show off their new [Gears][1] framework. Basically, developers can use Google Gears to easily build offline support into their web applications. Sure there are existing ways to do this, but being from Google, Gears is sure to get a lot of traction.

The Google Gears framework is consists of a smallish (700K) browser plugin for IE and FireFox. Client applications (including but not limited to Google Reader) communicate with it using a series of new APIs accessible via JavaScript.

The impact on Google Reader is quite good IMO. Beyond the obvious benefit of being able to read offline, the fact that you&#8217;re limited to 2000 recent posts provides a reasonably diverse selection of content making it easier to stay up to date across many feeds instead of just the popular ones.

For those interested parties, SQLite is used as the backing datastore. There&#8217;s also an API for a ThreadPool-like (or WorkerPool as Google calls it) structure allowing you to easily manage long running tasks.

The extension is available under the non-viral BSD license. [Ajaxian.com][2] has a couple of related stories including an interview with Brad Neuberg of the Dojo framework.

Pretty cool.

 [1]: http://gears.google.com/
 [2]: http://www.ajaxian.com