---
author: David Hogue
comments: false
date: 2006-03-18 16:28:49+00:00
layout: post
slug: copy-and-paste-with-unit-tests
title: Copy and Paste with Unit Tests
wordpress_id: 339
categories:
- Software Development
tags:
- old-blog
---

I've been trying the unit test thing again lately (both [NUnit](http://www.nunit.org/) and [AsUnit](http://www.asunit.org/)) and I've noticed that I often copy and paste a test to make a new test with similar setup.  I think copy and paste fits under the term [code smell](http://xp.c2.com/CodeSmell.html).  (I like that term, I think I'll start using it more often.)

Are unit tests just destined to be repetitive?  Maybe some of the things I'm testing go beyond simple unit tests into functional tests or acceptance tests.  I don't really know much about either.

Some of the code under test when this happens could be better designed.  Often when I end up with copied and pasted code to test different paths inside a class when probably the right thing is to do is make the class more testable by breaking up some functions or something.



#### Example


Lets say I have a test like this:


    
    public function testAdd():Void {
        graph.addObject(new GameObject());
        assertEquals("Count is 1", graph.count(), 1);
    }



and I want to test a similar function:


    
    public function testAdd():Void {
        graph.addObject(new GameObject());
        assertEquals("CountInRect is 1", graph.countInRect(0, 0, 10, 10), 1);
    }



or test the same function with slightly different input:



    
    public function testAdd():Void {
        graph.addObject(new GameObject());
        graph.addObject(new GameObject());
        graph.addObject(new GameObject());
        assertEquals("Count is 3", graph.count(), 3);
    }



P.S. The WordPress "visual rich editor" isn't too helpful when trying to format code.
