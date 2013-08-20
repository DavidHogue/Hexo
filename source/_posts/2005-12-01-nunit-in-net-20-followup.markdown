---
author: David Hogue
comments: false
date: 2005-12-01 20:16:58+00:00
layout: post
slug: nunit-in-net-20-followup
title: NUnit in .net 2.0 Followup
wordpress_id: 304
categories:
- Software Development
tags:
- old-blog
---

Since I got this error again and there seems to be some traffic to the [previous entry](http://vorpal.cc/blog/posts/nunit-and-net-20), I'll tell everyone how I fixed it the second time.





  1. 
Go get NUnit 2.2.3



  2. 
uncomment the startup block in nunit-console.exe.config and nunit-gui.exe.config




The startup block looks like this:

    
    <startup>
    	  <supportedruntime version="v2.0.50727"></supportedruntime>
    	  <supportedruntime version="v2.0.50215"></supportedruntime>
    	  <supportedruntime version="v2.0.40607"></supportedruntime>
    	  <supportedruntime version="v1.1.4322"></supportedruntime>
    	  <supportedruntime version="v1.0.3705"></supportedruntime>
    	
    	  <requiredruntime version="v1.0.3705"></requiredruntime>
      </startup>
