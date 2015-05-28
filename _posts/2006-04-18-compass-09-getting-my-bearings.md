---
title: 'Compass 0.9 : Getting my bearings'
author: ajordens
layout: post
permalink: /2006/04/compass-09-getting-my-bearings/
categories:
  - Java
  - Open Source Software
---
I just caught an announcement that Compass 0.9 was released. Not knowing what Compass actually was, I ventured over to the OpenSympony [site][1].

> Compass is a first class open source Java Search Engine Framework, enabling the power of Search Engine semantics to your application stack decoratively. Built on top of the amazing Lucene Search Engine, Compass integrates seamlessly to popular development frameworks like Hibernate and Spring. It provides search capability to your application data model and synchronizes changes with the datasource. With Compass: write less code, find data quicker.

Sounds pretty cool, basically an integration point between Lucene and Hibernate/Spring. It&#8217;s been an area of interest for some time, I&#8217;ve wanted to build a more googlish/search engine-ey interface to one of our applications at work. We&#8217;ve got rudementary searching in place, but it&#8217;s more pre-defined than ad-hoc. We provide the entities that you can search on and the relationships are mapped behind the scenes.

It works and it might even be more usable than something relatively open-ended like a traditional engine, but hey, we&#8217;ve utilizing hibernate on the persistence tier, I might at least try and incorporate something.

So I set out tonight to see how far I could get in a couple hours. Compass&#8217; integration with Hibernate &#038; Spring is fairly straight-forward, basically point it at an initialized SessionFactory and you&#8217;re set. **Note**: If you&#8217;re using Spring you must use the SpringHibernate3GpsDevice instead of the Hibernate3GpsDevice (it&#8217;s pretty funny what compass is doing behind the scenes to ensure that its event listeners get registered on the session factory, re: FieldInvoker&#8217;s on private collections, etc.).

The sticking point that prevented me from actually getting something real going was the compass equivalent of a mapping file. Currently there&#8217;s no easy way to convert an existing hbm hierarchy to compass. A tad unfortunate and there&#8217;s been some rumblings on the [user forums][2] but it&#8217;s not there yet. I&#8217;ve got an idea to whip a little templating solution together that&#8217;ll parse a simple text file and generate the approprate compass files. It shouldn&#8217;t be that difficult to hack together (easier than parsing the hbm.xml files) and it should give me an idea of whether or not there&#8217;s value in continuing down this path.

Needless to say it looks pretty interesting and the community seems active. I&#8217;ll post again a bit later in the week as I have time to work on this.

 [1]: http://www.opensymphony.com/compass/
 [2]: http://forums.opensymphony.com/forum.jspa?forumID=37