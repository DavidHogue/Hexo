---
author: David Hogue
comments: false
date: 2008-01-03 07:12:03+00:00
layout: post
slug: workaround-for-weird-firefox-bug-where-the-textarea-cursor-will-dissappear
title: Workaround for weird Firefox bug where the textarea cursor will dissappear
wordpress_id: 247
categories:
- Software Development
tags:
- firefox
- old-blog
---

Every once in a while I run across a bug in Firefox that basically hides the blinking cursor that is supposed to be in a textbox.  It's still there and I can still type, but I just can't tell where the next character will appear.  Every time this happens, I have to Google around a bit and find the Bugzilla bug describing it.

For my own reference: here is the [bug report](https://bugzilla.mozilla.org/show_bug.cgi?id=167801).  It will be fixed in Firefox 3.0, the workaround is to add a style="overflow: auto" to a parent element of the textbox.  Apparently it is caused by placing a textbox in a position: fixed element with a height.

I also found [a fix over on Bram.us](http://www.bram.us/2007/05/31/my-note-to-myself-dissapearing-firefox-caret-cursor-css-fix/) that is a bit of css that should fix every input and textarea on a page.
