---  
author: David Hogue  
layout: post  
title: Goodbye Wordpress  
date: 2013-08-13 22:16  
comments: true  
categories: Meta  
---

So I've been working on migrating from Wordpress to a static html scheme. For
now I'm using [Octopress][1] to generate pages. It's working well enough for
now, but I'm still looking for alternatives.

[1]: <http://octopress.org/>

I like static files because they're fast and simple to serve. I don't have to
worry about keeping Wordpress up to date with the latest security fixes or
adding layers of caching just in case an article gets picked up on Hacker News
or Reddit. I like that Octopress uses Markdown so I don't have to worry about
html while editing. I'm currently using [Texts][2] to do my editing and I'm
looking for a good workflow from that to Octopress still.

[2]: <http://www.texts.io/>

I don't really like that Octopress is as complex as it is. Creating a theme
meant navigating through a couple dozen html templates and Sass files. And
installing all the dependencies on both my desktop and server took some time
because I don't have a lot of other Ruby software I work with on either machine.
Comments are gone for now, though Disqus may be an option later if I want them
back.

Hopefully this is the start of a simpler, more focused blog. I still have a
little tweaking to do, but hopefully all the permalinks update correctly.

*Edit:* I'm also moving the RSS feed back to my server. It was on FeedBurner for
ages, but I don't use the stats and I'm afraid it's going to follow Google
Reader sooner or later.

*Edit2:* There were a few broken urls that have been fixed now. Some images
appear to be broken still though.

*Edit3:* Already moved on to a new platform: [Hexo][3]. It can read the same
markdown files as Octopress and I like the theming process better.

[3]: <http://zespia.tw/hexo/>
