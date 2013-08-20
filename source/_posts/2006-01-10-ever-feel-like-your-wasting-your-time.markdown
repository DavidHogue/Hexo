---
author: David Hogue
comments: false
date: 2006-01-10 05:19:52+00:00
layout: post
slug: ever-feel-like-your-wasting-your-time
title: Ever Feel Like You're Wasting Your Time?
wordpress_id: 319
categories:
- Software Development
tags:
- old-blog
---

Lately I've found myself spending many hours attempting to improve the code in a couple projects.  In both cases I am just [moving functions around](http://www.refactoring.com/catalog/moveMethod.html), [splitting up functions](http://www.refactoring.com/catalog/extractMethod.html), [extracting interfaces](http://www.refactoring.com/catalog/extractInterface.html) and such.  These operations are common refactorings.

My goal is to make the code more testable, more flexible, and overall easier to work with.  Problem is that there isn't much visible improvement for the clients and sometimes functions are broken in the process.  These clients have pressing bug reports and feature requests that I am trying to address and I almost feel like my time would be better spent just patching up the code.

Both of these projects have expanded greatly since their inception.  Features were added, large chunks of the infrastructure have to be changed every now and then.  The codebases are really inflexible so changing anything is painful and it takes a while to shake out all the bugs.  Once the bugs are taken care of it works alright; at least until the next change request.

I really want to believe I am making progress and my time is being spent in the right areas.  I know if I don't do this it will only get worse.  Still, I question every hour not spent working directly on a bugfix or feature.  (I do try to make improvements while changing related code, but that only gets me so far.)

_10:32pm grrr, sonofa, stupid...  Fixed stupid mistake in the title.  Can't believe I did that..._
