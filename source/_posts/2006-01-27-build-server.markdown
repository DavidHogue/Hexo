---
author: David Hogue
comments: false
date: 2006-01-27 06:43:21+00:00
layout: post
slug: build-server
title: Build Server
wordpress_id: 331
categories:
- Software Development
tags:
- old-blog
---

I finally got around to setting up a build server here for a couple of our larger projects.  I am using CruiseControl.net as the build server and NAnt to build everything.  Both of these projects had NAnt scripts already (though I have expanded them to include unit tests and some deployment type tasks).  All the source is in Subversion.

It's really pretty neat.  The CruiseControl.net service checks Subversion once a minute.  Every time a change is committed to the trunk it updates to the change and runs the NAnt script.  The script cleans up from the last build, compiles everything, copies files to where they go, and runs what unit tests there are.  It then notifies us if the build was successful or not.

So far no one has broken a build.  I am being a little more careful to double check what I am committing simply so I don't get called on for breaking something again.  (I did break something today, but it wasn't source code related.)

One of the projects has Selenium tests in addition to some light NUnit tests.  Selenium is a test framework for web apps and it all runs in javascript.  During the build process a NAnt task starts Firefox and runs the tests.  If the tests fail the build fails.  One thing that I had a little trouble with was getting the service to start a browser properly when no one is logged on to the server.  Right now I have to login and then logout after rebooting or Firefox never starts up.

There's a couple things I would still like it to do that I haven't got around to yet.  For one, it'd be cool if it zipped up the whole output and put the zip out on some nightly download area type place (with the subversion revision in the filename).  It should probably also archive the old zip files.  Another thing is that both the projects are currently .net 1.1.  When we move to 2.0 I have to figure out how to get NAnt to build to 2.0 or switch to MSBuild or something.



#### Links to tools






  * [CruiseControl.NET](http://confluence.public.thoughtworks.org/display/CCNET/Welcome+to+CruiseControl.NET) - build server


  * [Subversion](http://subversion.tigris.org/) - source control


  * [Selenium](http://nant.sourceforge.net/>NAnt - build scripts</li>
<li><a href=) - test tool for web applications


  * [NUnit](http://www.nunit.org/) - unit testing in .net


  * [MSBuild](http://blogs.msdn.com/msbuild/) - Microsoft's answer to NAnt (couldn't find an official site, this it the MSBuild team's blog)


