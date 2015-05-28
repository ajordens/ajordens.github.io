---
title: Porting a Swing App from Java5 to Java6
author: ajordens
layout: post
permalink: /2008/05/porting-a-swing-app-from-java5-to-java6/
categories:
  - General Discussions
  - Java
---
We&#8217;ve got a fairly significant Swing application that we couldn&#8217;t port to <span style="font-style: italic;">Java6</span> until Apple released a compatible JVM. Fortunately that <span style="font-weight: bold; font-style: italic;">finally</span> happened last week.

I&#8217;m down at JavaOne this week and was motivated to take a stab at resolving the couple dozen compilation problems and get things running.

It really wasn&#8217;t too difficult. The most annoying changes I had to deal with concerned our usage of old versions of the SwingWorker and JDIC classes. They have now been integrated into the platform with slightly different interfaces and aren&#8217;t source-level compatible with their predecessors.

I took a stab at swapping in a couple of new L&Fs, mainly Nimbus and Substance. As far as Nimbus goes, the build I grab&#8217;d from SwingLabs seemed to have a couple of problems dealing with custom UIs (a NPE attempting to replace the default SplitPaneUII). I didn&#8217;t see a build of the Java6 Update N available for the Mac so I couldn&#8217;t check to see if the problems I was seeing have been fixed. The new button UIs are definitely an improvement but I&#8217;m not quite sure how I feel about the scroll bars.

Substance was more or less a drop-in replacement that worked out of the box. The only problems I had was when I tried to apply particular themes or skins. Depending on

> UIManager.setLookAndFeel(new SubstanceBusinessLookAndFeel()); **BAD**
> 
> **<span style="font-weight: normal;">SubstanceLookAndFeel.setSkin(new MistSilverSkin());</span> GOOD**
> 
> **<span style="font-weight: normal;">UIManager.setLookAndFeel(new SubstanceLookAndFeel());</span> **

The former resulted in ClassCastExceptions between an internal Apple Aqua panel and a Substance panel. I suspect it just hasn&#8217;t been tested extensively with the Apple JVM.