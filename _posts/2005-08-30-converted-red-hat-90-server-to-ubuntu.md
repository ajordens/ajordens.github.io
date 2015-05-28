---
title: Converted Red Hat 9.0 Server to Ubuntu
author: ajordens
layout: post
permalink: /2005/08/converted-red-hat-90-server-to-ubuntu/
categories:
  - General Discussions
---
So I didn&#8217;t have anything better to do this past weekend but go into the office and migrate our legacy Red Hat 9.0 fileserver to Ubuntu.

Actually, that&#8217;s not true but this past Saturday was the only time the server wouldn&#8217;t be actively used. The server is an AMD 2700+ with 1024MB&#8217;s of ram and 300GB of storage in a RAID 1 configuration. We have these pretty cool 2-drive hot-swappable RAID units that do the mirroring in hardware. They&#8217;re great when they work.

Before the upgrade, we made sure that we had backups. No problem.

We start Saturday off by removing the two active drives in the system and inserting a brand new single drive to do the installation on. Fine. We reboot twice because we weren&#8217;t auto-booting of the Ubuntu cd. We get halfway through the drive partitioning, and the machine locks up. Reboot.

Following the second reboot, the machine&#8217;s bios reports the 300GB drive as a 40GB drive. Weird. Luckily we had another couple drives so we tried the process again. The guy helping me is far more experienced with Windows and thought it might have been the partitioning process. So we load up Partition Magic and have a go at it on Windows. No go, on the next boot, the **second** 300GB drive reported at 40GB.

Now things are getting a bit concerning. We&#8217;ve called the vendor and he hasn&#8217;t seen this before but promised to scratch his head and get back to us. We decide to swap out the RAID unit but not before giving it another attempt. Third time&#8217;s a charm.

The actual installation and data migration was far more straight forward. I installed and configured nis, cvs, samba, nfs, zope/plone, postfix, mysql, postgresql and bind on the new server. There was little in the way of compatibility conflicts.

Red Hat 9.0 starts their user-level userid&#8217;s at 500 whereas Ubuntu starts at 1000. This required a modification to nis so that it would export users > 500 and not the default > 1000. Plone required a little bit of manual configuration because the debian packages only setup the Zope instance. Samba defaulted to using the passdb.tbl file but that was simple enough to switch back to using the traditional smbpasswd file. DNS was also easier than I expected to setup. The previous administrator (a few years back) had used the Red Hat GUI tools to manage the DNS which resulted in a few wacky zone files. I basically just junked anything extraneous and copying over only our internal zone. No one has complained yet so I don&#8217;t think I missed any important hosts. Other than those few issues, the biggest hurdle was copying a couple hundred gigabytes of data over a usb 2.0 connection from our backup system to the new server.

I definitely recommend Ubuntu (they have a server version that installs sans-X). I&#8217;ve been a Debian user for quite a few years now and swear by it.