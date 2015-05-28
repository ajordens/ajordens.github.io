---
title: PostgreSQL on Windows
author: ajordens
layout: post
permalink: /2005/01/postgresql-on-windows/
categories:
  - Open Source Software
---
I&#8217;m sure you&#8217;re all aware that PostgreSQL 8.0 was release a couple days ago and a notable (and long awaited feature) was native support for windows.

I&#8217;ve yet to really put it through its paces on Windows, but I was impressed with the ease of install. Nothing out of the ordinary, just straight forward,  
(almost) no questions asked installation. 

**  
Whats New:**

**Savepoints**

*Savepoints allow specific parts of a transaction to be aborted without affecting the remainder of the transaction. Prior releases had no such capabilit  
y; there was no way to recover from a statement failure within a transaction except by aborting the whole transaction. This feature is valuable for applica  
tion writers who require error recovery within a complex transaction.*

Important for SQL conformance. I don&#8217;t really write the kind of applications that require DB-level save points. I&#8217;m usually abstracted by CMP in JBoss an  
d Hibernate for offline processes.

**Point-In-Time Recovery**  
*  
Though PostgreSQL is very reliable, in previous releases there was no way to recover from disk drive failure except to restore from a previous backup or us  
e a standby replication server. Point-in-time recovery allows continuous backup of the server. You can recover either to the point of failure or to some tr  
ansaction in the past.*

I&#8217;ve been happy with PostgreSQL&#8217;s reliability since [we][1] started using it as one of our supported JDBC data sources.  
The lack of point in time recovery capabilities was not a significant drawback but improved restoration is welcome.

**Tablespaces**

*Tablespaces allow administrators to select the file systems used for storage of tables, indexes, and entire databases. This improves performance and co  
ntrol over disk space usage. Prior releases used initlocation and manual symlink management for such tasks.*

Important for deployment into enterprise environments. 

**Improved Buffer Management, CHECKPOINT, VACUUM</strong<</p> 

*This release has a more intelligent buffer replacement strategy, which will make better use of available shared buffers and improve performance. The pe  
rformance impact of vacuum and checkpoints is also lessened.*

Performance improvements are always welcome. 

**Change Column Types**

*A column&#8217;s data type can now be changed with ALTER TABLE.*

Sure, I guess its important but not the kind of thing I routinely do.

**New Perl Server-Side Language**

*A new version of the plperl server-side language now supports a persistent shared storage area, triggers, returning records and arrays of records, and  
SPI calls to access the database.*

This is an interesting improvement. To date we&#8217;ve really stayed away from using DB-specific stored procedures and whatnot. I don&#8217;t think that the plperl  
additions are going to do anything to change this, but they&#8217;re something I might play around with in whatever spare time I can find.

**Comma-separated-value (CSV) support in COPY**

*COPY can now read and write comma-separated-value files. It has the flexibility to interpret non-standard quoting and separation characters too.*

Meh, not overly important to me.

All in all, I&#8217;m primarily concerned with performance. I realize its not Oracle and nor do I expect it to be. PostgreSQL is an entry-level database but w  
e have had good success with it to date. It does have a fairly decent feature set and sql compatibility compared with its direct competitors. First and f  
oremost, I welcome any and all performance improvements. The support for the windows platform should expose a few more people to the database who previous  
ly avoided it (because of the extra steps involved in setup, cygwin&#8230;etc) and went with MySQL.

 [1]: http://www.genologics.com/