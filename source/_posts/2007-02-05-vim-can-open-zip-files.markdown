---
author: David Hogue
comments: false
date: 2007-02-05 01:15:04+00:00
layout: post
slug: vim-can-open-zip-files
title: Vim Can Open Zip Files?
wordpress_id: 187
categories:
- Technology
tags:
- old-blog
---

I use [Vim](http://www.vim.org/) as my basic text editor in Linux.  Today I downloaded a zip file with wget and it downloaded very quickly.  I assumed it just saved an error page (as it sometimes does).  My first idea to check the error message was `vim ScrewTurnWiki-1.0.11-Precompiled.zip` and it gave me this:

[![vim zip](http://vorpal.cc/blog/wp-content/uploads/2007/02/screenshot-vim-screwturnwiki-1011-precompiledzip-dave-desktop.thumbnail.png)](http://vorpal.cc/blog/wp-content/uploads/2007/02/screenshot-vim-screwturnwiki-1011-precompiledzip-dave-desktop.png)

A list of all the files in the zip.  If I moved the cursor to a filename and hit enter, it opened the file.  It appears that I can edit the file :wq:wq writes the file and quits and it saves my changes back into the zip.

I really didn't expect that.  I figured it would give me a bunch of unprintable garbage if it tried to open a binary file like that.  I thought it was cool and just thought I'd share.
