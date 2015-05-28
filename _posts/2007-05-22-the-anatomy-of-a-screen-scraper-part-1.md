---
title: 'The Anatomy of a Screen Scraper : Part 1'
author: ajordens
layout: post
permalink: /2007/05/the-anatomy-of-a-screen-scraper-part-1/
categories:
  - General Discussions
---
This is the first part detailing my experiences writing a basic html screen scraper using a combination of bash, python and structured grep to retrieve, massage and present data. The results can be seen at [onesecondshy.com][1]. Code will eventually be published there as well.

First off, motivation. The motivation for this little project was to mine the data from [gastips.com][2] and present it more directly (and with less advertisements). GasTips.com is a grassroots site allowing individuals to submit gas prices on a community-by-community basis. Data is presented in well-formed tables accompanied by a plethora of google advertisements.

In an ideal world, we would have APIs that provide data is easily consumable formats. However, as long as there is value attached to data, there&#8217;ll be a desire to keep it private. The following is not meant as a step-by-step guide to scraping data and graphing it in python. Instead, my goal is to simply explain one approach to solving what is a common problem.

**<u>Step 1: Data Retrieval</u>**

Nothing too fancy here. A simple call to *wget* to download raw html.

*Part 2* of this series will move beyond this rather simplistic approach and cover data retrieval and aggregation using a *web spider*.

**<u>Step 2: Massaging</u>**

Once you&#8217;ve got raw html, the next logical step is to reduce it to a format amenable to manipulation&#8230; namely *csv*. *Sgrep* (or [Structured Grep][3]) a tool for searching and indexing html (amongst other things) easily gets the job done.

> <pre>sgrep -g html 'stag("TABLE") containing                       (attribute("SUMMARY") containing "XXX") .. etag("TABLE")' input.html
</pre>
> 
> <pre>&lt;html&gt;&lt;body&gt;&lt;table summary="XXX"&gt;&lt;tr&gt;&lt;td&gt;ABC&lt;/td&gt;&lt;/tr&gt;&lt;/table&gt;&lt;/body&gt;&lt;/html&gt;
</pre>

Running the above *sgrep* command on the html snippet will yield the following result:

> <pre>&lt;table summary="XXX"&gt;&lt;tr&gt;&lt;td&gt;ABC&lt;/td&gt;&lt;/tr&gt;&lt;/table&gt;
</pre>

You could easily take it further and retrieve only the contents of a particular table column or row. When parsing the *gastips.com* data, I used *sgrep* to get the data into a row-delimited form before running a simple python script that converted to csv. The row delimited form was as follows (where *&#8217;s denote a column header):

> <pre>*Header1*
*Header2*                       
Row1Column1
Row1Column2
Row2Column1
...
</pre>

The final *csv* output was:

> <pre>Header1,Header2,
Row1Column1,Row1Column2,
Row2Column1,Row2Column2,
...
</pre>

<u>**Step 3: Presentation**</u>

Sticking with the python theme established in the previous step, I investigated a few python graphing and charting libraries. I settled for the [Matplotlib][4], vastly overkill for my needs but a fun challenge nonetheless.

60 lines of hacky python later and I had something that could parse a csv file and plot resulting data.

Understandably, the devil is in the details. Plotting a simple x,y graph is trivial, it&#8217;s slightly more difficult to create something with some semblance of polish.

**<u>Step 4: Tying It All Together</u>**

The last step in all this is to create a suitable front-end. I chose a simple *for loop* in *bash.*

> <pre><em>for x in urls</em>
<em>1. download raw html</em>
<em>2. massage it (html -&gt; csv)                                                                                                                                          </em>    
<em>3. plot it (csv -&gt; html)</em> 
</pre>

Making a conscious distinction between the crawling (*downloading*), indexing (*massaging*) and presenting (*plotting* ) allows increased opportunity for parallel operations. Once you have the raw data, you can execute multiple indexing and plotting operations. A more scalable alternative to the common monolithic approach encompassing data retrieval, transformation and presentation in a single all-in-one package.

&nbsp;

That&#8217;s it for Part 1. As mentioned earlier, you can see the results at [onesecondshy.com][5]. The plots will actually mean something should you live on Vancouver Island. Future plans include writing a web spider and aggregation of data over a longer period of time (than the week provided by gastips.com) amongst other things.

 [1]: http://www.onesecondshy.com
 [2]: http://www.gastips.com
 [3]: http://www.cs.helsinki.fi/u/jjaakkol/sgrep.html
 [4]: http://matplotlib.sourceforge.net/
 [5]: http://www.onesecondshy.com/