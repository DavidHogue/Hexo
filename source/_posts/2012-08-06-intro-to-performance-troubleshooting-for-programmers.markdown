---
author: David Hogue
comments: true
date: 2012-08-06 23:01:39+00:00
layout: post
slug: intro-to-performance-troubleshooting-for-programmers
title: Intro to performance troubleshooting for programmers
wordpress_id: 1099
categories:
- Software Development
tags:
- debugging
- performance
---

Performance is something that I've spent some time with and I find quite interesting. Troubleshooting slow code seems like a straightforward process to me, but I find many times I get ahead of myself and confuse other developers. Sometimes they aren't aware of the many tricks and tools available to make their code faster. I figured I'd write up some introductory material.




### Your code needs to actually be slow to do this



Maybe your code is already fast enough. Maybe it doesn't make much difference to you if a page takes one or two seconds to render, or maybe you only have a few hundred rows in that database table. If that's the case don't worry about it. Trying to make code fast without knowing where it will slow down can make it ugly and difficult to maintain.



### Once you do have a problem, the first step is to determine where it is


![](http://davidhogue.com/wp-uploads/2012/08/screenNet-timeline.png)
You can't start troubleshooting slowness without first having at least a general idea of where the bottleneck is. That's a common thread I'll probably mention a few more times, but to start with try to figure out if you're getting hung up at the UI end, the DB end, or somewhere in the middle.

Sometimes this is as easy as watching your code run. Other times you need some tools. If your code powers a web page, open up Firebug (or your browser's equivalent) and look for where the time is spent.

If you have a database, see if you have any tracing or profiling tools. For SQL Server: SQL Profiler is useful.



### If your database is slow



I'm not going to go into much depth here, there are many sources that can give you pages and pages of pointers. However, there are a few easy things to check for: 1) Open up Windows Task Manager and see if the CPU or RAM are maxed out 2) Look at the tables being queries, are they huge? Do they have indexes?

If Task Manager doesn't give you enough details, there's always [Performance Monitor](http://davidhogue.com/blog/2011/12/performance-monitor-tips-tricks/). Or the modern SQL Server Management Studio has it's own Activity Monitor, there should be a button on the toolbar.

Try running the queries directly against the database, instead of through your code. Are they still slow? Great, start tweaking the query or the table until it gets better. Do this on a backup copy of the data and not your live production data!



### If your code is slow


It may be that you get the data quickly, but then for some reason the code to process that data is slow. There are usually only a few bottlenecks, and it usually comes down to a single piece of code that runs over and over hundreds or thousands of times.

I like to start with the IDE's debugger. Just start up the code and step over the lines one by one. You can usually "feel" when one of them is taking significantly longer. If that happens, restart the process, but this time step into that function. Eventually that should lead you to the problem.

If attaching a debugger isn't an option, logging or print statements with a basic timer can do the trick.

When neither of those tricks works, it's time to look for more specialized tools. There are code profilers out there that will tell you exactly how many milliseconds are spent on each line of code. On the downside they are almost as intrusive as attaching a debugger, so don't use them in production. I like dotTrace, but there are others out there for most environments.



### Wrapping up


So I don't know how helpful this will be to those of you that read this. For me performance issues have always been a matter of identifying the problem, and then applying a fix. Often the identification process is where I spend the most time (just like fixing a bug really.) Sometimes developers want to jump straight to a solution, but you can't do that without more information. The whole thing is often a process of elimination. Once you have a small piece of the app to focus on, and you can ignore everything else, it becomes much easer to come up with ideas to fix it.

As Sherlock says: "'Data! Data! Data!' he cried impatiently. 'I can't make bricks without clay.'"
