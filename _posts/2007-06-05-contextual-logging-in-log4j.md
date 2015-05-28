---
title: Contextual Logging in Log4j
author: ajordens
layout: post
permalink: /2007/06/contextual-logging-in-log4j/
categories:
  - citations
---
Just caught an interesting post come through JavaBlogs regarding [Atlassian][1]&#8216;s approach to [providing additional context][2] when logging errors in Confluence.

It brought something to my attention that was previously unknown, that is the Log4j *mapped diagnostic contexts* (not to be confused with the *nested diagnostic contexts or NDCs*). See the log4j wiki entry on [NDCvsMDC][3].

Evidently I live in a cave (or perhaps have been using commons-logging for too long) but basically a MDC is a thread-local&#8217;d structure exposing a map-like interface that, depending on your logging pattern, can be included in your logged messages. Particularly useful stuff if you&#8217;re developing a multi-threaded system (be it swing, j2ee or some other inherently multi-threaded framework) and want to provide useful debugging information.

UltraLightClient has an [entry][4] in their code community providing a logging example using MDC and Log4j.

Nice and simple.

 [1]: http://www.atlassian.com
 [2]: http://blogs.atlassian.com/developer/2007/06/a_little_more_context_with_you.html
 [3]: http://wiki.apache.org/logging-log4j/NDCvsMDC
 [4]: http://ulc-community.canoo.com/snipsnap/space/Log4J+MDC+Integration