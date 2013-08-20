---
author: David Hogue
comments: false
date: 2006-03-15 13:15:12+00:00
layout: post
slug: arguing-about-code-with-myself
title: Arguing About Code With Myself
wordpress_id: 338
categories:
- Software Development
tags:
- old-blog
---

Anyone else ever have conversations with themselves?   I wouldn't really say i'm hearing voices, but I can have a discussion with differering points of view in my head.

Today it went something like this:


> 1:This code should be unit tested.  Unit testing would solve all my problems.
2:Screw it.  I'm already in the code.  I'm on a roll.  I don't want to lose that momentum.
1: I'm going to add some tests.
2:We can't just slap tests on it.  This code is big and complicated.
1:Why?  Why can't the code be simple, readable, and still do everything it needs to do.  There's no reason for the code to be ugly.
2: We don't have time to make the code pretty.  We should concentrate on the nasty bug, fix it, and move on to the next bug.


I really want to side with #1, but #2 does have a point.  I often feel that I don't have time to fix things right.  Sometimes I think: I'll do the quick fix now and come back later.

Here's another one:


> 1:Let's move this code to a new function
2:Great!
1:Let's use generics to remain type safe
2:Wow that's a lot of nested generics *
1:I should make some new classes for these data types
2:We don't have time


*` Public Function GetData(ByVal ids As Dictionary(Of Integer, List(Of Integer))) As Dictionary(Of Integer, Dictionary(Of Integer, NameValueCollection))`
