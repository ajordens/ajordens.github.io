---
title: 'The Upgrade to Leopard &#8211; Relatively Painless'
author: ajordens
layout: post
permalink: /2007/10/the-upgrade-to-leopard-relatively-painless/
categories:
  - General Discussions
---
Last night I decided it was time to take the plunge and upgrade my MacBook Pro to Leopard.

All in all, the upgrade was fairly smooth and required no intervention from me after it was started.  There were a couple of gotchas I discovered after attempting to use the upgraded system which I&#8217;ll discuss in a bit more detail below.  

*Gotchas*

  * When I first booted into Leopard, I noticed that my account no longer had admin rights. 
  * Web Sharing (previously enabled) had been disabled.
  * A Leopard-enabled release of MailTags is not yet available.

The lack of an admin user was a slight inconvienence.  The fix required booting into single-user mode and adding my current user to the sudoers file and then using *dscl* to add the user to the admin group. 

Web Sharing was easy to fix by re-enabling it in the System Preferences.

The MailTags forums say that a beta release supporting Leopard should be available early next week.

Given that this laptop is also my development machine at work I was happy to see all of my tools still functioning.  I recently migrated to using MacPorts-built versions of PostgreSQL and Subversion, they&#8217;re still working with no re-compilation necessary.

The changes to Mail.app look nice and I&#8217;ll be looking forward to seeing if they&#8217;ve eased any of my Exchange-related burdens.

I&#8217;m also keen on seeing how well the Spaces implementation works.  I was using VirtueDesktops for sometime but ultimately got frustrated with some of the focus issues with applications across desktops.

Overall things look nice.  I&#8217;ve never been much of a Safari user but the improvements around search and inline PDF viewing are a nice touch.  Firefox could really learn something here.

That&#8217;s it for now, a generally positive upgrade experience but we&#8217;ll see how the next few weeks work out.

<p style="color:#008;text-align:right;">