---
title: First Impressions of Hadoop
author: ajordens
layout: post
permalink: /2008/01/first-impressions-of-hadoop/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
The other night I sat down and spent some time playing around with [Hadoop][1].

What follows here is based on my brief understanding of the project and one nights worth of experience <img src="http://littlesquare.com/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

Hadoop is an Apache Lucene project that provides an open-source implementation of [MapReduce][2]. MapReduce is a programming model emphasizing parallel processing that has been developed and popularized by Google. From everything I&#8217;ve read and seen of Google&#8217;s MapReduce implementation, Hadoop looks to be very similar. Interestingly enough, Yahoo! is a significant supporter of this project and has widely published and presented on their [experiences][3].

Having a general conceptual understanding of MapReduce but little experience with it, I set out to solve a relatively straight forward problem.

As part of our interviewing process, potential candidates are given a programming problem to solve. One that we&#8217;ve used previously involved the parsing of apache-style log files and gathering specific statistics. It wasn&#8217;t a stretch to see how this could be implemented using MapReduce and Hadoop.

**Step 1: Installing Hadoop**

My daily driver is a MacBook Pro so the installation went quite smoothly. Nothing significantly more difficult than unpacking an archive, updating a few environment variables, and running a few example jobs.

I setup a two machine cluster &#8211; my laptop and another VMware virtual machine. Nothing particularly sophisticated.

**Step 2: Breaking down the problem**

The first step of any implementation involves breaking the problem down into a series of map and reduction steps. *Hadoop* provides interfaces and abstract base classes that help you get started. Arguably the process of breaking any problem down into its fundamental building blocks is a significant challenge, but at the same time it&#8217;s part of the elegance enabled by a programming model such as MapReduce.

It&#8217;s important to note that the framework is responsible for all I/O operations and actually builds this functionality on top of it&#8217;s own implementation of a distributed file system. In order to make data available for processing, you must first copy it to the distributed file system. Likewise, if you want to do additional work on output data (*and not do it using* *Hadoop*), you must copy it from the distributed file system. This not only enables larger volumes of data to be made available to the cluster but it also allows the framework to partition and store records closer to the machines that will be processing them. Google has an interesting paper that describes their approach to distributed file systems (See [Google File System][4])

In the simplest terms, a mapping step is responsible for processing input data and generating *key -> value* pairs. *Hadoop* takes care of aggregating all values with their corresponding keys and passing this result (*key -> collection of values*) to a reduction step. A reduction step is responsible for reducing the *collection of values* into a suitable output value. See the Hadoop [quick start guide][5] for a simple implementation of both a map and reduce step.

**Step 3: The mapping step**

Take the following problem definition: *Given a collection of apache log files determine the urls with the most hits and return them in descending order.*

The mapping step is fairly straight forward. It&#8217;s responsible for parsing individual log records and outputting a *url* and *count* for each.

In this example, the count would always be 1 and you can think of this mapping step as a marker. It&#8217;s responsible for flagging the url from each record it parses. It&#8217;s the reduction step&#8217;s responsibility to count up all of the individual flags.

**Step 4: The reduction step**

> *Example Input:* [http://www.google.ca, [1,1,1,1,1,1,1]], [http://www.yahoo.com, [1,1,1], [http://www.microsoft.com, [1,1,1,1,1]]

As mentioned previously, the responsibility of the reduction step in this example is to reduce these inputs by counting up the number of flags. The output would look something like:

> [http://www.google.ca, 7], [http://www.yahoo.com, 3]

**Step 5: Putting it all together**

That&#8217;s it. The result of running a job with these map and reduce steps would be similar to:

> http://www.google.ca 7
> 
> http://www.yahoo.com 3
> 
> http://www.microsoft.com 5

Unfortunately the outputs are sorted by value and we haven&#8217;t yet quite satisfied the problem definition. However, the beauty is that we can now pass this output through another mapper that will invert the key/value and then sort by key. The output of that job will be a list of urls sorted by their hit count. Success!

All in all it&#8217;s an incredibly powerful idea and framework. Absolutely overkill for small tasks like these but if you&#8217;ve got a many terabytes (or petabytes) of data and a couple thousand processing nodes, it&#8217;s more than adequate.

 [1]: http://hadoop.apache.org/
 [2]: http://labs.google.com/papers/mapreduce.html
 [3]: http://developer.yahoo.com/blogs/hadoop/
 [4]: http://labs.google.com/papers/gfs.html
 [5]: http://hadoop.apache.org/core/docs/current/quickstart.html