---
title: 'Hack Day Mashup : Salesforce + Google Maps'
author: ajordens
layout: post
permalink: /2007/03/hack-day-mashup-salesforce-google-maps/
categories:
  - General Discussions
---
I know it&rsquo;s been done multiple times previously but I&nbsp;decided to play around with Google Maps a bit more.

My initial goal was to interface with our companies data in Salesforce and plot it accordingly using the Google Maps API.&nbsp; We have all sorts of conditions and variables attached to our data so it would (and did) make an interesting map.

**Problem: **It quickly became apparent that our salesforce account&nbsp;didn&rsquo;t [support][1] API access.&nbsp; Evidently it cost more money.&nbsp; That being said, Salesforce does have a great API and developer community but without access to it, you&rsquo;re pretty much S.O.L.&nbsp; 

**Solution: **Even without programmatic access, I discoved that you can still create reports and export results to CSV.&nbsp; Nothing exciting but it did prove to be the easiest and most efficient way to get data out.

Once I had report data, I wrote a massager in python that took a CSV file, stripped out the useless information, and used Yahoo&rsquo;s public geocoding service to translate addresses into appropriate latitude and longitude values.

The original plan was to build a django-based front end around it but that was scrapped in the interest of time.&nbsp; Instead I used a bit of php thrown together from various sources.

In the end it turned out to be a fairly straightforward (but interesting nonetheless) hack.&nbsp; I used a couple hours at the end of day to implement basic filtering capabilities.&nbsp; The data being displayed concerned sales territories, current and potential accounts as well as probability that any given account would convert.&nbsp; Different aspects were colour-coded and labeled.

At the end of the day I was quite happy with what I managed to produce.&nbsp; The Google Maps API is quite trivial to work with, the challenging part was finding worthwhile data to chart.&nbsp; 

I&rsquo;ll take some screenshots and post shortly.

 [1]: http://helpdesk.codingrobots.com/