---
author: David Hogue
comments: false
date: 2006-12-06 03:43:09+00:00
layout: post
slug: starting-with-xna
title: Starting with XNA
wordpress_id: 177
categories:
- Software Development
tags:
- old-blog
---

Started playing with [Microsoft's XNA](http://msdn.microsoft.com/directx/XNA/default.aspx) yesterday.  XNA is a game development framework from Microsoft that allows development of 2D and 3D games for windows and XBox360.  I wasn't expecting much.  I mean it's a pre-1.0 beta from Microsoft....

I have been meaning to start doing a little in-my-spare-timeLike I have any spare time!  I haven't even posted anything in over a month game development for a while.  Right now I'm trying to evaluate a few different platforms to use: Flash, XNA, Java, or hardcore C++.

Game Studio Express is the IDE needed to develop for XNA.  It is actually an addon to Visual C# Express, their free C# IDE, so you need to install that first.  It's very familiar if you've used Visual Studio at all.  All the code is in C# and there are a few sample projects.

The framework is definitely coder focused with some content "pipeline" features.  This feels reversed from Flash where it is aimed at designers with scripting kind of worked in.

There are readily accessible classes that give you the basic stuff you need right away: mouse, keyboard, vectors, etc.  The main class must inherit from a base class that has a few methods to override for updating, drawing, loading resources, etc.  I assume it handles the main game loop as well.

I've only spent a few hours with it, so I can't tell if the basic stuff they give you is very limiting or not.  The built in Microsoft controls in other .net technologies seem useful and extensible at first, but then I inevitably get into a situation where I need it to do something they didn't think of and have to override some bizarre function in what feels like a hack to do something seemingly simple.

So far it seems a whole hell of a lot easier to work with then back in the day when I had to write all my vector and input code by hand.  I can't see high performance game engines written in a VM with a garbage collector for some time yet, but it might just work out for the so-called casual games.
