---
title: 'If All Else Fails&#8230; try Oracle Text'
author: ajordens
layout: post
permalink: /2006/10/if-all-else-fails-try-oracle-text/
categories:
  - Database
---
The last week or so I&#8217;ve spent doing some performance optimizations on our application in preparation for a data-intensive demo.

Everything was going well, caught some of the low hanging fruit (running things on the EDT, not batching requests, retrieving too much data, etc) but ran into a brick wall when trying to do a contains (%VALUE%) query on a table with 100k records joined to a table with 75million records.

ie) SELECT tableA.* from TableA tableA join TableB tableB on tableA.fk = tableB.pk WHERE tableB.sequence LIKE &#8216;%VALUE%';

The explain plan (the DB in this instance was Oracle) didn&#8217;t look bad when doing the query on TableB, but when joining to TableA it absolutely blew up.

To cut to the chase here, I ended up creating a contextual index on the column using the [Oracle Text][1] package that was installed along with the DB. The explain plan complexity droped like a stone and things were good again.

In the end, a rather simple solution to a problem that was quite significant in our books. I don&#8217;t know enough about the Oracle Text package to say whether its a good thing or not. We&#8217;re doing context-based searches on long strings of characters, not the documents for which it appears to have been defined. Already I&#8217;ve found that a search for 3 characters takes magnitudes amount of time longer than a search for 4 characters (although this makes sense).

What I didn&#8217;t try was creating a straight index on the column but from people I talked to and what I read that wouldn&#8217;t have helped in the case of the %%. We had another case where an UPPER() function call was causing it to miss an index, but I believe in that case I should be able to create a index on the UPPER&#8217;d result or perhaps another column in the table and a trigger that always UPPER()&#8217;s the result in it.

Back to my regularly scheduled life as a developer, too much DB work for one day.

 [1]: http://www.oracle.com/technology/oramag/oracle/04-sep/o54text.html