---
title: Using Interfaces with JAXB
author: ajordens
layout: post
permalink: /2009/11/using-interfaces-with-jaxb/
categories:
  - General Discussions
---
I set about the other day to use JAXB-annotated classes to generate some JSON as part of some web services work.

The trivial case worked.

> @XmlRootElement   
> public class ExtMessage   
> {   
> &#160;&#160;&#160; private String owner; 
> 
> &#160;&#160;&#160; @XmlElement   
> &#160;&#160;&#160; private ExtConcreteBody body; 
> 
> }

What I set about doing next caused some immediate grief.&#160; My intention for ‘body’ is to actually be one of many JSON entities. First attempt was to introduce a JSONBody interface and use that instead of ExtConcreteBody.

> @XmlRootElement   
> public class ExtMessage   
> {   
> &#160;&#160;&#160; private String owner; 
> 
> &#160;&#160;&#160; @XmlElement   
> &#160;&#160;&#160; private JSONBody body; 
> 
> }

Of course that didn’t work.&#160; At marshalling time, the JAXB provider complained about not supporting interfaces.

A quick search on Google said I wasn’t the only person who had run into this problem before.&#160; 

Best resource I found was the [JAXB User Guide][1].&#160; Seems to have some funny rendering and be slightly out of date, but it led me down the correct path.

Essentially you need to make use of an **XmlJavaTypeAdapter**.&#160; JAXB ships a default one (AnyTypeAdapter) that will generate a ‘<font face="cour">type="xs:anyType"</font>’ in your xml schema.&#160; If you want specific type support, you can implement your own Adapter.&#160; 

After adding the class-level @XmlJavaTypeAdapter(AnyTypeAdapter.class) to JSONBody, I thought I had it licked.

Then the JAXB provider complained that “Marshalling Error: class [&#8230;] nor any of its super class is known to this context”.

**WTF?**

Fortunately that led me to a comment on a random blog post on [Collections and JAX-RS][2] mentioning that you should use an @XmlSeeAlso(…) if you want to avoid that error.

Finally it works.

> @XmlRootElement
> 
> @**XmlSeeAlso**(ExtConcreteBody.class)   
> public class ExtMessage   
> {   
> &#160;&#160;&#160; private String owner; 
> 
> &#160;&#160;&#160; @XmlElement   
> &#160;&#160;&#160; private JSONBody body; 
> 
> }
> 
> @**XmlJavaTypeAdapter**(AnyTypeAdapter.class)   
> public interface JSONBody   
> {   
> }
> 
> @XmlRootElement   
> public class ExtConreteBody implements JSONBody   
> {   
> &#160;&#160;&#160; private int id;
> 
> }

The JSON looked like:

> {"extMessage":{"body":{"@type":"extConcreateBody","id":"0"},"owner":"dummy.user"}}

Which seemed reasonable to me.

Hopefully this helps anyone else out there that is having grief trying to do the same thing!

 [1]: https://jaxb.dev.java.net/guide/Mapping_interfaces.html
 [2]: http://syrupsucker.blogspot.com/2008/10/collections-and-jax-rs.html