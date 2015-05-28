---
title: 'Upgraded to Leopard : Making use of /etc/paths.d and path_helper'
author: ajordens
layout: post
permalink: /2008/01/upgraded-to-leopard-making-use-of-etcpathsd-and-path_helper/
categories:
  - citations
---
In Leopard, Apple has introduced a new mechanism for managing and maintaining your system path ($PATH).

Previously (and in most current Linux environments) paths were managed by updating the PATH environment variable directly in either the system profile (<span style="font-style: italic;">/etc/profile</span>) or your local profile (<span style="font-style: italic;">~/.bash_profile</span>).

Commonly you had entries like:

> <pre>export JAVA_HOME = /usr/lib/j2se/jdk1.5.0_13/
  export PATH=$PATH:$JAVA_HOME/bin
  ...
  
</pre>

In Leopard, you no longer have to modify the profile to make adjustments to system paths. Instead, you can put a simple text file containing a path entry (<span style="font-style: italic;">or entries</span>) into <span style="font-style: italic;">/etc/paths.d/</span>.

Each line in this file will be interpreted as a path and added automatically to the system path.

> <pre>macos-gls000120:~ ajordens$ ls -al /etc/paths.d/
total 40
drwxr-xr-x    7 root  wheel   238 Jan 22 18:51 .
drwxr-xr-x  105 root  wheel  3570 Jan 23 11:59 ..
-rw-r--r--    1 root  wheel    13 Sep 23 20:53 X11
-rw-r--r--    1 root  wheel    16 Jan 22 18:58 groovy
-rw-r--r--    1 root  wheel    15 Jan 22 18:58 maven
-rw-r--r--    1 root  wheel    20 Jan 22 18:58 postgresql
-rw-r--r--    1 root  wheel    15 Jan 22 18:58 scala

macos-gls000120:~ ajordens$ cat /etc/paths.d/scala 
$SCALA_HOME/bin
</pre>

It&#8217;s up to you whether you include an environment variable or specify the full path.

**Enter Leopard**

In order to take advantage of this new feature, your <span style="font-style: italic;">/etc/profile</span> needs to invoke <span style="font-style: italic;">/usr/libexec/path_helper.</span> Depending on your upgrade path to Leopard, your profile may or may not have been automatically updated.

Unfortunately mine wasn&#8217;t and I couldn&#8217;t find a definitive post telling what changes I had to make to the profile. I decided to write the procedure up so that anyone else wanting to take advantage of <span style="font-style: italic;">paths.d</span> and <span style="font-style: italic;">path<span style="font-style: normal;"><span style="font-style: italic;">_helper</span> could do so.</span></span>

> <pre>macos-gls000120:~ ajordens$ cat /etc/profile
# System-wide .profile for sh(1)

if [ "${BASH-no}" != "no" ]; then
        [ -r /etc/bashrc ] && . /etc/bashrc
fi

export ANT_OPTS="-Xmx256M"

export POSTGRESQL_HOME="/opt/local/lib/postgresql82"
export CONFBASE=/usr/local/src/confluence-2.6.2
export HADOOP_HOME=/usr/local/src/hadoop-0.15.2

export GROOVY_HOME=/usr/local/src/groovy-1.5.1
export SCALA_HOME=/usr/local/src/scala-2.6.0-final
export MAVEN_HOME=/usr/local/src/maven-2.0.7

export JAVA_HOME="/System/Library/Frameworks/JavaVM.framework/Versions/1.5.0/Home/"

if [ -x /usr/libexec/path_helper ]; then
       eval `/usr/libexec/path_helper -s`
fi
</pre>

That&#8217;s basically it. I put the <span style="font-style: italic;">path_helper</span> invocation at the end of the profile because I wanted to be able to substitute environment variables.