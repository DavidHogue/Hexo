---
author: David Hogue
comments: false
date: 2005-12-17 05:45:41+00:00
layout: post
slug: why-are-developers-afraid-of-exceptions
title: Why are developers afraid of exceptions?
wordpress_id: 316
categories:
- Software Development
tags:
- old-blog
---

Why?  In most of the code I have been working on lately it seems like the developer was afraid of exceptions.  Now a lot of this code is 1-3 years old and written by VB developers in VB.NET.  (I'm not trying to bash VB here.  I believe good code **can** be written in any language.)  I have heard a few arguments against exceptions which I agree with under certain circumstances.  





  1. 
Exceptions should not be used in normal program logic.  Certainly if you are writing a loop and could throw and then catch a few thousand exceptions this is true, but if there is an error in the code or data then I think an exception is appropriate.  I try to check my public function parameters and throw ArgumentException or ArgumentNullExceptions.



  2. 
Exceptions are slow.  Slow is a relative word.  Especially when programming.  Again if an exception will be thrown and caught several times during normal program execution that isn't good.  However if you throw an exception when invalid data comes back from the database or when a webservice isn't responding then it is not slow at all.




I have heard both of these used as excuses not to **ever** throw an exception.  That they just aren't a valid option under any circumstances.  There are some places where I feel exceptions are useful:




  1. Invalid input: the program shouldn't crash if the user puts text in an integer input, but if that text makes it down to the lower levels of code where it shouldn't be.  In either case the user should be presented with an error message.


  2. "Impossible" states: as a sanity check.  What if some one mucked up the database, or if some files were accidentally deleted.


  3. Corrupt data/connectivity issues: when the database is down for example



I'm just sick of stored procedures that return a 0 on an error, then the function checks for 0 and returns -1, then the page checks for -1 and makes a label visible, etc.  It's just so f'ing confusing when code at so many different layers has to check for the error code and pass an error up the stack.  I also find exceptions much easier to debug (unless they are caught and silently discarded, but that's another post).

Guess I just needed to vent a little...
