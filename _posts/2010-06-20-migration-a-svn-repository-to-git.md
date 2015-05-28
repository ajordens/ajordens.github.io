---
title: Migrating a SVN Repository to GIT
author: ajordens
layout: post
permalink: /2010/06/migration-a-svn-repository-to-git/
categories:
  - General Discussions
  - Open Source Software
---
Yesterday I took on the task of migrating a remote SVN repository to GIT.&#160; 

I recently bought a small cloud server from Rackspace with the goal of amalgamating various services I had hosted previously at Webfaction.

The SVN –> GIT migration was simple and painless (thanks to [Jon Maddox][1] for the reference instructions).&#160; Importantly, all the commit history from Subversion was maintained.

&#160;

Create a new *git* user:

> <font color="#444444" face="Verdana">adduser git</font>

&#160;

As the *git* user

> <font color="#444444" face="Verdana">mkdir repos</font>
> 
> <font color="#444444" face="Verdana">cd repos</font>
> 
> <font color="#444444" face="Verdana">mkdir trunk_tmp</font>
> 
> <font color="#444444" face="Verdana">cd trunk_tmp</font>
> 
> <font color="#444444" face="Verdana">git-svn init <a href="http://x.y.z/svn/trunk">http://x.y.z/svn/trunk</a> –no-metadata</font>
> 
> <font color="#444444" face="Verdana">git config svn.authorsfile ~/repos/users.txt</font>
> 
> <font color="#444444" face="Verdana">git-svn fetch</font>
> 
> &#160;

The *users.txt *should contain a mapping of svn to git users in the following format:

> <font color="#444444" face="Verdana">svnusername = My Full Name <my email address></font>

&#160;

After the *git-svn fetch* operation has completed (it will download all revisions from subversion and may take a while), do the following: 

> <font color="#444444" face="Verdana">git clone trunk_tmp trunk</font>
> 
> <font color="#444444" face="Verdana">rm –rf trunk_tmp</font>

**

*~git/repos/trunk* is the new home of your GIT repository.

&#160;

To access it remotely (*over ssh*):

> <font color="#444444" face="Verdana">git clone ssh://git@<host>/~git/repos/trunk</font>

&#160;

Simple as that.&#160; I’m the only one using the repository so tunnelling it over a single user account is satisfactory.&#160; I’d recommend setting up ssh private/public keys to make authentication more seamless.

&#160;

**Resource**

  * <http://git.or.cz/course/svn.html> – Provides a reasonable mapping of SVN –> GIT commands. 
  * <http://www.jonmaddox.com/2008/03/05/cleanly-migrate-your-subversion-repository-to-a-git-repository/> – More detailed instructions on the repository migration.

 [1]: http://www.jonmaddox.com/2008/03/05/cleanly-migrate-your-subversion-repository-to-a-git-repository/