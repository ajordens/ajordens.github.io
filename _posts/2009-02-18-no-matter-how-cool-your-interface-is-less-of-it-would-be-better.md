---
title: '&#8220;No matter how cool your interface is, less of it would be better.&#8221;'
author: ajordens
layout: post
permalink: /2009/02/no-matter-how-cool-your-interface-is-less-of-it-would-be-better/
categories:
  - General Discussions
  - Java
---
Interesting little [article][1] over on InfoQ talking about *Alan Cooper*’s book **About Face**.

&#160;

Few key points:

  * Design for Intermediates Users
  * Use Tools that Help Beginners to Become Intermediates
  * Less is More
  * Design for the Probable, Provide for the Possible
  * Eliminate Errors or Confirmation Dialogs

&#160;

There’s an interesting closing comment discussing the need (*or lack there of*) for error or confirmation dialogs.&#160; 

> “Cooper notes that while they [error dialogs] are used to signal that something went wrong with the code, the user tends to interpret them as “I’ve done something wrong.”&#160; When users are told that they are wrong repeatedly, they start to hate your product”

<font face="Trebuchet MS" color="#888888"></font>I suspect there’s some truth behind the statement, however all things being equal, if your product is blowing up, there’s a good chance that users aren’t going to be happy campers anyways.

That being said, I agree that showing an error dialog with some cryptic exception message only decipherable by the originating author, is probably not doing anyone a favor.&#160;&#160; 

Using the Java IDE IntelliJ as an example, it’s quite rare for a user to get an actual error dialog.&#160; Instead, there’s a little status icon in the corner that will blink red whenever there’s a problem.&#160; Clicking it will provide additional details with the option of submitting it back as a bug report.&#160; 

It’s important to remember who the user is, and considering the article’s focus on differentiating between beginner, intermediate and expert users, this **status icon** approach is probably best suited for intermediate/expert users, and not beginners.&#160;

 [1]: http://www.infoq.com/articles/UI-Principles-Naysawn-Naderi