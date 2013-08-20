---
author: David Hogue
comments: false
date: 2007-06-20 16:05:41+00:00
layout: post
slug: a-useful-article-on-msajax-and-updatepanels
title: A Useful Article on MSAJAX and UpdatePanels
wordpress_id: 225
categories:
- Software Development
tags:
- old-blog
---

I found [this article on UpdatePanel tips and tricks](http://msdn.microsoft.com/msdnmag/issues/07/06/WickedCode/) useful.  The official site at [http://ajax.asp.net](http://ajax.asp.net) has loads of documentation, but I haven't found it too useful other than for the very basic stuff.

The feel I got from the ajax.asp.net documentation was that you weren't supposed to write any JavaScript to use with UpdatePanels.  This article showed how to trigger JavaScript before and after an UpdatePanel updates and how to bypass the UpdatePanels altogether.

Also, [Firebug](http://www.getfirebug.com/) has been very useful in debugging this since you can see the full request and response for all the communication back to the server.  The logging ability is also _much_ nicer than having alert boxes everywhere.
