---
title: 'Good Advice &#8211; Don&#8217;t let performance overly influence design'
author: ajordens
layout: post
permalink: /2004/05/good-advice-dont-let-performance-overly-influence-design/
categories:
  - Java
---
Matthew Wilson has some good advice in this thread on [<u>A good performance architecture ?</u>][1]. 

*  
Don&#8217;t worry too much about performance in your design phase. Dont ignore it of couse. Implement a smart design and it will alow for the changes that may ha  
ve to be made for performance.  
* 

Based on my experiences, I tend to agree. There are often too many variables still outstanding during the design phase that would prevent any non-high lev  
el performance choices from being made. It&#8217;s difficult to tune for performance unless you have intimate knowledge of the various components and their requ  
irements. This type of knowledge isn&#8217;t typically available during the design phase of many projects. Try and understand the limitations of the particular  
technology you&#8217;re considering, but don&#8217;t allow the limitations to force you into making **silly** design decisions. 

Design and implement a solid flexible architecture (easier said than done). Implement iteratively where possible, getting feedback and usage statistics fr  
om the prospective enduser(s) as you go. Use the information gathered at each iteration to further solidify your implementation, allowing you to make the  
necessary changes only as required.

 [1]: http://www.theserverside.com/discussions/thread.ts<br />
s?thread_id=26171 "A good performance architecture ?"