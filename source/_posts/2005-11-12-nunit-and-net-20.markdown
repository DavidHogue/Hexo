---
author: David Hogue
comments: false
date: 2005-11-12 01:51:16+00:00
layout: post
slug: nunit-and-net-20
title: NUnit and .net 2.0
wordpress_id: 299
categories:
- Software Development
tags:
- old-blog
---

I've been using .net 2.0 and the new Visual Studio for a bit now.  I haven't had many problems yet.  I still have to keep a vs2003 project file around since I am the only one using vs2005 and I have to compile my releases with vs2003 since the servers don't have 2.0 yet.

One problem I ran across though is running unit tests in nunit.  I get the following:

`C:>nunit-console UnitTestsbinDebugUnitTests.dll
NUnit version 2.2.2
Copyright (C) 2002-2003 James W. Newkirk, Michael C. Two, Alexei A. Vorontsov, Charlie Poole.
Copyright (C) 2000-2003 Philip Craig.
All Rights Reserved.
OS Version: Microsoft Windows NT 5.1.2600.0    .NET Version: 1.1.4322.2032
The format of the file 'UnitTests' is invalid.`

The gui gives me a similar message with a System.BadImageFormatException.  I've tried adding <supportedruntime version="v2.0.50215" /> to nunit-console.exe.config and nunit-gui.exe.config, but It's not helping.

Anyone out there know what the deal is?

_Edit 5:16: the xml wasn't showing_
