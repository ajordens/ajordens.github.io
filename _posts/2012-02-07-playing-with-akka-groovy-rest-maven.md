---
title: Playing with Akka + Groovy + REST + Maven
author: ajordens
layout: post
permalink: /2012/02/playing-with-akka-groovy-rest-maven/
categories:
  - General Discussions
---
First things first, I consider myself a polyglot programmer reguarly running the spectrum from Java to Groovy to JRuby to Python.  Scala is certainly interesting from the outside looking in, but I haven&#8217;t had the time to jump in with both feet.

My latest forays into Akka came as a result of some investigation I was doing for a new platform at work.  Basically, I was looking for something to handle job/task execution across a number of different physical machines.

One option would have been to rig something up with Groovy, a simple daemon exposing a RESTful API (*or fetched jobs from a message queue*) that used GPars behind the scenes to manage concurrency on each individual machine.  Job state would be bubbling up to an overarching service that could manage scheduling across a few machines.

We&#8217;re already using Groovy/Java on a couple other newish projects and ideally the solution to this problem would also fit in that box.  Scala, as interesting a language as it is wouldn&#8217;t be fair to thrust on a team who&#8217;s language of choice has historically been Perl (*but is moving towards the JVM*).

And so I set forth to survey the landscape for Akka + Java/Groovy examples.  In particular, I was looking for something that combined Remote Actors + HTTP/REST, perferably being built in Maven (*but I&#8217;d take some Gradle*).  I found [a few][1], the chat server ones looked relevant but a little bit dated.  I ended up putting something together myself and pushing it to github.

<https://github.com/ajordens/akka-job-scheduler-example>

It uses Akka 1.3 and has a server component (runnable via **mvn jetty:run**) that hosts remote actors and a simple REST resource.  There is also a client service that can be run on multiple machines, it polls the server for jobs, executes them and fires a response back.

The example is trivialized but it does tie a number of different pieces together.  One bit of initial grief I had was around trying to get akka-http running in Jetty 8.0.4.  It wouldn&#8217;t fly, and I ended up having to fall back to 7.4.0.

 

Enjoy.

 

 

 [1]: http://akka.io/docs/akka/1.3/additional/external-sample-projects.html