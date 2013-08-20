---
author: David Hogue
comments: true
date: 2011-07-28 18:17:06+00:00
layout: post
slug: in-response-to-request-for-comments-issues-with-net-and-microsoft-product-versioning
title: 'In response to Request for Comments: Issues with .NET and Microsoft Product Versioning'
wordpress_id: 51
categories:
- Technology
tags:
- microsoft
- versioning
---

I started writing a comment on Scott Hanselman's blog post [Request for Comments: Issues with .NET and Microsoft Product Versioning](http://www.hanselman.com/blog/RequestForCommentsIssuesWithNETAndMicrosoftProductVersioning.aspx), but it got too long so I decided to make my own post about it.

A few thoughts to throw on the pile of comments already there:

**I like [semantic versioning](http://www.semver.org/)** like 4.1.2, but I could see that maybe the marketing department would want to make the name a little friendlier.  If some words are in there, keep it simple and consistent.  _Wiz Bang 2011 SP 2 Beta 3_ is the most complex I should ever have to parse.  And that's if I want to get all technical and play with pre-release software.

I think the most a non-developer, like your boss or manager, should really care about is two numbers.  One for the version of the product, _Office 2010_ for example, and one for updates of at least moderate size that increments the SP or .x number.

**Lose the acronyms.**  How many people know what CTP or PU or even R stand for?  At least stick with SP like Windows had been doing for years.  Couldn't CTP be replaced with the word Beta, or Preview?

Put the numbers in descending order of importance.  If it's going to be _Wiz Bang 2011_, fine, I'll treat 2011 as the major version that I am using.  Wiz Bang 2011 SP1 would be alright too if it's a collection of medium to small changes.  If it's a new, incompatible version that's being sold separately, don't add an R2, change the major number from 2008 to 2010.

And finally if you're already using decimal notation, like 3.5, don't throw other numbers around.  Update that number or tack another .1 on there.  3.5.1 means it's a little bug fix update.  3.5 R2 means "say what?"


