---
author: David Hogue
comments: false
date: 2007-10-15 19:32:04+00:00
layout: post
slug: i-just-fixed-an-odd-timeout-error-with-our-cruisecontrolnetnantwatin-setup
title: I Just Fixed an Odd Timeout Error With Our CruiseControl.net/NAnt/WatiN Setup
wordpress_id: 233
categories:
- Software Development
tags:
- old-blog
---

**The problem:**  
  
I have this project I'm working on that uses [WatiN]() WatiN is a tool to write tests for web applications by controlling an Internet Explorer window. to test an asp.net site.    For some reason some tests would fail with a timeout trying to find an element or waiting for an element to show up after an UpdatePanel postback.  It would go through about half the test before stopping, it was able to open the browser, click buttons, type text, etc.  
  
I couldn't figure it out.  I ran the tests from the command line with NAnt, but they all worked then.  They all worked when I ran them from localhost.  I put [Ignore] attributes on most of the tests, I used [MSE](http://www.codeplex.com/Wiki/View.aspx?ProjectName=MSE) MSE: Managed Stack Explorer.  It will connect to a .net process and give a stack trace of where it is currently. looking for deadlocks.  I couldn't figure it out for the longest time.  
  
**The Solution:**  
  
Finally I went to Windows Update on the build server.  I thought maybe my workstation has some patch that is not on the server yet.  When I got there it told me that due to being on the internet zone, instead of the trusted zone, it couldn't do it's stuff.  This got me thinking an eventually I went to the url the tests were hitting and that wasn't in a trusted zone either.  
  
_Adding the urls to the local intranet zone fixed all my problems._  I'm not sure if the security was restricting WatiN or the msajax library.  I'd suspect the ajax stuff just because it seems like WatiN isn't going to be restricted by IE's security features.  
  

