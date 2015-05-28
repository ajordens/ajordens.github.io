---
title: 'DoS&#8217;ing Virus Scanners : Can it be done?'
author: ajordens
layout: post
permalink: /2007/05/dosing-virus-scanners-can-it-be-done/
categories:
  - citations
---
A bit of curiosity here.

The amount of time to run a virus scan on my work laptop is now approaching 8 or 9 hours. It&#8217;s reached the point where there really is no convenient time of day to have it run. Our system administrator currently has them running automatically at 4:00am, but when I&#8217;m up and out the door at 7:00am it&#8217;s usually only scanned 700k of the estimated 2million files.

Sounds like a bit of an opportunity to game the virus scanner. A couple of possibilities off the top of my head:

  1. I don&#8217;t know the logistics involved with scanning a single file or if the amount of time varies upon it&#8217;s makeup. Taking a brute force attack, the deployed virus could create a couple million files strategically placed to increase the scan time to the point where people start canceling scans early.
  2. Write something that artificially increases system load and therefore system scan time. It should be possible to make such an app smart enough to only run when it&#8217;s detected increased load from the virus scanning process.

Rather simplistic but who knows? If nothing else, with ever increasing hard drive sizes, we&#8217;ll need some better heuristics to prevent linear increases in scan times.