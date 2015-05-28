---
title: 'GluonJ Test Drive : Simple AOP'
author: ajordens
layout: post
permalink: /2008/02/gluonj-test-drive-simple-aop/
categories:
  - General Discussions
  - Java
  - Open Source Software
---
I admitedly don&#8217;t have a lot of experience with the various AOP frameworks that have gained popularity over the past few years.

I happened to be looking at [Javassist][1] a couple weeks back and noticed that they were in the process of developing a lightweight AOP framework on top of it called [GluonJ][2]. It&#8217;s still in fairly active development with a 1.5b being released last November.

I naively set out to solve what I thought was a pretty simple problem, track statistics about object serializations. Essentially I wanted to build something similar to [JDBCSpy][3] that tracked and exposed basic serialization information over JMX. Initially I&#8217;m thinking basic things like # of serialized objects and # of bytes serialized. I spend my days working on a client/server application and this type of information would be useful, if done in a transparent and non-intrusive way.

**Caveat** &#8211; There might be (and probably are) better ways to accomplish this, I&#8217;m not dead set on using the AOP hammer to solve this problem but it does present a nice excuse to try it out.

**Attempt #1**

My first attempt was to refine the definition of java.lang.Object and insert advice around writeObject().

This unfortunately didn&#8217;t make it very far as it doesn&#8217;t look like GluonJ allows you to mess with Object. You can refine any other class (<span style="font-style: italic;">even the final ones</span>) but there&#8217;s no love for <span style="font-style: italic;">java.lang.Object</span>.

**Attempt #2**

Second attempt was a bit more selective. I choose an object to monitor serializations for and went about trying to apply advice to its writeObject().

Unfortunately, I didn&#8217;t have much success in being able to apply any sort of advice (@Before, @After, @Around) to a private method. In hindsight, it would have been less then ideal anyways as most <span style="font-style: italic;">Serializable</span> objects don&#8217;t implement their own writeObject() anyways.

**Attempt #3**

After a couple dead ends I decided to approach to problem from a slightly different angle. Rather than focusing on modifying the behaviour of the object being serialized, why not change the behaviour of the object actually responsible for performing the serialization. In this trivial example, that object was the ObjectOutputStream.

It worked and didn&#8217;t require very much code at all.

> **<span style="text-decoration: underline;">The Glue Code</span>**  
> <span style="font-style: italic;">This doesn&#8217;t really do much other than instruct the runtime that whenever ObjectOutputStream.writeObject() is invoked, we want to do a System.out.println() afterwards. Pretty simple right?</span>
> 
> <pre>@Glue
public class SerializationGlue
{
    /**
     * @param obj Object
     * @return Number of bytes in the serialized form of 'obj'
     */
    public static long calculateSize(Object obj)
    {
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        try
        {
            ObjectOutputStream out = new ObjectOutputStream(baos);
            out.writeObject(obj);
        }
        catch (Exception e)
        {
            e.printStackTrace();
            return -1;
        }

        return baos.size();
    }

    @After("{ System.out.println(`obj size=` + org.jordens.jdbcspy.testutil.gluonj.SerializationGlue.calculateSize(object)); }")
    Pointcut pc1 = Pcd.define("object", "$1")
                      .define("target", "$0")
                      .call("java.io.ObjectOutputStream#writeObject(Object)");
}
</pre>
> 
> **<span style="text-decoration: underline;">The Test Code</span>**
> 
> <pre>public class Runner
{
    public static void main(String[] args)
    {
        List&lt;Long&gt; values = new ArrayList&lt;Long&gt;()
        {
            public String toString()
            {
                return "List&lt;Long&gt;[" + size() + "]";
            }
        };
        
        for (long i=0; i&lt;100000; i++)
        {
            values.add(i);
        }

        try
        {
            ByteArrayOutputStream baos = new ByteArrayOutputStream();
            ObjectOutputStream out = new ObjectOutputStream(baos);
            out.writeObject(values);
        }
        catch (Exception e)
        {
            e.printStackTrace();
        }
    }
}
</pre>
> 
> <span style="font-weight: bold; text-decoration: underline;">How do I run this?</span>  
> java -javaagent:gluonj-1.5b.jar=org.jordens.jdbcspy.testutil.gluonj.SerializationGlue -classpath classes/ org.jordens.jdbcspy.testutil.gluonj.Runner
> 
> <span style="font-style: italic;">would print:</span>  
> obj size=1400181
> 
> Nothing too crazy there. One niceity in all of this is the relative ease in which you can enable/disable the runtime code weaving. Just leave off the -javaagent:XXX and you&#8217;re effectively back to normal.

**Conclusions**

GluonJ looks pretty cool but obviously it&#8217;s still fairly new and lacks many of the capabilities available in a more mature offering like AspectJ. That being said, the documentation is pretty good and the learning curve was basically non-existent. If you&#8217;re looking for something to play around with, it&#8217;s probably a bit easier to get started with.

The possibilities are certainly encouraging and I&#8217;ll definitely be keeping an eye on the progress of GluonJ as well as taking a more hands-on look at AspectJ.

 [1]: http://www.csg.is.titech.ac.jp/~chiba/javassist/
 [2]: http://www.csg.is.titech.ac.jp/projects/gluonj/
 [3]: http://code.google.com/p/jordens-jdbcspy/