---
author: David Hogue
comments: false
date: 2007-08-04 20:13:50+00:00
layout: post
slug: looking-for-a-web-application-speed-testing-tool
title: Looking For a Web Application Speed Testing Tool
wordpress_id: 226
categories:
- Software Development
tags:
- old-blog
---

I'm not sure if anyone will notice this, it's been over a month since my last post...

Anyway, I'm looking for a tool to test a web application's performance.  Specifically I'm looking for something with these features:



	
  * Give it a url of a page and it will load the page, images, css, javascript, css images, and flash files in the order that a browser would.

	
  * Hit the server just like a browser: only 2 connections per user, only 1 javascript file at a time, supports gzip compression.

	
  * Can optionally use the Last-Modified, If-Modified-Since, ETag, and Expires headers on subsequent requests from each user.

	
  * Reports on average time to load the full page.

	
  * Outputs to a basic format like csv or simple xml that I could load into Excel for example.

	
  * Appents to the log so that I could run this once a day and gather stats.

	
  * Can be run from the command line so I could set up an automated process or integrate into the build server.



Things that would be just sweet, but not absolutely required:

	
  * Reports on the time it takes for the user to see a partial page; i.e. layout, links and 