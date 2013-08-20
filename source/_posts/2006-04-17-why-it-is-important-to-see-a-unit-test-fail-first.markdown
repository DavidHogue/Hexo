---
author: David Hogue
comments: false
date: 2006-04-17 14:45:12+00:00
layout: post
slug: why-it-is-important-to-see-a-unit-test-fail-first
title: Why it is Important to See a Unit Test Fail First
wordpress_id: 90
categories:
- Software Development
tags:
- old-blog
---

#### The short version:


For the tests to be really effective you have to be able to trust them and seeing the test fail first reinforces my trust that the tests are working.



#### The long version:


The first thing I heard about unit testing and test driven development (TDD) is that the tests are written first.  But, the next thing I heard was that you need to see the test fail.  It never seemed that important and often when I'm coding I don't want to get out of code writing mode to run the test.

I can understand writing the test, then attempting to compile and having the compiler give an error that it can't find the function I just wrote the test for.  Code, compile, fix syntax errors, compile, fix syntax errors, compile, code, compile... Is my usual rythm and has been for so long it's hard to change.  It should be code, compile, fix syntax errors, compile, run tests, fix tests, run tests, code.

Anyway, to get to my point: if I write the test, then the code under test without _running_ the test I have no idea if the test is working.  Sure it's running and the bar is green, but what if the test is broken?

What promped this post was some code I just wrote.  I really didn't think the code would pass the test on the first try, and when it did I didn't believe the test.  I had to go and break the code just to make sure the test was working.

I'm still new to TDD and I am learning a lot each time I try to apply it to a project.  It's been tough, but very educational.
