---
title: Having fun and writing good software
author: ajordens
layout: post
permalink: /2010/03/having-fun-and-writing-good-software/
categories:
  - General Discussions
---
The act of writing good software is as much process execution as it is source code generation. Follow the right process and it can be a tremendously enjoyable experience.

There&#8217;s nothing I like better than to come home from a day in the office and marvel at the amount of work accomplished (*easily measured as tasks completed, bugs squashed, etc.*). See that burn down chart trending downwards can bring a tear to a man&#8217;s eye!

Working hard is not what burns me out, it&#8217;s the soul sucking meetings and status updates along the way.

As a working example, I&#8217;m going to outline the high level processes, tools and techniques that my team and I regularly follow during our quest to develop good software and get it into the hands of our customers.

First, I&#8217;ll quickly outline the various tools that are used to make our collective lives much easier.

**Tools**

We are huge believers in the entire Atlassian stack. We started out with JIRA five or six years ago, and our tool box has expanded to include Confluence, Fisheye, Crucible, Bamboo and most recently GreenHopper.

If you&#8217;re a development shop (*of any size really*) looking for a kick ass suite of tools, look no further than what Atlassian has to offer.

For the purpose of this post, I&#8217;m going to focus on JIRA/GreenHopper, Crucible and Bamboo.

JIRA is a typical bug tracking software, [GreenHopper][1] is a set of agile extensions that allow you to easily manage and prioritize User Stories, Tasks, Bugs, etc., visualize burn downs, and manage sprints/releases on a per-project basis.

Every single piece of work we work on is estimated and tracked in GreenHopper. Burn downs are generated automatically and actively monitored. Prior to GreenHopper, we were manually tracking cards on a whiteboard and generating burn downs through Excel. **Very cumbersome**. I don&#8217;t even want to remind anyone of what happens when someone knocks all the cards off your whiteboard.

[Crucible][2] is essentially online code reviews done right. Simply point it a repository (*subversion in our case*) and you can completely manage the peer review process through a web browser. Prior to moving to the online review process, we were doing over the shoulder reviews prior to check-in. This required someone to drop whatever it was they were doing, and head over to your desk for 15-20 minutes. With Crucible, code is committed first and reviews setup immediately after. You can easily track what code has been reviewed and what hasn&#8217;t.

[Bamboo][3] is the last piece of our puzzle and manages all of our continuous integration builds. We have a series of builds that are either run per check-in or nightly. Performance reports are generated and published to a Maven site nightly.

**Process**

For the past two years we&#8217;ve been developing software in effectively two week chunks with a release every month.

Each two week iteration starts on a **Wednesday** and consists of the following:

  * A 1hr kick-off and retrospective meeting
  * Daily 10 minute scrums with members of Development and QA.
  * A 1hr sync. session with Product Management every Thursday to quickly review progress and have any outstanding questions answered.
  * An all hands on deck 2hr test session every second Thursday. This includes members of Development, QA and Product Management.
  * A 15 minute show & tell every second Tuesday (*last day of the iteration*) with members of Development, QA, Product Management and Technical Writing.

Ignoring the scrums, that amounts to < 5hrs of meetings an iteration. Sounds simple right?

All of our kick-off meetings involve a review of our backlog and upcoming iteration. The backlog is a JIRA version that theoretically contains all the user stories, tasks, bugs, and anything that we could possibly work on. It&#8217;s prioritization is a collective effort by both Development and Product Management. Items in the backlog may or may not be estimated, and each 2 week iteration includes roughly 1-1.5 weeks of estimated work per developer. This 1-1.5 dev weeks / iteration / developer is essentially our velocity and can be adjusted to account for risk and granularity of tasks being worked on.

Once tasks are pulled into an iteration, they must be (re)estimated (*typical* *granularity is 1-3 days*). Design is a considered a critical task and it&#8217;s not uncommon to see dedicated design and review tasks in our iterations.

At the end of each iteration we run a retrospective. This gives us an opportunity to review velocity from the previous two weeks, as well as identify things that we did well as a team and things we would like to improve upon. We identify 2-3 items from the list to focus on for the next iteration.

Every morning we kick off the day with a quick 10 minute scrum. This scrum provides each member of the team with an opportunity to highlight what they&#8217;ve worked on in the last day and identify any blockers to the group. Depending on whether or not everyone is in the office, we may choose to run this in-person or via Jabber/XMPP.

Once a week we take an opportunity to sit down with Product Management and review our backlog. We&#8217;ll take a stab at estimating the highest priority items and may even move them into a coming iteration / release. We typically only plan an iteration or two into the future.

Finally, to end of an iteration we have an all hands on deck test day on the last Thursday. This involves all members of development, our QA representative, and at least one person from Product Management. We prepare our test cases ahead of time and take over a board room for 2 hours. It&#8217;s important to get everyone in the same room in order to make efficient use of time. Questions must be answered quickly, and it&#8217;s important to have representation from both Development and Products.

Throughout an iteration we will do frequent deployments for other people in the organization to play with. With only one technical writer for the whole company, it&#8217;s been a difficult haul to keep user facing documentation up to date with each release. In addition to documenting the expected and actual behaviours as part of User Stories, we&#8217;ve started doing quick 20 minute show & tells on the last day of an iteration. This gives the technical writer and product management one last opportunity to review features before the iteration is closed and the release goes out the door.

Assuming everything goes to plan, we close everything down on a Tuesday and prepare ourselves to start fresh on the Wednesday. It&#8217;s important to note that we purposely start and end our iterations mid-week. We found the stress level to be significantly higher when we attempted to rush for a Friday completion date.

That&#8217;s it in a nutshell. We&#8217;ve been following this basic process for the last year or so with a decent amount of success. Of course nothing is perfect and we&#8217;ve made minor modifications as necessary.

I&#8217;d be interested to hear what others are doing for a lightweight agile process and what forms of tooling they&#8217;ve incorporated.

Cheers!

 [1]: http://www.atlassian.com/software/greenhopper/
 [2]: http://www.atlassian.com/software/crucible/
 [3]: http://www.atlassian.com/software/bamboo/