---
title: Good ANTLR Resource
author: ajordens
layout: post
permalink: /2008/09/good-antlr-resource/
categories:
  - General Discussions
  - Java
---
I was playing around with ANTLR today and was at bit overwhelmed at both the detail and lack of detail in various documentation and resources I was able to find. Plenty of grammar examples kicking around but some more recent tutorials that used ANTLR v3 would have been helpful.

The problem I&#8217;m trying to solve is simple, define a grammar for a basic search language (*to potentially be extended over time*), parse it into an AST and manipulate appropriately.

After some initial frustration, I did make headway on parts 1 + 2 of the plan. We&#8217;ll see how the rest plays out next week.

For the benefit of others, if you&#8217;re looking to get started with ANTLR, here&#8217;s a useful introduction [blog post][1]. A quick search on dzone would have saved some trial and error.

For what it&#8217;s worth, getting ANTLR hooked into Maven is pretty simple and there&#8217;s decent documentation available for that. The IntelliJ plugin for ANTLRWorks is quite slick and includes a nice debugger.

I&#8217;m going to have to pickup *The Definitive ANTLR Reference* if this implementation pans out.

 [1]: http://blog.centuryminds.com/2008/09/antlr-tutorial-dependency-injection-language/