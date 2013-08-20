---
author: David Hogue
comments: false
date: 2006-05-21 01:24:15+00:00
layout: post
slug: unit-testing-payoff
title: Unit Testing Payoff
wordpress_id: 350
categories:
- Software Development
tags:
- old-blog
---

Today1 I got my first taste of the real usefulness of unit tests beyond the initial design/development phase.

We have this piece of JavaScript that fades between several images in slideshow kind of way.  The previous version had done this using Internet Explorer's filters and did not work in any other browsers.  I wasn't real happy with this, being a Firefox user, but there was little I could do about it.

So when we finally decided to make a cross-browser version I figured I would do it test first with [JsUnit](http://www.jsunit.net).  My first problem was adding tests to the existing code.  The code wasn't very testable, so I would extract the code piece by piece.  Each piece I pulled out I wrote a test for, then I went and manually tested with several browsers to make sure nothing broke.  Once I had my tests in place, I started adding new code that would make the images fade in other browsers.

This was sometime last week.  Today we went to publish the change to the production servers and a bug was found.  The new code didn't work if there was more than one slideshow on a page.  So I went and added a test for multiple slideshows.  Sure enough the test failed.  I went about fixing the test and broke a few other tests in the process because I overlooked something.  I fixed those tests, and published the changes.

I was confident that my changes would not break anything and that I could put the code into production.  If there were no tests, I would have spent much longer making the change and probably broken some live sites in the process.

This was a pretty time critical change that the customer wanted _yesterday_.  Sometimes it does feel like I am going slower by writing tests.  In this case TDD saved me time.  Maybe not overall, but it saved me time when speed was critical.





  1. Today being two or three weeks ago when I started this post.  I've been slacking... ↩


