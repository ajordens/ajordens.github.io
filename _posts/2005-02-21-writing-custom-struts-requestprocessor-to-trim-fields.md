---
title: Writing custom Struts RequestProcessor to trim fields
author: ajordens
layout: post
permalink: /2005/02/writing-custom-struts-requestprocessor-to-trim-fields/
categories:
  - Java
---
One of the web applications I maintain had a need to have fields trimmed. I had previously just relied on validation to return an invalid field if it had  
been left in an untrimmed state by the end user. Not necessarily the most ideal situation so I looked for a way to automatically trim fields requiring as  
little code as possible (hey, i&#8217;m putting this together in the middle of the night).

Haven&#8217;t done too much with custom request processors but they looked like the best choice.

So i started out writing a request processor with an implementation for processActionForward. It didn&#8217;t work as expected so I tried implementing a differe  
nt method. A short while later I had a custom RequestProcessor with an implementation for processPopulate. The jist of the implementation was the functio  
n would loop through the parameters in the http request object, manipulate the string arrays, trim the desired value and put it back in the request. It a  
ctually worked like a charm and was easily implemented once I figured out the nuances of the request processor.