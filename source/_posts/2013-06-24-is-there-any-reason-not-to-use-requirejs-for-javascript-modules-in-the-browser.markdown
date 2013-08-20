---
author: David Hogue
comments: true
date: 2013-06-24 14:39:04+00:00
layout: post
slug: is-there-any-reason-not-to-use-requirejs-for-javascript-modules-in-the-browser
title: Is there any reason not to use RequireJS for JavaScript modules in the browser?
wordpress_id: 1266
categories:
- Software Development
tags:
- javascript
- requirejs
---

I started using [RequireJS](http://requirejs.org/) on some new smaller projects a while ago. If you don't know, it is a tool for loading JavaScript files that are structured as modules as well as loading dependencies in the correct order. It does some other fancy things like optionally loading files after the page is loaded, plugins, and other areas I haven't explored yet.

To me the biggest feature is the module format and dependency tracking. JavaScript has never really had any module system or method for referencing other files. The best that we could do back in the day was put all the script tags in the HTML in the right order and avoid writing code that created globals.

Now I'm trying to make some inroads on converting a large project's scripts over to modules. 

With the number of files and size of each one, it's become difficult to extend them. It's not even easy to pull a script or two out into a unit test harness at this point because it takes a while to sort out what each file assumes is already on the page.

I'm thinking that converting the existing project over will modularize the code, maybe even split up some of the biggest files, and make it much easier to move forward with changes in the future. It'll take a little time to refactor the code, it will really save us some time in the future. (I hope.)
