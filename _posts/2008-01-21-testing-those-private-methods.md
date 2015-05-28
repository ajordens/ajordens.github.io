---
title: Testing those private methods
author: ajordens
layout: post
permalink: /2008/01/testing-those-private-methods/
categories:
  - General Discussions
  - Java
---
I&#8217;ve been working my way through [Working Effectively with Legacy Code][1] and one of their strategies for testing classes has particularly hit home.

**Situation**

> <p style="text-align: left;">
>   You&#8217;ve fixed a bug in a method that lacks any test cases and is not easily incorporated into a test harness.
> </p>
> 
> <p style="text-align: left;">
>   More often than not this method is private (<span style="font-style: italic;">because we all test our public methods right?</span>)
> </p>

The obvious and straight-forward approach to testing (in this situation) would be to write a test case against whatever public method ultimately results in the problem code being executed.

Unfortunately, if the public method was easily tested we hopefully wouldn&#8217;t be finding ourselves in this situation (<span style="font-style: italic;">because we&#8217;d either have had test cases that already executed the problem code &#8211; or they&#8217;d be easily added</span>).

What you&#8217;re often faced with is a combination of two things, local state maintained by the class (<span style="font-style: italic;">pesky</span> <span style="font-style: italic;">instance variables</span>) and state passed in to the method as parameters. With appropriate use of stubs and mock objects, the latter should be workable. However, unless you&#8217;re dealing with a stateless class the matter of local state is an annoying yet unavoidable complication.

What follows is one idea that I&#8217;ve seen work quite successfully in these types of situations.

**Step 1: The Minor Refactor**

This initial refactor involves extracting the pertinent portion of business logic (that you want to put under test) and any instance-level state that it requires. Often this is as simple as extracting a private method and passing any required class variables/state in as parameters. What you should be left with is a method that has all of it&#8217;s dependencies provided to it, this is important.

<pre>private void updateSpinner(List xyzs)
    {           
        // this map should contain 1 and only 1 spinner
        JSpinner spinner = instanceSpinnerMap.values().iterator().next();
        spinner.setValue(xyzs.size());
        spinner.setEnabled(false);
    }
</pre>

**becomes**

<pre>private void updateSpinner(List xyzs, JSpinner spinner)
    {
        spinner.setValue(xyzs.size());
        spinner.setEnabled(false);
    }
</pre>

Fairly trivial change and significantly more testable (ignoring the fact that it&#8217;s still a private method).

**Step 2: A little less private**

Unfortunately, private methods aren&#8217;t the easiest things in the world to test. You may not like what I&#8217;m going to suggest next&#8230; but depending on the situation, you may get a lot of mileage out of making that <span style="font-style: italic;">private</span> method <span style="font-style: italic;">package-private</span> instead. If you&#8217;re already programming against interfaces and have a decent package layout, you likely won&#8217;t run into too many problems.

**Step 3: Write test cases**

Now that you&#8217;re able to instantiate the class and invoke it&#8217;s new package-private utility method, there&#8217;s no excuse not to write a couple of unit tests against it.

**Step 4: Updated Functionality**

Obviously there was a method to our madness and the whole reason we under took this exercise was the change the functionality of this class/method.

Depending on your approach to testing (TDD or TSA &#8211; <span style="font-style: italic;">test soon after)</span> you should now be able to update the functionality of the method and write new test cases.

**Step 5: Run Tests**

Run both the previous and new test cases to verify that you haven&#8217;t broken previous functionality and that it also supports the new capabilities you just finished adding.

All in all, I&#8217;ve seen this work quite successfully. With a little discipline, there&#8217;s no reason why we can&#8217;t get more of the code we&#8217;re writing under test. Of course this isn&#8217;t a replacement for interface-level testing nor a reason to throw the private modifier out the window, but rather another idea to keep in the back of your mind as your bug fixing or making minor feature changes.

 [1]: http://www.amazon.com/Working-Effectively-Legacy-Robert-Martin/dp/0131177052