---
title: Lessons Learned as a Project Lead
author: ajordens
layout: post
permalink: /2008/10/lessons-learned-as-a-project-lead/
categories:
  - General Discussions
---
It&#8217;s been a busy couple of months. For those that don&#8217;t know, my role has shifted slightly from being focused on the technical aspects of an existing product to leading a few seasoned developers in their efforts on an entirely new suite of products. It&#8217;s an interesting challenge to do *green-field* development again, particularly in a different (*but complementary*) [domain][1].

We are approaching the 6 week and it&#8217;s about time I reflect on what we&#8217;ve accomplished and tease out a handful of lessons learned.

I&#8217;ll be using the terms *iteration* and *sprint* more or less interchangeably in what follows.

**Lesson #1 : Be Agile**

*Being agile* is a pretty generic goal these days. To be specific, we&#8217;ve found a lot of value in developing rhythm within the team; things like regularly sized iterations, scheduled kick offs, test days, retrospectives, etc.

Shorter iterations (*we&#8217;re doing 2 week*) have forced us to decompose tasks at a sufficiently granular level. Borrowing some thoughts from [Joel Spolsky][2], we&#8217;ve set an upper bound of task size at 2 days to help drive the necessary design aspects. On the flip side, we generally don&#8217;t go smaller than .5 day estimates. Estimates are done as a team using [planning poker][3]. There are still surprises but we&#8217;re finding out about them after a day or two which makes the response that much easier to make.

Like any project, an iteration must have a well defined beginning and end. In our case, we spend a couple hours on the Monday morning doing the necessary breakdowns for the sprint. The sprint concludes with an all hands test day on the Friday (*2 weeks later*) with a quick planning meeting the afternoon before. Iteration retrospectives are held on either Friday or Monday as scheduling permits.

Focusing on having working software (*and being able to demo it*) at the end of an iteration is important. I&#8217;ll admit failure in this (*so far*) but we&#8217;re committed to regular iteration demos starting next week. In our case, the product manager has expressed an interesting in giving these demos which should help drive home the customer problems we&#8217;re addressing.

Test days are critical to the success of an iteration. In my opinion, you shouldn&#8217;t be coding features on the last day of an iteration*.* You should be testing. If you&#8217;ve been regularly testing throughout the iteration than you likely won&#8217;t need an entire day but the distinction is vital.

Resist the temptation to focus solely on feature development, fallout from test day needs to be included in the next iteration.

Lastly, it&#8217;s important to take time to reflect on the iteration. Grab a few beers and take the last hour of an iteration to discuss the good and bad with your team. Document the feedback and **be prepared** to incorporate it into the next iteration.

**Lesson #2 : Communication**

Nothing new here, a team must communicate in order to be successful. For us, we&#8217;ve found value in regular 15 minutes morning scrums to discuss current tasks and blockers. Even though we all sit together in the same *pod*, IM is a significant inter-team communication tool for us.

As the project lead, I&#8217;ve got regular weekly opportunities to share status with other project stakeholders. There are weekly meetings with requirements analysts to discuss two things.

  1. Acceptance criteria for a feature currently under development.
  2. Sign-off for completed features.

In week one of an iteration, we&#8217;re focused on specifying acceptance criteria for the features we will be implementing. In week two we&#8217;re getting sign-off for the features that we did complete. *Rinse and repeat*.

These meetings are quick (*1hr*) and should stay that way.

**Lesson #3: Adequate Tooling**

We work in an environment that has embraced the [Atlassian][4] product suite (*JIRA, Confluence, FishEye, Crucible and Bamboo are all heavily used*).

It&#8217;s important to track the status of both an iteration and project. Stakeholders need this information regularly and you need to be able to provide it regularly (*with minimal effort to boot*).

There are a number of perfectly acceptable ways to track the status of a project, some manual and some electronic.

> Our typical approach to task management involves using physical cards*.* A team would do a breakdown and the outcome would be a series of task cards (*including an estimate*). The developer would be assigned 1..* cards and expended effort would be recorded directly on the card. When work was completed, test suggestions were written on the card and then handed off to QA.

> The project lead would look at the stack of tasks and produce a burn down chart to share progress with stakeholders.

I had a few problems with the manual nature of this process. There are three inputs to an iteration: bugs, user stories/tasks, and general to-do items. My pet peeve was in the general duplication of information. Bugs and general to-do items are already tracked in JIRA, and having to also track them on task cards seemed counter-intuitive. Not to mention the effort required to manually manage burn-down charts.

Fortunately for us, there is an extension ([GreenHopper][5]) available for JIRA that essentially duplicates what we were previously doing manually. We&#8217;re now consistently tracking bugs, user stories/sub-tasks, and general purpose to-do&#8217;s. *GreenHopper* leverages existing JIRA functionality around time tracking and reporting to provide a series of planning and task-oriented views. Everything is interactive and moving a task from one iteration to another is a simple drag and drop operation. *GreenHopper* can generate burn-down charts for particular iterations and JIRA is able to track estimation accuracy (*amongst a slew of other things*).

To summarize, I&#8217;ve still got time to write code which equates to me being a pretty happy camper.

*Process is important as much as it enables you to consistently move forward. Too little and you won&#8217;t know where you&#8217;re going, too much and you&#8217;ll never get there.*

 [1]: http://www.genologics.com/biorepository
 [2]: http://www.joelonsoftware.com/items/2007/10/26.html
 [3]: http://www.planningpoker.com/
 [4]: http://www.atlassian.com/
 [5]: http://www.greenpeppersoftware.com/confluence/display/GH/Plugin