---
title: 'caBIG Annual Meeting &#8211; A developers perspective'
author: ajordens
layout: post
permalink: /2008/06/cabig-annual-meeting-a-developers-perspective/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
For the past couple of days I&#8217;ve been attending the [caBIG][1] Annual Meeting (*it&#8217;s the 5th such meeting and by all accounts the most well attended*).

**About caBIG**

> **<span style="font-weight: normal;"><em>caBIG™ stands for the cancer Biomedical Informatics Grid™. caBIG™ is an information network enabling all constituencies in the cancer community – researchers, physicians, and patients – to share data and knowledge. The components of caBIG™ are widely applicable beyond cancer as well.</em></span>**
> 
> **<span style="font-style: italic; font-weight: normal;">The mission of caBIG™ is to develop a truly collaborative information network that accelerates the discovery of new approaches for the detection, diagnosis, treatment, and prevention of cancer, ultimately improving patient outcomes.<br /></span>**

**<span style="font-weight: normal;">In a nutshell, <em>caBIG</em> is an initiative of the <em>National Cancer Institute</em> built heavily upon open-source components that aims to motivate and facilitate the sharing of data. It strongly suggests a front-loaded UML workflow (<em>using MDA</em>) and incorporates certain aspects of ontologies and common data definitions to help guarantee consistent semantics (<em>and syntax</em>).</span>**

**<span style="font-weight: normal;">From a purely technical perspective, I&#8217;ve never been sold on the idea of MDA. I&#8217;ve had experience with both open-source and commercial modeling tools that have never fulfilled on the promise of true round-tripping (<em>and if you don&#8217;t have round-tripping&#8230; well, you&#8217;re in for a world of hurt</em>). Now in the <em>caBIG</em> case, there is a pipeline of transformations that you&#8217;re more or less required to run through&#8230;</span>**

  1. **<span style="font-weight: normal;">Create a UML representation of your object and domain models</span>**
  2. **<span style="font-weight: normal;">Annotate the model with caBIG specific annotations and stereotypes</span>**
  3. **<span style="font-weight: normal;">Run the annotated model through the <em>Semantic Integration Workbench</em> (<em>another caBIG tool</em>)</span>**
  4. **<span style="font-weight: normal;">Submit the final model (<em>XMI</em>) to caBIG for approval and insertion into the caDSR (<em>cancer data standards repository</em>)</span>**

**<span style="font-weight: normal;">Make a change in the future and you&#8217;re more or less required to run through steps #1-4 again.</span>**

**<span style="font-weight: normal;">Once you have a validated UML model, you can then run through the <em>caCORE SDK</em> and generate skeleton code for a 3-tiered application consisting of (<em>at a high level</em>) a Hibernate data model, an external API and some middleware code to glue the API and data model together. <em>Round-tripping is essentially non-existent from what I&#8217;ve heard and seen.</em></span>**

**<span style="font-weight: normal;"><strong>You&#8217;re done! Congratulations on achieving Silver-level compliance.</strong></span>**

**&#8230;**

***<span style="font-weight: normal;">wait a second.</span>***

**<span style="font-weight: normal;">It&#8217;s a little bit too process heavy for my liking. I would have liked to see the</span> *<span style="font-weight: normal;">NIH/caBIG</span>* <span style="font-weight: normal;">be first and foremost focused on data interoperability and</span>** less on tools, particularly those that **dictate particular workflow****s** (*like UML -> annotation -> MDA -> Code Generation*).

I&#8217;d much rather see an extensible API with pluggable end-points, a meta data registration service and a suite of validation test cases. Define suitable goals and keep it simple. *Provide suitable incentives and vendors **will** support it*.

There&#8217;s more than one way to provide interoperability.

As a developer working on existing products that are considering support for *caBIG*, the requirement to fundamentally change my development process is a bit unnerving. Speaking generally, there&#8217;s no guarantee that everyone has UML models for their systems and even if they did, attempting to do full MDA transformations on them would be fairly ambitious.

That&#8217;s it for now. It&#8217;s been an interesting conference and I&#8217;ve learned a lot about the various initiatives and their progress. Off to visit customers in Cincinnati tomorrow!

 [1]: https://cabig.nci.nih.gov/overview/