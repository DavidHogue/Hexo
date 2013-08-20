---
author: David Hogue
comments: true
date: 2006-10-06 01:41:37+00:00
layout: post
published: false
slug: data-binding-isnt-always-the-solution
title: Data Binding Isn't Always The Solution
wordpress_id: 166
categories:
- Software Development
tags:
- old-blog
---

Data Binding Doesn't Scale.  Well, maybe scale is the wrong word.  More like it is difficult to use in a situation more complex than a demo or tutorial.  

Note that for the purposes of this post when I say data binding I mean doing things like adding a System.Windows.Forms.Binding to a TextBox's Text or a ComboBox's SelectedValue properties for a custom object, 

Like most development tools from Microsoft, data binding just doesn't apply to every problem.  It works great for getting something simple up and running, but the minute you want to make it work a little differently, or on a slightly more complex situation, you should probably drop it and just write some code to copy properties back and forth

Passive ViewPassive View a form of what used to be the Model View Presenter (MVP) pattern.  Martin Fowler has split the MVP pattern into the [Supervising Presenter](http://www.martinfowler.com/eaaDev/SupervisingPresenter.html) and [Passive View](http://www.martinfowler.com/eaaDev/PassiveScreen.html) patterns. can be a good alternative to data binding.  Especially if you have logic or formatting needs that a Binding can't easily handle.

Recently I've heard it said that features in Visual Studio are designed for demos.  That is, they are designed to be impressive when giving a demo (they can make claims like "reduces code by 70%!").  They are not designed for maintainability or extensibility.

That is fine with me.  Use data binding in the simple cases where it works.  If you have a small app that you need to just get something done, use binding.  Just know that it will be easier to replace the bindings then extend them much.  The 80-20 rule might apply: use data binding in the 80 percent of situations where it fits, and in the other 20: don't force it.

I've had the same experience with the vs2003 web forms designer, data grids, xml serialization.  I could come up with more examples, but I think you get the idea.  In each case the tool worked well initially. However, I have seen a _ton_ of hours go into customizing these in ways Microsoft didn't intend.  In each case it would have been much better just to replace the prepackaged Microsoft solution with a small amount of custom code that did exactly what was needed and nothing more.

The problem, I guess, is that the marketing materials say that this is the way to do it.  Use this feature in every situation whether it fits or not.  They don't present different options with trade offs.

And I understand that it is marketing.  It just seems to me that there is a lack of options when it comes to .net and the Microsoft way.

I'm not sure if I had a point in there.  I've just been working with data bind lately and finally decided to scrap it on the screens I'm working on.  The resulting code is much cleaner.  Plus, since it doesn't need reflection, the code is more obfuscatable.  As an added bonus it's also more testable.
