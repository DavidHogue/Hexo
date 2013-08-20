---
author: David Hogue
comments: true
date: 2013-05-14 18:09:12+00:00
layout: post
published: false
slug: finding-which-piece-of-javascript-still-has-a-reference-to-a-dom-node
title: Finding which piece of JavaScript still has a reference to a DOM node
wordpress_id: 1182
categories:
- Software Development
---

So this might be blindingly obvious and I just never noticed it before. I'd like to think it's a new feature since last time I tried to debug this kind of thing, otherwise I took a whole lot more time than I needed to in the past.

It's fairly easy in javascript when manipulating the DOM to accidentally reference a node after you've removed it from the page. Maybe an event handler is still attached, or a global array still points to it. In a small app it's not a problem, but once the app gets big enough that memory is a concern there's usually a significant amount of code to go through.

I was looking for ways to reduce the memory taken up by the page and at the same time make things faster. That's when I found this on Stack Overflow: [Finding JS memory leak in chrome dev tools](http://stackoverflow.com/q/11930050/32127). The top answer linked to this jsFiddle: [jsfiddle.net/C5xCR/6/](http://jsfiddle.net/C5xCR/6/)



### The steps:





	
  1. Open the page and get to the point in the app where you think the object should be removed

	
  2. Take a heap snapshot

	
  3. Find the element in the heap

	
  4. Open the "Object's retaining tree




