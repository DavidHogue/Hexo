---
author: David Hogue
comments: false
date: 2007-12-13 19:31:14+00:00
layout: post
slug: quick-tip-fullscreen-window-in-wpf
title: 'Quick Tip: Fullscreen Window in WPF'
wordpress_id: 245
categories:
- Software Development
tags:
- old-blog
- wpf
---

(aka Windows Presentation Foundation aka Avalon aka XAML)


    
    WindowState = WindowState.Normal;
    WindowStyle = WindowStyle.None;
    Topmost = true;
    WindowState = WindowState.Maximized;



That's it, nice and easy.  Setting WindowState to normal before and then maximized after fixed an issue where it was fullscreen, but didn't expand to cover the taskbar.

I did this in order to make a patch for [Big Visible Cruise](http://code.google.com/p/bigvisiblecruise/), a new app that displays [CruiseControl.net](http://ccnet.thoughtworks.com) statuses in a big noticeable window.  ([Issue 14](http://code.google.com/p/bigvisiblecruise/issues/detail?id=14))

I got some ideas from [this forum post](http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=177710&SiteID=1) on the MSDN forums.

Big Visible Cruise is hosted on Google Code.  I'd never used it before, but it was really easy and simple to log in, add a comment, and attach a patch.
