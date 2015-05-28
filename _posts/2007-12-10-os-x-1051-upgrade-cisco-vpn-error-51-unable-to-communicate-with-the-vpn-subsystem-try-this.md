---
title: 'OS X 10.5.1 Upgrade + Cisco VPN + &#8216;Error 51: Unable to communicate with the VPN subsystem&#8217; ?  Try this.'
author: ajordens
layout: post
permalink: /2007/12/os-x-1051-upgrade-cisco-vpn-error-51-unable-to-communicate-with-the-vpn-subsystem-try-this/
categories:
  - citations
---
If you&#8217;ve recently upgraded to OS X 10.5.1 and noticed your Cisco VPN client reporting a friendly &#8216;*Error 51: Unable to communicate with the VPN subsystem*&#8216; error, you&#8217;ll need to do the following.

> sudo /System/Library/StartupItems/CiscoVPN/CiscoVPN restart 

Essentially the Cisco VPN extension just needs to be restarted.

Thanks to [Anders Brownworth][1] for this tip.

 [1]: http://www.anders.com/cms/192/CiscoVPN/Error.51:.Unable.to.communicate.with