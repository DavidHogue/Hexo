---
author: David Hogue
comments: false
date: 2005-11-01 19:04:57+00:00
layout: post
slug: ioc-and-testability
title: IoC and Testability
wordpress_id: 296
categories:
- Software Development
tags:
- old-blog
---

I had heard of Inversion of Control and Dependency Injection before, but it wasn't until recently that I started using them.  In a [post](http://vorpal.cc/blog/?p=13) not long ago I wrote about how I was trying to get unit tests on a class that depended on a host of static methods in other classes.  While trying to write some wrapper classes I almost had an IoC pattern going before I knew it.  A comment pointed me to [Castle](http://www.castleproject.org/index.php/Container) and [Spring](http://www.springframework.net/).

I have since used both frameworks.  In that project I started to use Castle's IoC container, but then I realized I didn't really need it and I just passed everything in to the constructor manually  (my case was pretty simple).  On another project I used Spring.Net.  In that project I am relying heavily on Spring.Net to create my objects and for configuration.  It's great I can completely modify the program's behavior at runtime just by editing the .config file.
