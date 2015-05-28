---
title: 'Pet Peeve:  Don&#8217;t email my password to me in plain text'
author: ajordens
layout: post
permalink: /2008/06/pet-peeve-dont-email-my-password-to-me-in-plain-text/
categories:
  - citations
---
You know the drill.

  1. Signup for some random service on the internet
  2. Receive a confirmation email with your account information

or

  1. Forget a password for some random service on the internet
  2. Receive an email with your current password

In today&#8217;s day and age, I&#8217;m not aware of any good reason why we (*the services*) should be transmitting user credentials (*namely their passwords*) in an email. The [HBC Run For Canada][1] site was the latest example I ran into. If I go to the bank and tell them I&#8217;ve forgotten my PIN, are they going to verify my identity and just tell me my old pin or require me to specify a new pin? I suspect the later.

Bearing in mind that I&#8217;m slightly more technical than most people but I don&#8217;t expect any service to store my password in plain text let alone be able to provide it to me on-demand.

We&#8217;ve already got infrastructure for single-use *reset password* URLs, *hints*, etc. so let&#8217;s use them uniformly. Nothings perfect but depending on your particular audience, something like [OpenID][2] could very well be a nice solution to end-user authentication.

 [1]: http://www.hbcrunforcanada.ca/2008/index.php
 [2]: http://openid.net