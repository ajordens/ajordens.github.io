---
title: 'Combining Heroku and Dropwizard: My Own Personal Staging Environment'
author: ajordens
layout: post
permalink: /2013/01/combining-heroku-and-dropwizard-my-own-personal-staging-environment/
categories:
  - General Discussions
---
<!--?xml version="1.0" encoding="UTF-8" standalone="no"?-->

<div style="font-family: Arial;">
  <!--?xml version="1.0" encoding="UTF-8" standalone="no"?--></p> 
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Think what you may about Heroku, they do offer a <strong>free tier</strong> and it&#8217;s trivially simple to use it as your own personal staging environment. In this post, I&#8217;m going to outline what it takes to take a simple Dropwizard service and get it running in Heroku. For anyone looking for a bit of depth, this example will also include database access (<em>Heroku also gives you a free PostgreSQL database</em>)<em> </em>and touch on using Dropwizard&#8217;s Liquibase integration for database migrations.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">For the record, I am not particularly for nor against Heroku as a platform. I believe it&#8217;s a great service that makes it almost too easy to get off the ground and into the continuous deployment frame of mind. I simply lack the experience using it at scale, opting instead for AWS, to comment on it&#8217;s applicability across all stages of an application. </span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Maybe I&#8217;m cheap (<em>Heroku&#8217;s a few more dollars than the equivalent in AWS</em>) or maybe I just really <strong>really </strong>enjoy (<em>the pain of?</em>) managing Chef and setting up my own VPCs.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;">Getting Started</strong>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">First off, let&#8217;s get a simple Dropwizard project up and running. </span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ git clone git://github.com/ajordens/dropwizard-example-groovy.git</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Make sure it compiles and runs locally.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ mvn clean install</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ java -jar my-example-service/target/my-example-service-0.1-SNAPSHOT.jar server my-example-service/config.yml</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Lastly, create a simple PostgreSQL database and test database migrations.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ createdb myexampleDB</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ java -jar my-example-service/target/my-example-service-0.1-SNAPSHOT.jar db migrate my-example-service/config.yml</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Assuming everything worked successfully, you&#8217;ll now have a service capable of serving html views and json data as well as a simple database.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;"><br /></strong>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;">Setting up Heroku</strong>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;"><br /></strong>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">If you have not already signed up for a free Heroku account, do so now. </span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">You will also need to install the appropriate <a href="https://toolbelt.heroku.com/">Heroku Toolbelt</a> release for your operating system.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ heroku login</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    Enter your Heroku credentials.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    Email: example-app@xyz</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    Password (typing will be hidden): </span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    Authentication successful.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ heroku create example-app</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    Creating example-app&#8230; done, stack is cedar</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    http://example-app.herokuapp.com/ | git@heroku.com:example-app.git</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    Git remote heroku added<br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Almost done, all that&#8217;s left now is to get the Heroku database connection properties. </span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Update <em style="font-weight: bold;">config-heroku.yml</em> with the values listed in the PostgreSQL add-on section of your application (<em>login to heroku.com</em>)</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;">Pushing Code to Heroku</strong>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;"><br /></strong>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><strong>    </strong>$ git push heroku master</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ heroku ps:scale web=1</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">After pushing code to Heroku, it&#8217;s completely normal to see your maven build occur immediately. </span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">When the build finishes, the app will be accessible via http://<strong>app-name</strong>.herokuapp.com</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ heroku open</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">This works in part due to the magical <strong>Procfile</strong> that I snuck into the <em>dropwizard-example-groovy</em> project.  </span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">The Procfile simply tells Heroku how to start the web application and because Dropwizard is a completely self-contained jar, it runs in Heroku using the same <strong style="font-style: italic;">java -jar </strong>syntax that you would use to run locally.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <em style="font-size: 14px;">Almost magical.</em>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;">Migrating Databases on Heroku</strong>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;"><br /></strong>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Managing your Heroku databases is almost as simple as if they were running locally.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ java -jar my-example-service/target/my-example-service-0.1-SNAPSHOT.jar db migrate my-example-service/config-heroku.yml</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Want to drop everything.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ java -jar my-example-service/target/my-example-service-0.1-SNAPSHOT.jar db drop-all &#8211;confirm-delete-everything my-example-service/config-heroku.yml </span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;">Using Git Flow?</strong>
  </div>
  
  <div style="font-family: Arial;">
    <strong style="font-size: 14px;"><br /></strong>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">If you&#8217;re accustomed to using git-flow, you will frequently want to push feature branches to Heroku.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">It&#8217;s simple.</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">    $ git push heroku feature/BRANCH_NAME:master</span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">This will allow you to test and deploy a non-master branch in your staging environment.  </span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;"><br /></span>
  </div>
  
  <div style="font-family: Arial;">
    <span style="font-size: 14px;">Have further questions?  I&#8217;ve been running Dropwizard apps in Heroku for awhile now, <a href="http://twitter.com/ajordens">ping me via Twitter</a>.</span>
  </div>
</div>