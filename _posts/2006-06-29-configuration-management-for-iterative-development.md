---
title: Configuration Management for Iterative Development
author: ajordens
layout: post
permalink: /2006/06/configuration-management-for-iterative-development/
categories:
  - General Discussions
---
We&#8217;re currently going through a bit of a development methodology change from fairly heavyweight 3-6mo releases (typically consisting of requirements, development and finally QA) to far more agile 3 week iterations.

It&#8217;s looking like each 3 week iteration will be broken down as follows: 70% development, 20% QA and 10% planning, give or take a few hours.  The formal planning of each iteration will soley focus on the tasks being worked on during the roughly 2 weeks of development time.  More forward-looking planning will occur outside the course of normal iterations.  The 20% of QA time will be include both developers and dedicated qa persons.  We&#8217;ve found that developers have a knack for uncovering problems (perhaps by their own design) that QA miss, and vice-versa, QA has much more thorough testing procedures than developers.  Previously developers have been involved with QA on an as-needed basis so it&#8217;ll be interesting to see how it works out as they&#8217;re formally included in the process.

Given that our iterations are quite short, we&#8217;ve put some emphasis on developing a configuration management process that remains lightweight while encouraging frequent commits and testing without hindering the rest of the development team.  We migrated from CVS to Subversion about 10 months ago and haven&#8217;t looked back since.  The ability to branch in constant time was and remains a motivating factor.  After reading some of Brad Appleton&#8217;s comments on [parallel software development][1] best practices, we&#8217;ve decided to start with the following branching strategy:

  1. The trunk remains relatively sacred (the only thing more sacred is a maintenance branch).  Commits to the trunk should primarily consist of merges from iteration or maintenance branches.  Rarely would there be a need to do an online commit of code that didn&#8217;t exist previously in another branch (maintenance, iteration, bug fix, etc.).
  2. The work of each iteration will be performed on an *iteration* branch.
  3. Each task in an iteration will be performed on a sub-branch off the primary *iteration *branch.  This is to enable multiple developers from different teams to collaborate on a feature set without worry about the rest of the team.  At the end of the task, the branch should be merged back into the iteration and removed.  For some reason if a task does not get completed in the two weeks of development, it does not get merged down and work likely continues during subsequent iterations (although red flags should be raised if you&#8217;ve got tasks spanning iterations).
  4. At the end of the iteration, the branch is tagged, and merged down to the trunk and the process starts over again.

We&#8217;ve attempted to keep the amount of process-related overhead to a minimum without sacrificing quality and artifact (tasks) tracking.  With any luck things will work out, and if not, the nice thing is we&#8217;ll be able to make adjustments on subsequent iterations&#8230; something that previously wasn&#8217;t easily accomplished on 6mo iterations.

Personally I&#8217;m looking forward to the change.  I&#8217;ve been relatively fortunate that as a technical lead I&#8217;m primarily responsible for the technical underpinnings (items like CruiseControl, SVN, etc.) of the process rather than the planning aspects of a particular iteration or increment (set of iterations that make up a release).  It&#8217;s going to be nice working on deliverables that are scoped well enough that you can get everything done in 2 or 3 weeks of development time!

 [1]: http://www.cmcrossroads.com/bradapp/acme/branching/