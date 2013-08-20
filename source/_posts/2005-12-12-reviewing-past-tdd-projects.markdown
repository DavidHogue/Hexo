---
author: David Hogue
comments: false
date: 2005-12-12 01:00:04+00:00
layout: post
slug: reviewing-past-tdd-projects
title: Reviewing past TDD Projects
wordpress_id: 310
categories:
- Software Development
tags:
- old-blog
---

Recently I've had to work on some older projects of mine.  A couple of these projects were key turning points in my understanding of test driven development.

There is the first project that I tried to use [NUnit](http://www.nunit.org/) on: While it does have classes and uses some basic inheritance, it is mostly procedural.  There is loads of logic in both the individual pages themselves and stored procedures.  Additionally the tests were added after the code.  I knew this wasn't correct at the time, but that's the way it worked out.

The tests were hard to write, I couldn't get seperate "units" to test.  The best I could do was call functions wrapped in a SQL transaction, then rollback the transaction at the end of the test.  Not good for a few reasons: They weren't really _unit_ tests, they had major external dependancies (database, config files, and would only run inside an ASP.NET server instance), and the test data could remain between tests.

On the second project the tests came in very handy.  While they still weren't driving the development and it was dificult to test some areas, it was **much** better.    During testing more tests were added based on bugs found.  This really helped debugging as the logic was quite complicated in places.  They worked more as regression tests and customer acceptance tests than unit tests.

The most recent project is where I finally saw the light.  Every class is isolated from every other class.  What dependencies there are is handled with DI by [Spring.NET](http://www.springframework.net/).  A few tests do hit the database or load config files, but they are few and mostly for sanity checking.

So, the conclusion is: TDD is much easier when the tests are done first and when the code is loosely coupled.  Proper TDD almost forces good object oriented design and loose coupling.  Improper TDD can be a nightmare and drive developers away from the methodology.
