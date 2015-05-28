---
title: Company-wide Scripting Languages (unix shell languages versus jython)
author: ajordens
layout: post
permalink: /2005/04/company-wide-scripting-languages-unix-shell-languages-versus-jython/
categories:
  - Open Source Software
---
Caught the following post @ &#8216;the life of glenn&#8217; about [scripting languages][1]

*Lately I&#8217;ve been thinking about how important it is for a company to standardize on a scripting language. We had some scripts that help us deploy our s  
oftware on client machines. The problem is they rely on bash being in a certain location the machine running the script. If we write our scripts in a java  
scripting language and take the language with us when we go to deploy the software it will solve all of our problems. Currently at work we have perl script  
s, python scripts, groovy scripts, and of course the standard shell scripts.</p> 

I think for personal use on your own machine in the office you can use what ever you wish but scripts that others in the company use it should be standardi  
zed. Just might thoughts after doing a hard run today.  
</em>

Well, it comes down to what you and your administrators know. There&#8217;s always more than one way to skin a cat.

perl has it&#8217;s uses, bash definately has its uses, and even python/jython have their uses, as do csh, tcsh, zsh, etc.

Do i want to have to copy my scripts dependencies everywhere I want to run my script. Not really, at least with todays systems.

In this particular case (I know the details because I work with Glenn), the problem was because the original author of the bash scripts developed them on a  
linux machine and we went to use them on a new solaris machine, where /bin/sh != bash of course. Switching the #! fixed our problems for the most part.  
You have this same problem with perl scripts when perl is not installed where the scripts expect them. 

The problem with saying you shouldn&#8217;t use bash or another shell scripting language and standardize on something like jython, is that unless you&#8217;re going to  
make system calls, you&#8217;re eliminating all the useful unix command-line tools that are available. On the flipside, if you are making system calls, then yo  
u&#8217;re depending on the availability of certain versions of the command-line tools being available (ie. gnu tools vs. traditional solaris tools) which could  
potentially be a mistake onto its own.

If I want someone else to maintain a script (or heaven forbid execute it or make an on the fly modification), I can&#8217;t really expect them to learn a java sc  
ripting language. It&#8217;s sort of a catch-22, if java script languages were available everywhere (let alone java being available everywhere), perhaps such a  
thing would be viable. But until such time, we&#8217;re stuck with tradition.

So in the end, nice idea Glenn, but I don&#8217;t think I&#8217;ll be endorsing the change <img src="http://littlesquare.com/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

 [1]: http://glennsaqui.blogspot.com/2005/04/scripting-languages.html