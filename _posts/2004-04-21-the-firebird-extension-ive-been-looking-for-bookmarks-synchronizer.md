---
title: 'The firebird extension I&#8217;ve been looking for&#8230;. Bookmarks Synchronizer'
author: ajordens
layout: post
permalink: /2004/04/the-firebird-extension-ive-been-looking-for-bookmarks-synchronizer/
categories:
  - Open Source Software
---
I&#8217;ve contemplated writing some software to handle bookmark synchronization in Mozilla Firebird (between computers). I&#8217;ve been side-tracked lately with rea  
l work, but I came across <a href="http://forums.mozillazine.org/viewtopic.php?t=41742" target=_new>this</a>. It&#8217;s a bookmark synchronizer that uses FTP t  
o export your firebird bookmarks into xbel and ship them to an ftp site of your choice. You can then hookup your other browsers and have them download the  
xbel bookmarks from the ftp site. I develop both at home and the office and like to have some commonality in my bookmarks between the two locations. Tra  
ditionally I&#8217;ve just exported from mozilla and manually transfered the bookmarks across and imported manually. A bit of a pain to say the least. 

The firebird extension is not perfect, but works alright. It might be nice if it did the file transfers over ssh but I can live with ftp for now. Additio  
nally, it doesn&#8217;t look like it has the ability to merge remote and local bookmark files so that may cause problems if you are simultaneously modifying book  
marks on different systems. 

My original plan for a Java implementation was centered on a distributed system. I don&#8217;t have much experience in the area and wanted something that would  
force me to check out Jini, JXTA and the like. No luck so far but perhaps I&#8217;ll have some time in the future.

Bottom line, if you have multiple systems and want to facilitate some sharing of the bookmarks, check out the &#8216;Bookmark Synchronizer&#8217; extension for Mozilla  
Firebird. It&#8217;d be nice if there was such a thing built into my RSS reader (<a href="http://www.nongnu.org/straw/" target=_blank>Straw</a>), but for now I  
can live with the manual exports.