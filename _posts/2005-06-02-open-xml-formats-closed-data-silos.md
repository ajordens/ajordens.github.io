---
title: Open XML formats, Closed Data Silos
author: ajordens
layout: post
permalink: /2005/06/open-xml-formats-closed-data-silos/
categories:
  - General Discussions
  - Open Source Software
---
I&#8217;ll start off this post by saying kudo&#8217;s to Microsoft for the announcement that * for the first time the default file format (I&#8217;m assuming in Office 12) will be open and accessible by anyone*. I haven&#8217;t yet had time to watch the video but I&#8217;ll do that tonight. There is a lot more information on the new open data formats at [Channel9][1] (including a video). Brian Jones has also starting [blogging][2] and has more information regarding the formats there (including links to a couple whitepapers).

This is very important to all end users, developers and mom/pop&#8217;s alike. It&#8217;s also equally important that Microsoft isn&#8217;t going to force you to upgrade to take advantage of the new format, they&#8217;ll be providing patches for 2000, 2003 and XP. There will be varying levels of support for the format (ie. With the new open formats, embedded ole objects will be stored as an embedded xml structure within the enclosing xml file, while in backports, embedded ole objects will be stored as binary in closing file). The embedding of xml structures is a fairly nice aspect as it could allow users to make changes any aspect of a document (including the sub-components) independent of using Office. Icing on the cake is the document compression which looks to result in a reduction of file sizes compared with previous binary formats. 

Scoble, any idea if these [viewers][3] will get updated to support the new xml format(s)? 

I&#8217;d like to relate this to a problem we&#8217;re facing in my line of work (that is, developing scientific data management tools for Labs). Our customers have made significant capital investments in instruments that to date (and for the foreseeable future) only output proprietary data formats. It&#8217;s a bit worse than the Microsoft situation, because there are multiple binary data formats (storing vast amounts of data) with each vendor providing software that only allows viewing of their own format. Each instruments is effectively treated as an independent data silo. Times are changing and there has been a movement at various institutions and standards organizations to develop an open xml-based format and analysis tools that will work on this open format. End-users are beginning to understand the benefits of the open format and what it allows them to do (ie. better downstream analysis of data across a variety of commercial and open-source tools, you&#8217;ll no longer be strictly limited to the manufacturers set of tools). The biggest problem people are facing is trying to convince the large instrument manufacturers to adopt such a format. Until such time as we have vendor support, the standards bodies have been forced to attempt the reverse engineering of these data formats. It&#8217;s a difficult problem because it does takes substantial effort to understand a data format that has no assurances of remaining static between releases. I&#8217;d love to see some of these manufacturers follow Microsofts lead but I don&#8217;t think its likely any time soon.

 [1]: http://channel9.msdn.com/ShowPost.aspx?PostID=73329
 [2]: http://blogs.msdn.com/brian_jones/
 [3]: http://www.microsoft.com/office/000/viewers.asp