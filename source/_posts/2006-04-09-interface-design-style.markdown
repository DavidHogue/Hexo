---
author: David Hogue
comments: false
date: 2006-04-09 17:56:14+00:00
layout: post
slug: interface-design-style
title: Interface Design Style
wordpress_id: 342
categories:
- Software Development
tags:
- old-blog
---

I have a few thoughts about coding with interfaces.  Not quite code style, but more like design style.  None of these are set in stone, just some of my personal preferences.

I prefer interfaces over base classes -- base classes have code shared by all implementations.  While there is an argument that the base class's code will be better tested since it is used more, I think there is an advantage to multiple independent implementations of an interface.  Interfaces also make unit testing much easier.  And a class can implement multiple interfaces, but it can only have one base class (in .net anyways)

I don't use many static (shared in vb) methods.  They lead to tight coupling, difficult testing, and very procedural designs.  You can't override static methods.  I will make an exception for simple utility methods and factory methods.  Most of the static methods I have seen are only static to avoid creating an instance of the class and assigning it to a variable.  I don't think saving one line or a few bytes of memory isn't worth the frustration.  Something like MessageBox.Show("Hello, World!") would be fine, but if everything is static you lose most of the advantages of object oriented programming.
