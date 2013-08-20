---
author: David Hogue
comments: false
date: 2006-05-31 01:10:01+00:00
layout: post
slug: excel-com-visual-studio-2005-web-sites-shoddy-codebase-vb-fun
title: Excel + COM + Visual Studio 2005 Web Sites + Shoddy Codebase + VB == !Fun
wordpress_id: 351
categories:
- Software Development
tags:
- old-blog
---

ugh.

Not a good day.  I guess I really don't have much to say.  Just frustrated and need to write this somewhere...

Let's start with Excel.  Oh, the fun you can have with Excel.  So, I'm trying to create a spreadsheet through COM with VB.NET.  According to the marketing material and docs it should be simple.  Paste this code in and you have a spreadsheet!  Sure like that'll happen.  I'm just getting a generic error number.  Not even a message, just a number.  This works fine on my workstation, but not the laptop.  I hope I never have to deal with COM again.

Then Visual Studio and it's stupid "Web Site" projects.  I hate how these manage references: If it's a dll you get a .refresh file, if it's a project it goes in the .sln (wtf?), if it's in the GAC it adds to the web.config.  The web config one was frustrating me today.  It kept adding useless lines to the web.config for Excel and friends.  With the Excel references in the web.config, every page would crash if the machine didn't have Excel (even if it wasn't doing anything near Excel).  The site works fine if I take them out, so I have no idea what their function is.

I'm currently switching to a [Web Application Project](http://webproject.scottgu.com/).  Sucks when you have to download an addin to get back functionality that used to be there.  I'm worried when I hear all this new stuff from Microsoft (C# 3.0, linq, xaml, wpf, wwf, wtf).

Hey, Microsoft!  Fix the issues with the new releases first, then put some time into the next version.  Seriously 2.0 only recently came out, Visual Studio has a ton of bugs and you're already well into the next version.

Anyway, don't take any of this seriously.  Just having a frustrating day.
