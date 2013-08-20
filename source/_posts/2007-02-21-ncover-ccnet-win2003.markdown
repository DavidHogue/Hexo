---
author: David Hogue
comments: false
date: 2007-02-21 00:20:06+00:00
layout: post
slug: ncover-ccnet-win2003
title: NCover + CCNet + Win2003
wordpress_id: 196
categories:
- Software Development
tags:
- old-blog
---

Having trouble running NCover on a new Windows 2003 build server? Getting an error like "Profiled process terminated. Profiler connection not established"?  Does NUnit-Console.exe keep running after NCover has exited and NAnt hangs waiting for NUnit, but NUnit never finishes?

Run this from the directory where NCover is installed: `regsvr32 coverlib.dll`

I found the solution at the [NCover forums](http://ncover.org/SITE/forums/thread/43.aspx#94).
