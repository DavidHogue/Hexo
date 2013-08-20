---
author: David Hogue
comments: false
date: 2007-01-30 05:16:44+00:00
layout: post
slug: thats-better-site-updates
title: That's better (site updates)
wordpress_id: 185
categories:
- Meta
tags:
- old-blog
---

I finally got around to fixing up this place a bit.  I made new SSL certificates (because my other certs had expired).  I set up a root CA a while back using [this guide](http://www.eclectica.ca/howto/ssl-cert-howto.php).

Also, if you've been here recently you may have noticed some warnings about SSL from the non-SSL pages (like the main blog page).  This was because I had to do some funky stuff to get the [WordPress admin area to be SSL only](http://vorpal.cc/blog/category/security/wordpress-and-ssl.html).  This worked fine for a while, but updates and plugins caused some links to use https urls instead of http.  I fixed that with the [Secure Admin](http://haris.tv/2007/01/11/wordpress-ssl-plugin-secure-admin-patched-and-working/) plugin.

Anyway, I've got a few errands to run now, so that's it.  There are a few topics that I've been thinking about for a while now and I may actually get around to posting them soon.  We'll see.....
