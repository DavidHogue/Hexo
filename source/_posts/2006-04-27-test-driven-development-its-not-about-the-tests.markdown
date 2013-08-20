---
author: David Hogue
comments: false
date: 2006-04-27 23:00:09+00:00
layout: post
slug: test-driven-development-its-not-about-the-tests
title: 'Test Driven Development: It''s Not About the Tests'
wordpress_id: 347
categories:
- Software Development
tags:
- old-blog
---

The following is what I have learned about test driven development over the last year or so:

It's not about the tests.  What? How can this be, it is called **test** driven development!  True, but the tests in TDD are not for the QA team.  They are not for use at the end of the project for testing betas or anything.  TDD tests don't [obviate](http://www.google.com/search?q=define%3A+obviate) the need for traditional testing with integration tests, acceptance tests, etc.

So if TDD isn't about the tests then what is it about?  Glad you asked.  It's about designing your code to be testable.  The theory is that testable code is better designed.  It is very difficult to slap a unit test on to an existing class that wasn't designed for testability.  There are a few factors that make a class testable: 




  1. Self contained - it should be as self sufficient as possible (aka [low coupling, high cohesion](http://www.ugolandini.net/AccoppiamentoCoesioneE.html)).  The fewer dependecies a class has the easier it is to test.


  2. Requires data to be passed in rather than finding it (aka [Dependency injection](http://www.martinfowler.com/articles/injection.html)).  A method has all it's data handed to it in parameters is easier to test (and debug!) than a method that calls utility methods that get the data from somewhere else.


  3. Predictable (aka no fancy name :)).  Classes that have well defined inputs and outputs are much easier to test.



Really what it comes down to is this: If the class is easier to test, it is a better design.  The test first paradigm just forces you to use good design.  It makes a good design the path of least resistance.

Cohesion, coupling, and polymorphism are all words I knew the meaning of before.  It wasn't until I really started doing test driven development that I understood them.  I've learned how to write better code thanks to TDD.  It helps me to design better code (even when I'm not using the tests).

Another thing about tests: when I get sidetracked or distracted and come back to the code I often forgot where I was.  By looking at the tests I can easily figure out what I have done.
