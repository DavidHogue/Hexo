---
author: David Hogue
comments: false
date: 2007-03-17 01:36:57+00:00
layout: post
slug: fast-tests-slow-tests
title: Fast Tests > Slow Tests
wordpress_id: 203
categories:
- Software Development
tags:
- old-blog
---

> 
------ Test started: Assembly: I*****Lib.Tests.dll ------

90 passed, 0 failed, 0 skipped, took 3.30 seconds.




vs.



> 
------ Test started: Assembly: Win***.UnitTests.dll ------

722 passed, 0 failed, 11 skipped, took 127.41 seconds.




Which would you run more often?  To be fair the second project is much, much larger than the first: 117450 non comment lines, compared to 1454.  The big one is vb, the small one is c# so line count might not be the fairest comparison, but you get the idea.

Still, two minutes (plus compile time) is long enough that I don't run the tests all that often.  Or, if I do run them often, I feel like I am not moving fast enough.  With just 3 seconds to run the tests; I can anytime I stop typing for a few seconds.

The main things slowing the big project down are the database, and ui tests.  Almost every test needs to talk to the database.  I've been able to get the tests running against an embedded database with the minimum amount of data, but it's still slow.  The ui tests are run through [NUnitForms](http://nunitforms.sourceforge.net/).
