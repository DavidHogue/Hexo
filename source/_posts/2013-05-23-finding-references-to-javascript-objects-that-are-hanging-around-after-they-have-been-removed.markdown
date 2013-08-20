---
author: David Hogue
comments: true
date: 2013-05-23 05:30:54+00:00
layout: post
slug: finding-references-to-javascript-objects-that-are-hanging-around-after-they-have-been-removed
title: Finding references to JavaScript objects that are hanging around after they
  have been removed
wordpress_id: 1185
categories:
- Software Development
tags:
- debugging
- javascript
- memory
---

So this might be blindingly obvious and I just never noticed it before. I'd like to think it's a new feature since last time I tried to debug this kind of thing, otherwise I took a whole lot more time than I needed to in the past.

It's fairly easy in javascript when manipulating the DOM to accidentally reference a node after you've removed it from the page. Maybe an event handler is still attached, or a global array still points to it. In a small app it's not a problem, but once the app gets big enough that memory is a concern there's usually a significant amount of code to go through.

I was looking for ways to reduce the memory taken up by the page and at the same time make things faster. That's when I found this on Stack Overflow: [Finding JS memory leak in chrome dev tools](http://stackoverflow.com/q/11930050/32127). The top answer linked to this jsFiddle: [jsfiddle.net/C5xCR/6/](http://jsfiddle.net/C5xCR/6/) which was a good place to experiment with the tools a bit.



### The steps:





	
  1. Open the page and get to the point in the app where you think the object should be removed

	
  2. Open Chrome's DevTools and go to the Profiles tab

	
  3. Take a heap snapshot

	
  4. Find the element in the heap

	
  5. Open the Object's retaining tree



You should get something that looks a little bit like this:
![](http://davidhogue.com/blog/wp-content/uploads/2013/05/dev%20tools%20references.png)


It doesn't link you directly to the source file, but you do get variable names which you can then find in your code. This works best if you can do it on a un-minimized, dev copy of the code.
