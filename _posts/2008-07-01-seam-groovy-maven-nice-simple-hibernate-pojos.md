---
title: 'Seam + Groovy + Maven : Nice Simple Hibernate POJOs'
author: ajordens
layout: post
permalink: /2008/07/seam-groovy-maven-nice-simple-hibernate-pojos/
categories:
  - General Discussions
  - Java
---
Being a long weekend, I had a couple hours yesterday to mess around with my *Maven* build in the hopes of integrating *Groovy* and ridding myself of a lot of *Hibernate* boilerplate (*you know, all the annoying getters/setters*).

I&#8217;m currently working on a *Seam-based* prototype and *Groovy* is certainly applicable to aspects other than *Hibernate* but it was a good initial goal.

**Required POM Changes**

<pre>&lt;build&gt;
&lt;plugins&gt;
    &lt;plugin&gt;
        &lt;groupId&gt;org.codehaus.groovy.maven&lt;/groupId&gt;
        &lt;artifactId&gt;gmaven-plugin&lt;/artifactId&gt;
        &lt;version&gt;1.0-rc-2&lt;/version&gt;
        &lt;executions&gt;
            &lt;execution&gt;
                &lt;goals&gt;
                    &lt;goal&gt;generateStubs&lt;/goal&gt;
                    &lt;goal&gt;compile&lt;/goal&gt;
                    &lt;goal&gt;generateTestStubs&lt;/goal&gt;
                    &lt;goal&gt;testCompile&lt;/goal&gt;
                &lt;/goals&gt;
            &lt;/execution&gt;
        &lt;/executions&gt;
    &lt;/plugin&gt;
&lt;/plugins&gt;
&lt;/build&gt;
</pre>

***The gmaven plugin is able to cross-compile Java and Groovy. The compilation phase will generate Java stubs corresponding to the groovy classes prior to compiling the actual Java classes. This allows for seamless dependencies to exist between Groovy and Java.***

***It&#8217;s important to note that your Groovy sources must (by default) be in a <span style="text-decoration: underline;">src/main/groovy</span> folder.***

<pre>&lt;dependencies&gt;
    &lt;dependency&gt;
        &lt;groupId&gt;org.codehaus.groovy.maven.runtime&lt;/groupId&gt;
        &lt;artifactId&gt;gmaven-runtime-default&lt;/artifactId&gt;
        &lt;version&gt;1.0-rc-2&lt;/version&gt;
    &lt;/dependency&gt;
&lt;/dependencies&gt;
</pre>

**Results**

Simple as that. *Unit tests passed!*

I&#8217;m able to take a class that looked like:

<pre>@Entity
public class Annotation
{
    private Long id;
    private String name;<br /><br />    private Specimen specimen;
    private Patient patient;<br /><br />    /**
     * Getter for property 'id'.
     *
     * @return Value for property 'id'.
     */
    @Id @GeneratedValue
    public Long getId()
    {
        return id;
    }<br /><br />    /**
     * Setter for property 'id'.
     *
     * @param id Value to set for property 'id'.
     */
    public void setId(Long id)
    {
        this.id = id;
    }
...
}
</pre>

and make it look like:

<pre>@Entity
public class Annotation
{
    @Id @GeneratedValue
    Long id;<br /><br />    @Length(max=50) @NotNull
    String name;<br /><br />    @ManyToOne @JoinColumn(name = "specimen_id")
    Specimen specimen;<br /><br />    @ManyToOne @JoinColumn(name = "patient_id")
    Patient patient;
}
</pre>

Much simpler and without a lot of unnecessary boilerplate.

**Gotchas**

Just a couple of things to be aware of. Simple stuff really if you actually read documentation and know what you&#8217;re doing <img src="http://littlesquare.com/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

Firstly, Groovy sources have to live in *src/main/groovy*.

Secondly, don&#8217;t add private modifiers to your attributes if you want the generated Groovy stubs to include getters/setters. This is probably more obvious if you&#8217;re creating your Groovy classes from scratch. I forgot to remove them when I was converting from a Java POJO and had a minor WTF moment.

Next step will be to see how much Groovy could potentially be leveraged for other aspects of the system.