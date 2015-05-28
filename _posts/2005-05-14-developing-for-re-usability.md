---
title: Developing for re-usability
author: ajordens
layout: post
permalink: /2005/05/developing-for-re-usability/
categories:
  - Java
---
Lately we&#8217;ve been re-using a few legacy components in other applications and its forced me to think a little bit about developing for re-usability.

Here are a few off the cuff thoughts on re-usable component development

1) Adequately comment all public/protected (and ideally private) methods.  
&#8211; By adequate I mean full javadoc including expected parameter value ranges, is null?, etc. If a method throws an exception (checked or unchecked), includ  
e that in the documentation.  
&#8211; If appropriate, consider external non-code documentation for the component.

2) Provide controlled accessors to variables instead of direct access.  
&#8211; Avoid allowing people to do componentInstance.variable = null. It&#8217;s just good coding habits.

3) A failure in the component should not bring down the calling application.  
&#8211; No one would actually consider doing this right? but a System.exit() inside a method is just plain terrible and unacceptable.  
&#8211; Exception conditions should be handled appropriate and resources/connections closed. 

4) Adequate (but not excessive) logging  
&#8211; Make proper use of the different logging levels.  
&#8211; Don&#8217;t hardcode log4j usage and create an unwanted dependency in calling applications.  
&#8211; Don&#8217;t log stack traces and then proceed to re-throw the exception: ie)

catch (IOException e)  
{  
// this logger is worthless and may cause unnecessary console prints  
// in the calling application.  
logger.error(&#8220;Error accessing file: &#8221; + file, e);  
throw new CustomException(&#8220;Error accessing file: &#8221; + file, e);  
}

5) Unit-test  
&#8211; A unit-test should help self-document and code review the component. The unit test should cover all boundary conditions on variables and alert the devel  
oper if they missed something.  
&#8211; A unit-test will act as a form of documentation showing expected uses and results.  
&#8211; A test will serve as a foundation point that other developers can build upon as they integrate. There&#8217;s nothing worse than wanting to use a component bu  
t not being sure if it actually works correctly and having to test it yourself.

6) Interface development **(updated)**  
&#8211; Start with the development/specification of an interface between your code and the outside world.  
&#8211; When it comes time to implement your component, program to the interface.  
&#8211; Avoid directly calling/loading of implementing classes, consider the use of Factories or alternatively DI frameworks like Spring.

I&#8217;ve got to run now so that&#8217;s all for now.