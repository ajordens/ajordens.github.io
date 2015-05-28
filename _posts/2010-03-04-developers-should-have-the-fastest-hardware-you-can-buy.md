---
title: Developers should have the fastest hardware you can buy
author: ajordens
layout: post
permalink: /2010/03/developers-should-have-the-fastest-hardware-you-can-buy/
categories:
  - General Discussions
tags:
  - hardware
---
I was fortunate enough to recently have my 3 year old MacBook Pro retired from service. A new and *much faster* one has appeared in its place.

**Old Laptop** (*2.333ghz, 5400rpm HD, 3GB DDR2*)

*mvn clean install &#8211;* 8-10 minutes depending on system load

*mvn clean install -DskipTests &#8211;* 4-5 minutes depending on system load

*JBoss startup &#8211;* 70-90 seconds depending on system load

*IntelliJ Responsiveness* &#8211; Slow

**  
**

**New Laptop** (*2.8ghz, 128GB SSD, 4GB DDR3*)

*mvn clean install &#8211;* 3 &#8211; 4 minutes

*mvn clean install -DskipTests &#8211;* 70 seconds

*JBoss startup &#8211;* 32 seconds

*IntelliJ Responsiveness* &#8211; Blazing Fast

Night and day difference. I haven&#8217;t counted yet, but on average, I would anticipate doing probably between 8 and 12 build + deploys a day. A realistic estimate would put my daily build time savings around **30 minutes**. And that&#8217;s discounting the morale and efficiency boost coming from not having to context switch every time the machine bogs down because something is running in the background.

I&#8217;m a developer and speed geek. I&#8217;m that guy who grew up with the 300A Celeron overclocked to 450mhz. I&#8217;m greatly annoyed with inefficiencies and constantly find myself tweaking aliases, just to get that 5 step build process down to one.

**  
**

**Fuzzy Math**

Assuming a pie in the sky daily wage of **$300** (*to make the numbers easier*), a **30 minute savings per day** equates to **$18.75**. Multiply that by **250 days** worked in a typical year (*2000 hrs*) and you&#8217;re looking at a theoretical productivity gain of over **$4500**.

I would argue that regardless of how efficient you think your programmers are today, you will **always <span style="font-weight: normal;">see positive benefits from ensuring they always have access to decent hardware and build environments.</span>**

Now take this new laptop. It cost under **$3000** (*apple premium*). If laptops aren&#8217;t your thing, a desktop can be had probably half.

If you cannot justify spending $3000 per developer every 1.5years, at least consider upgrading core components. I don&#8217;t have numbers, but I&#8217;m guessing that a significant portion of the improvements I&#8217;m seeing were a result of the SSD.

Either way, if you value the time of your programmers, I don&#8217;t see how you can lose.

*Time is money, and efficient programmers == happy programmers.*