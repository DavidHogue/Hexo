---
author: David Hogue
comments: false
date: 2006-05-06 22:21:36+00:00
layout: post
slug: tdd-is-hard-work
title: TDD is Hard Work
wordpress_id: 349
categories:
- Software Development
tags:
- old-blog
---

Especially when you're not used to the rythm of it.  I've been playing with unit tests for long enough that, at this point, I feel vulnerable without them.  However it's still easy for me to stray and write a bunch of code without tests.  Sometimes it seems harmless: I'll just add a line or two here, it won't break any tests, so what's the harm?



> I'll just add a line or two here, it won't break any tests, so what's the harm?



The problem with that is that when I come back to the code tomorrow, or next week, or next year I won't have tests for that functionality I just added.  Someone else could come along and not know what those two lines are there for, so they remove them.  All the tests pass, so they assume nothing is broken.  Then some time later the customer gets it and a feature is missing, or worse: a bug reappeared.

I've recently adopted a personal policy of only writing code that a test requires and no more.  If I want a new feature I have to add a failing test before I can write the code, and then only write enough code to make the test pass.  It's very easy to be writing the code to make the test pass, and then add "just a little bit" more.  I don't easily switch back to writing a test after writing the code to pass the previous test.  Or while refactoring I will think of some corner case or some nifty feature and just add it right there without creating a test first.

This works on new projects as long as I'm structured enough to follow my policy, but it gets really difficult with legacy code.  I'm talking huge projects (relatively anyway), with little to no automated tests and very rigid structures.  The code is not very object oriented at all.  And we are winding down development (the customer wants to get the project finished ASAP) and only doing bug fixes.  Honestly with this project I just want to get it done and I'm not worried about the tests.  Though, that does make it harder to enforce my policy on my other projects when I switch back and forth.
