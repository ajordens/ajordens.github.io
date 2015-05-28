---
title: What makes an effective code review?
author: ajordens
layout: post
permalink: /2008/02/what-makes-an-effective-code-review/
categories:
  - General Discussions
  - Java
---
As developers, we&#8217;re all responsible for writing code in one way or another. We write it ourselves or help others write it better. Either way, code gets written and we all move on.

The rest of this short post will be focused on code reviews and what (<span style="font-style: italic;">I think</span>) makes them efficient and beneficial.

**Code Reviews (CRs)**

> <p style="font: 12.0px Helvetica">
>   <strong>Code review is systematic examination (often as peer review) of computer source code intended to find and fix mistakes overlooked in the initial development phase, improving both the <span style="font-style: italic;">overall quality of software</span> and the <span style="font-style: italic;">developers&#8217; skills</span>. &#8211;</strong> <strong>Wikipedia</strong>
> </p>

It&#8217;s not a stretch to realize that there is a strong relationship between the overall quality of software and the skills of the developers building it. Invest in developer education and you should have better software coming out the other end (<span style="font-style: italic;">at the very least you&#8217;ll have different and likely more challenging problems &#8211; assuming you&#8217;re not bottlenecked on process</span>). In my mind, code reviews are an essential part of any development process. Regardless of whether you do them face to face or over the &#8216;net, the code will always come out better and the reviewers better informed.

**What a Code Review isn&#8217;t**

A code review isn&#8217;t an exercise in rubber stamping. It&#8217;s an opportunity for both the developer and reviewer to reach consensus while verifying that the proposed implementation or code change under review satisfies both the functional and non-functional requirements of the system. If it isn&#8217;t satisfactory, the expectation should be that any required changes will be made and the code re-submitted for review. The reviewer should hold power over what gets committed and what doesn&#8217;t.

At the company I work for, code reviews are mandated for every non-trivial commit, regardless of whether you&#8217;re a junior or senior developer. In the past our reviews have typically involved two people (developer and reviewer) and been done at the developers desk. They&#8217;re scheduled adhoc-ly with the reviewer involved generally being someone with an in-depth knowledge of the area being modified. More recently, we&#8217;ve been trying out [Crucible][1] in support of offline CRs.

It goes without saying that any code submitted for review should be atomic. Nobody likes reviewing 50+ significantly changed files on a project you spent the past 3 weeks working on. Break that down into three separate commits and everyone involved will be much happier :).

**What&#8217;s Worked**

A lot of things have worked. We&#8217;ve gotten progressively better over the past few years with every project making noticeable improvements to our overall development process.

Obviously the good thing for us is that code is getting reviewed before it gets committed to the repository. We&#8217;ve taken to documenting common problems and have developed a quick check list to help ensure a more thorough review. We&#8217;re generally successful with our attempts to have more senior developers (or domain experts) do reviews for junior developers, although it does vary a bit depending on the stage of development we&#8217;re in.

Alongside the code review check list, we&#8217;ve also developed a series of lessons we&#8217;ve learned the hard way. Unfortunately, software development is complex and you&#8217;re going to make mistakes along the way. It&#8217;s part of the learning process and the only way you&#8217;re going to avoid repeating them is to make sure they&#8217;re well documented and made front and center.

**What Could Be Better**

Scheduling of reviews has been a hot topic for us in the past. People are busy and it hasn&#8217;t always been possible to get the most appropriate person involved in a review. Part of the motivation for looking at a tool like Crucible is to enable offline code reviews at the convenience of the most appropriate reviewer. An offline CR is one in which the developer commits his/her change to a private branch and schedules a web-based review (using Crucible). Once the CR is complete, comments are sent back to the developer who then addresses them and either gets a follow-up in person review or schedules another offline one.

There are certainly benefits and drawbacks to both approaches. An offline CR loses a bit of the human touch and the emphasis on education could be diminished. Something that I&#8217;ve been experimenting with is doing an initial face-to-face review but committing to a private branch. The reviewer can then take a more in-depth look (at their leisure) at the code in a private branch before it&#8217;s actually merged into a team branch.

It&#8217;s important to have a process around code reviews. Something we&#8217;ve learned the hard way is that large commits (50+ files) don&#8217;t go over very well with reviewers (in-person or otherwise). They take a long time and diminishing returns start after you&#8217;ve been looking at code for longer than an hour or two. That being said, some large changes are unavoidable and have to be dealt with, but more often than not with a bit more decomposition you&#8217;ll have a handful of atomic commits that collectively address the same problem. It&#8217;s not surprising that most of the large change sets I&#8217;ve seen have come at the end of a particular feature or project. Unfortunately this usually leads to a series of conversations around whether we can afford to slip a completion date in order to ship code that&#8217;s up to par. Nobody likes to have these conversations.

The other thing to note is that it&#8217;s important to have documented outcomes and follow-up loops. This is more easily accomplished if you&#8217;re using a tool like Crucible, but could be as simple as a page of hand-written notes and a completed checklist.

**What Makes a Good CR** <span style="font-style: italic;">(my top 5)</span>

  * **<span style="font-weight: normal;">Code submitted for review should be atomic and in a consistent state (passing tests, etc.)</span>**
  * **<span style="font-weight: normal;">The size of a change set should be consistent (<span style="font-style: italic;">maybe you set a goal of getting a review after X days or Y modified files</span>).</span>**
  * <span style="font-weight: normal;">Code should be reviewed by someone with a solid understanding of the area being modified.</span>
  * <span style="font-weight: normal;">A review should never be rushed. A reviewer should be free to prevent a commit from going through.</span>
  * **Code reviews must have documented outcomes that can and will be followed up on.**

 [1]: http://www.atlassian.com/software/crucible/