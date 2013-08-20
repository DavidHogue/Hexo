---
author: David Hogue
comments: false
date: 2006-03-30 07:52:00+00:00
layout: post
slug: javascript-class-event-handlers
title: Javascript Class Event Handlers
wordpress_id: 340
categories:
- Software Development
tags:
- old-blog
---

For a while now I've been trying to make my javascript code more object oriented by using javascript "classes".  Now classes in javascript are a little odd: there's no class keyword.  Methods are just functions inside a "class" function.  Events have a few quirks too and I was having trouble getting events to play well with classes.

Here's an example class:

    
    function ExampleClass() {
         // methods
        this.exampleFunction = function() {
            alert('HI!');
        }
        this.eventHandler = function() {
            this.exampleFunction();
        }
        // constructor
        setTimeout(function() { this.eventHandler(); }, 10000);    // run eventHandler in 10 seconds
    }



The problem I was having was that when the timeout called eventHandler it didn't have a reference to `this` anymore!  There is a neat trick to get around this though:


    
    var me = this;
    setTimeout(function() { me.eventHandler(); }, 10000);



By setting a variable (`me`) equal to `this` and using that I can keep a reference to the class when the event fires.  I saw this trick once or twice in actionscript, but never thought to apply it to javascript.

There is a [neat article](http://w3future.com/html/stories/callbacks.xml) about this I found.  [Sjoerd Visscher's weblog](http://w3future.com/weblog/) has a whole bunch of good stuff about really advanced javascript.

I found a [recent post](http://west-wind.com/weblog/posts/5033.aspx) where it looks like someone else was running into the same problem and the commenters suggested the same solution.


