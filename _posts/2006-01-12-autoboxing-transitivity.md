---
title: 'Autoboxing &#038; Transitivity'
author: ajordens
layout: post
permalink: /2006/01/autoboxing-transitivity/
categories:
  - General Discussions
---
This has been written about by [others][1] but I&#8217;m going to comment on it as I did run into it tonight.

I&#8217;ll start by saying that I sit on the fence with regards to the use of autoboxing in java5. Normally I think it&#8217;s alright but I did run into a situation this evening where the transitivity properties of equality didn&#8217;t hold as I expected (well I expected them to behave as they did, but it did run slightly counter to the definition of transitivity depending on how the code was written).

**Code:**  
`<br />
public class Test {</p>
<p>public static void main(String[] args)<br />
{<br />
  Long int1 = new Long(1);<br />
  long int2 = new Long(1);<br />
  Long int3 = new Long(1);</p>
<p>  System.out.println(int1 == int2);<br />
  System.out.println(int2 == int3);<br />
  System.out.println(int1 == int3);<br />
}</p>
<p>}`  
**Output:**  
`<br />
true<br />
true<br />
false<br />
`

However, if we swap 1L in for &#8216;new Long(1)&#8217;, than transitivity holds and A == B &#038;&#038; B == C &#038;&#038; A == C.

Nothing more than food for thought. 

It&#8217;s almost too easy to unconsciously make use of autoboxing so we should weigh the benefits of simplicity with the potential for some unexpected results.

 [1]: http://blogs.sun.com/roller/page/mary?entry=friday_free_stuff_a_puzzler