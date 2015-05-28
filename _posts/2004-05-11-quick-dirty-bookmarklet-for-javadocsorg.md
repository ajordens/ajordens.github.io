---
title: 'Quick &#038; Dirty Bookmarklet for Javadocs.org'
author: ajordens
layout: post
permalink: /2004/05/quick-dirty-bookmarklet-for-javadocsorg/
categories:
  - Open Source Software
---
Here&#8217;s a \_very\_ quick and dirty little javascript bookmarklet that I put together for use with the www.javadocs.org service. It will prompt you for a java  
class, and then open the Javadoc&#8217;d API for the class via www.javadocs.org. 

javascript:topic=prompt(&#8216;Search API for&#8230;&#8217; );location=&#8217;http://www.javadocs.org/&#8217; + escape(topic); 

Just add a bookmark with that as the contents and voila. It&#8217;s pretty simple, but it&#8217;ll make my life a bit easier when I want to lookup something quickly. 

Note, that I&#8217;m doing this in FireFox, so your mileage may vary in other browsers. I&#8217;d like to figure out how to add another search engine that will allow  
me to query the javadocs.org without needing the javascript popup prompt.