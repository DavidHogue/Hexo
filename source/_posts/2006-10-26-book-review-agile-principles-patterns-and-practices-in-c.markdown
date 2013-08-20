---
author: David Hogue
comments: false
date: 2006-10-26 06:35:52+00:00
layout: post
slug: book-review-agile-principles-patterns-and-practices-in-c
title: 'Book Review: Agile Principles, Patterns, and Practices in C#'
wordpress_id: 162
categories:
- Software Development
tags:
- old-blog
---

The short version: This is the kind of stuff that every .net developer should know, but almost nobody talks about.

There are some books on design patterns and agile is growing in the .net world.  A lot of the material in the PPP book covers topics that I haven't seen any .net specific books touch. (principles, packaging).  It's chock full of good information on how to design at the class and package level.

The original version of the book was in Java and C++.  I would have been fine with that, but when I heard there was a C# version coming out soon I decided to wait.  I'm hoping with it being C# oriented I can pass it around the office and get a few people interested.

The book is broken up into sections:



#### Agile Development



This section covers Agile development and Extreme Programming at a mid to high level.  Probably not the best book if you are looking purely for info on XP, but it's a good introduction/refresher.  The sections on testing, refactoring, and the bowling game were especially good.



#### Agile Design



This is the real meat of the book.  It covers principles of object oriented design.  I'd seen references to these before and even looked some of them up, but it's useful to have them all in one place with examples in a familiar language.

This section also covered uml diagrams.  Good info, but I think a single chapter would have been enough.  It is useful information and I know I personally don't make use of diagrams enough when trying to explain what I am thinking.

The section wraps up with a chapter on designing a simple program.  This chapter really made me think and I learned a great deal from it.



#### The Payroll Case Study



The book goes on to create a payroll application.  The chapters in this section cover several design patterns.  The authors also point out that design patterns demonstrated are overly complex for the the small sample code.  The trade-offs of patterns are listed.  This is nice because a lot of material on patterns talks about when to use a pattern, but not when not to use a pattern

This section also covers packaging the payroll application.  This something I haven't seen covered anywhere else.  After reading this it becomes obvious why some packages used here at work are so hard to work.  (not that I'm blaming anyone.  I'm as much responsible as anyone else)



#### Summary



I thought the book was extremely informative, enlightening, and well written.  I'd recommend it if you want to learn more about how to design classes and packages.  It does a good job of telling you not just how to code, but why you want to code in this or that way.

It doesn't cover any specific libraries like ASP.NET, Windows Forms, or ADO.NET.  If that's what you're looking for there are many, many other books.
