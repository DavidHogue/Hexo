---
author: David Hogue
comments: false
date: 2005-12-13 06:53:38+00:00
layout: post
slug: my-dads-virii
title: My Dad's Virii
wordpress_id: 312
categories:
- Technology
tags:
- old-blog
---

I was doing some work on my home network when I found some odd traffic.  I started looking closer and I found that my Dad's computer was connecting directly to random SMTP servers.  There were a few connections on non-standard ports as well.  So, I went down there and fired up a free virus scanner.

There were 91 virii, and 1 worm according to [Trend Micro's Housecall](http://housecall.trendmicro.com).  His computer was spewing out emails to tons of addresses but he doesn't care because he can still use it and doesn't see the problem.

I have removed the virii that I found and blocked port 25 to anything other than the ISP's mail server.  I've got the feeling that I missed a virus or two.  There are still some attempted connections to non-standard ports.

Luckily those are blocked by the firewall.  A good firewall should block outgoing traffic as well as incoming.  Aside: I am using [m0n0wall](http://m0n0.ch/wall/) for my home network.
