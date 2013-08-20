---
author: David Hogue
comments: false
date: 2006-07-26 02:45:25+00:00
layout: post
slug: firefox-20b1-mini-review
title: Firefox 2.0b1 Mini Review
wordpress_id: 355
categories:
- Technology
tags:
- old-blog
---

I've been using the [Firefox 2.0 Beta 1](http://www.mozilla.org/projects/bonecho/all-beta.html) for a week or so now.  So far it's looking pretty good.  The rendering engine is the same as 1.5, but there are some new features:

[
![screenshot of Firefox suggest](http://vorpal.cc/blog/wp-content/uploads/2006/07/firefox-suggest.thumbnail.png)
](http://vorpal.cc/blog/wp-content/uploads/2006/07/firefox-suggest.png)



#### Built in google suggest



The search bar will now suggest common phrases as you type.  I assume this is using [Google Suggest](http://labs.google.com/suggest), but I don't know that for certain.  While cool, some people may see it as some sort of privacy concern.  I'm not sure if it can be turned off.




#### Built in spell checker



Firefox will spell check most text fields as you type.  Seems to work pretty good so far and I haven't had any problems with it.  I used to use [SpellBound](http://spellbound.sourceforge.net/) for this.

[
![screenshot of changing Firefox's default reader](http://vorpal.cc/blog/wp-content/uploads/2006/07/change-reader.thumbnail.png)
](http://vorpal.cc/blog/wp-content/uploads/2006/07/change-reader.png)



#### Better feed reader support



This is cool.  While 1.0 had some simple stuff with live bookmarks, 2.0 has much better support for external readers.  When you click the orange rss icon in the address bar it shows you the feed in a presentable way, not the ugly xml.  Then it gives you a button to subscribe to the feed with your default reader.  It supports external programs as well as web based feed readers.

[
![screenshot of setting up a custom reader](http://vorpal.cc/blog/wp-content/uploads/2006/07/reader-setup.thumbnail.png)
](http://vorpal.cc/blog/wp-content/uploads/2006/07/reader-setup.png)

I use Gregarius for most of my feed reading and I was able to get it to work with the new feeds by messing with the config.  Here's how to add your own web based reader: 





  1. Go to about:config


  2. Filter on browser.contentHandlers


  3. Add 3 strings like in the [last screenshot](http://vorpal.cc/blog/wp-content/uploads/2006/07/reader-setup.png)


  4. Restart Firefox





#### Session storage



I've only had the beta crash once on me.  After the crash it loaded up all the tabs I had open.  I think I'm going to love this feature if it works well as I have several tabs open all the time, sometimes for hours or days at a time.
