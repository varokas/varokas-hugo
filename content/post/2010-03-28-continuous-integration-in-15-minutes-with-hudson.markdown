---
author: varokas
comments: true
date: 2010-03-28 18:43:49+00:00
slug: continuous-integration-in-15-minutes-with-hudson
title: Continuous Integration in 15 Minutes with Hudson
wordpress_id: 113
categories:
- Software Engineering
---

My motto: If something goes wrong, I want to know it now. [Continuous Integration](http://martinfowler.com/articles/continuousIntegration.html) is always one of the most useful Agile practice I adore. It remove the phrase "But it was working on my machine .. yesterday!" out of the equation by putting a central environment that the build must run on. Most people might be more familiar with [Cruisecontrol](http://cruisecontrol.sourceforge.net/), but the lack of snappy setup and configuration for newbies is one of the big downsides it has. I was just introduced to [Hudson](http://hudson-ci.org/) recently and really likes the simplicity it offers. I recommend this to teams that start using CI, because it is really easy to set up.


### CI Basics


First, let me talk real quick about CI, to summarize its benefits and allow us to see how Hudson comes to play with that. Continuous Integrations in the wild usually follow these steps.



	
  1. One of the Developers in the team checks in code to a code repository (SVN, Mercurial, etc).

	
  2. Hudson sees that there's a new code and checks out the code in its own workspace

	
  3. Hudson run the build script (usually [Ant](http://ant.apache.org/), or the increasingly popular [Maven](http://maven.apache.org/)) that is checked in the code. The build script usually follow these steps ( I will surely blog more about this later ).

	
    1. Checking

	
    2. DB

	
    3. Generating code

	
    4. Compile

	
    5. Run automated test

	
    6. Run code analyzer tool (Static Analysis, Code Metrics , Test Coverage)

	
    7. Deploy the compiled code on test server




	
  4. Hudson gather build results and compile a report (compile pass/failed, number of test passed/failed)

	
  5. Hudson publish a report on the website, and send out (emails/rss/twitter) to the developer that breaks the build

	
  6. The developer has to take responsibility to fix the error and commit in the fix




### Installing Hudson





	
  1. Hudson is distributed a form of (.war) file. Download the latest one from their [website](https://hudson.dev.java.net/).

	
  2. Prepare any Java Servlet container. [Tomcat](http://tomcat.apache.org/download-60.cgi), would do. For windows, I suggest installing it as a service.

	
  3. Use Tomcat Manager to upload and deploy hudson.war

	
  4. Goto http://localhost:8080/hudson

	
  5. On the left menu, goto "Manage Hudson", then "Configure System". Enter email server information




### Configuring the build





	
  1. Each build project is called jobs. There's a link to create one once you browse to hudson, click on it.

	
  2. Enter the job name. Choose "Build a free-style software project**".**

	
  3. In Source code Management section, choose the one you use. Provide the path to your project source repository.

	
  4. In Build Triggers, select how often we want Hudson to grab the source code. In regular standalone projects, we usually do it every time a developer checks in code ("Poll SCM"). The parameter is a schedule in cron format. Every fifteen minutes ( */15 * * * *) should suffice for most projects. Note that this does not mean that we will build every 15 minutes, it means that Hudson will be checking for changes in the SVN every 15 minutes.

	
  5. In build section, select add build step. Choose "Invoke Ant" and provide the target name. If the build.xml is not at the root of the repository, choose "Advanced..." and provide the ant file path.

	
  6. In Post build actions, select Email notification and enter a list of everybody in your team. This will make Hudson send out an email to everybody when there's a build broken.




### Establishing Fix-the-Build Culture


This is probably the most important thing you need to do, even more important than the tool itself. This is when you get team members together. Introduce their new neighbor, the build server. Then establishing the team rule of "You break the build, you fix the build". This does not mean that the junior member will be entirely on their own when problems arise. But he needs to be responsible for grabbing the right people when something happens and everybody is accountable for their commits.

Making such rule would ensure that you would have the near-shippable quality product every day. Well... something that compiles and automatically tested at least :-).
