---
title: Code Reviews w/ Crucible
author: ajordens
layout: post
permalink: /2007/04/code-reviews-w-crucible/
categories:
  - General Discussions
---
We&#8217;ve used [FishEye][1] to better understand our source code repositories for some time now. 

Cenqua (the Austrailians behind Fisheye) were exhibiting at last years JavaOne. I mentioned that we actually paid for FishEye (they gave the impression that most people eval&#8217;d continouslly) and they were quick to explain their new product and offer entry to early access program around it. This new product was [*Crucible*][2]* *and it&#8217;s motivation was to provide a means to perform efficient and effective offline code reviews.

I was generally impressed with their brief demo and left excited.

Traditionally, our code reviews have been face-to-face interactions where one person (the reviewer) looks over varying amounts of code prior to the author checking it in. However tedious they may be, code reviews help maintain a certain quality in the code base and are treated as a learning opportunity, particularly if the author is more junior and the reviewer senior. 

*Crucible* provides an integration to FishEye that allows you to easily manage the review process around a particular change set. You&#8217;re able to select multiple authors (a useful thing when you want multiple eyes looking at the same piece of code) and perform a review using a nice Ajaxy web interface. Now that the product has emerged from its early access program, you can get a demo or trial version of at its [website][3].

The entire process is managed offline, you&#8217;ll get an email notifications whenever you&#8217;ve been selected as a reviewer or someone has commented on your code. 

Part of the problem we face at work with online code reviews (reviews that preceed a checkin) involves scheduling. More often than not, there&#8217;s a non-trivial amount of code to review and the emphasis is often placed on getting it checked in. Keeping track of the required changes (and following up on) can be difficult as well. Not to mention that it can be distracting to have to spend an hour or two reviewing code.

Needless to say, Crucible is nice but not perfect. For us, policy still dictates that we don&#8217;t want code committed to the repository without review. With Crucible, we&#8217;ll commit to a private branch, have it reviewed, and merge down to the respective trunk. 

There&#8217;s been discussions around the office that it would be nice to be able to perform a review off of a *diff* file. Face to face interaction is also lost when using a purely offline tool. Although, this can be partially solved if the author is providing timely replies to the reviewers comments.

In the end, it&#8217;s a useful tool. We&#8217;re still using the early access release and it hasn&#8217;t been rolled out to all of development. That being said, most of us that did use it found it beneficial. If we could get *diff*-based reviews, we&#8217;d be sold.

 [1]: http://www.cenqua.com/fisheye
 [2]: http://www.cenqua.com/crucible
 [3]: http://www.cenqua.com/crucible/