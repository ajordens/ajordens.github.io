---
title: Re-signing a JAR with Bash
author: ajordens
layout: post
permalink: /2007/04/re-signing-a-jar-with-bash/
categories:
  - General Discussions
---
As mentioned previously, we had a little problem at work with a certificate that prompted us to un-sign and re-sign a significant number of jars.

We didn&#8217;t have *ant* available in all production deployments so my co-workers [ant macro][1] was unfortunately not appropriate. If you&#8217;re in a situation where *ant* is available, do check it out.

About the only thing we did have was *bash* and the *JDK/JRE*. It doesn&#8217;t look like the JDK provides any tools to automate the un-signing process , so we resorted to uncompressing and removing all signatures contained within the META-INF directory.

The only kicker resulted from a jar file (*jh.jar from JavaHelp*) that contained the same resource in the same package multiple times but with different capitalizations (ie. Foo.gif and foo.gif). When uncompressing on a Windows machine, you&#8217;ll loose one of the versions due to NTFS being case-insensitive. This caused a bit of grief and we ended up settling on manually signing a fresh copy of the jar that wasn&#8217;t previously signed.

Here&#8217;s a snippet of what we hacked together (poorly formatted on the web):

> #!/bin/bash

> for i in \`find . -name &#8216;*.jar&#8217;\`; do  
> tmp\_file=tmp\_$$
> 
> \# Un-sign jar  
> mkdir $tmp_file  
> cd $tmp_file
> 
> echo &#8220;Scrubbing $i&#8221;  
> jar -xf ../$i  
> if [ -e META-INF ]; then  
> if [ -e META-INF/\*.SF ]; then rm -f META-INF/\*.SF; fi  
> if [ -e META-INF/\*.DSA ]; then rm -f META-INF/\*.DSA; fi  
> if [ -e META-INF/\*.RSA ]; then rm -f META-INF/\*.RSA; fi  
> fi
> 
> echo &#8220;Packaging $i&#8221;  
> jar cfM ../$i .  
> cd ..
> 
> echo &#8220;Signing $i&#8221;  
> jarsigner -keystore [keystore] -storepass [password] $i [alias]
> 
> rm -rf $tmp_file  
> echo &#8220;&#8221;  
> done

Unlike the ant macro, this script won&#8217;t necessarly create a META-INF if it didn&#8217;t exist previously. If that causes you grief, you&#8217;ll want to add a *mkdir META-INF ; touch META-INF/MANIFEST.MF* prior to the *Packaging* stage.

 [1]: http://frank.neatstep.com/node/29?PHPSESSID=fbfa811070fde8b64b231eca49986ce5