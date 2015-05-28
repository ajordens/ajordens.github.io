---
title: 'Django/Python + LinkedIn JSAPI <> oAuth Tokens'
author: ajordens
layout: post
permalink: /2012/02/python-linkedin-jsapi-tokens/
categories:
  - General Discussions
---
This past week I spent a little time working with LinkedIn&#8217;s JavaScript APIs.

The APIs themselves are quite powerful and easy to work with.  Complications arose when it came time to convert the temporary JSAPI tokens to their oAuth equivalents.

<https://developer.linkedin.com/documents/exchange-jsapi-tokens-rest-api-oauth-tokens>

First things first, LinkedIn only passes the JS API oAuth 2.0 token over an SSL connection.  Slighly annoying from a development perspective, as I wasn&#8217;t normally running SSL on my local Mac. That being said, getting nginx setup through homebrew was straight forward. It works fine with a self-signed certificate as well.

**Once you have SSL setup**

<pre>&lt;script type="IN/Login" data-onAuth="onAuth" data-onLogout="onLogout"&gt;&lt;/script&gt;<br /></pre>

<pre>function onAuth() {            </pre>

<pre><span style="white-space: pre;">	</span>$.post("https://" + window.location.hostname + "/my-app/token-exchange");</pre>

<pre>}</pre>

**After a successful LinkedIn authentication, the onAuth() function will be invoked and a POST made to your backend resource over SSL.**

<pre><span style="font-size: 13px;">def token_exchange(request):</span></pre>

<pre><span style="font-size: 13px;"> </span><span style="font-size: 13px;">oauth_token = None</span><br /><span style="font-size: 13px;"> </span><span style="font-size: 13px;">oauth_secret = None</span></pre>

<pre><span style="font-size: 13px;"> if request.session.get('linkedin_oauth_token'):        </span></pre>

<pre><span style="font-size: 13px;"><span style="white-space: pre;">	</span>oauth_token = request.session.get('linkedin_oauth_token')        </span></pre>

<pre><span style="font-size: 13px;"><span style="white-space: pre;">	</span>oauth_secret = request.session.get('linkedin_oauth_secret')    </span></pre>

<pre><span style="font-size: 13px;"> else:        </span></pre>

<pre><span style="font-size: 13px;"> <span style="white-space: pre;">	</span>oauth_token = request.COOKIES.get('linkedin_oauth_%s' % settings.LINKEDIN_API_KEY)        </span></pre>

<pre><span style="font-size: 13px;"><span style="white-space: pre;">	</span>oauth_token = urllib.unquote(oauth_token)        </span></pre>

<pre><span style="font-size: 13px;"><span style="white-space: pre;">	</span>oauth_token = json.loads(oauth_token)</span></pre>

<pre><br /><span style="font-size: 13px;"> consumer_key = settings.LINKEDIN_API_KEY        </span></pre>

<pre><span style="font-size: 13px;"> consumer_secret = settings.LINKEDIN_SECRET_KEY        </span></pre>

<pre><span style="font-size: 13px;"> access_token_url = 'https://api.linkedin.com/uas/oauth/accessToken'</span></pre>

<pre><span style="font-size: 13px;"> access_token = oauth_token.get('access_token')</span><br /><span style="font-size: 13px;"> consumer = oauth2.Consumer(             </span></pre>

<pre><span style="font-size: 13px;"><span style="white-space: pre;">	</span>key=consumer_key,             </span></pre>

<pre><span style="font-size: 13px;"><span style="white-space: pre;">	</span>secret=consumer_secret</span></pre>

<pre><span style="font-size: 13px;"> )</span></pre>

<pre><span style="font-size: 13px;"> client = oauth2.Client(consumer)</span><br /><span style="font-size: 13px;"> resp, content = client.request(access_token_url, "POST", body='xoauth_oauth2_access_token=%s' % access_token)        </span></pre>

<pre><span style="font-size: 13px;"> request_token = dict(urlparse.parse_qsl(content))        </span></pre>

<pre><span style="font-size: 13px;"> oauth_secret = request_token.get('oauth_token_secret')        </span></pre>

<pre><span style="font-size: 13px;"> oauth_token = request_token.get('oauth_token')</span><br /><span style="font-size: 13px;"> request.session['linkedin_oauth_token'] = oauth_token        </span></pre>

<pre><span style="font-size: 13px;"> request.session['linkedin_oauth_secret'] = oauth_secret<span style="line-height: 0px;">﻿</span></span></pre>

 

The code snippet above is a **django view **that requires **oauth2**.

And that&#8217;s it.  You&#8217;ve now successfully converted JS API tokens to oAuth tokens in a Python/Django environment.