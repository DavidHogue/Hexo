---
author: David Hogue
comments: false
date: 2007-11-12 21:05:24+00:00
layout: post
slug: avoiding-the-startup-time-for-webservice-xml-serialization
title: Avoiding the startup time for webservice xml serialization
wordpress_id: 239
categories:
- Software Development
tags:
- old-blog
- webservice
- xml
---

#### The short version



In the build tab of a project's properties is an option called "Generate serialization assembly", turn it to "On" to theoretically improve performance.



#### The long version



Recently I've been working on speeding up a web application that depends heavily on a huge webservice: 884 "operations" are supported[Firebug](http://getfirebug.com/) + document.getElementsByTagName("li").length, the wsdl is 2 megabytes.  Startup takes several minutes before anything happens.  And it is mostly the startup time causing problems, things go smoothly after that.

While trying to improve things I found this single line causing most of the delay: `_myStore = new WebServices3();`  And it was only the first time that the webservice was initialized that the delay happened.

I started searching and ran across a knowledgebase article explaining how to create an XmlSerializers assembly.  Apparently the XmlSerialization process usually generates code at runtime and this can take a while.  The article explained how to pregenerate this code to save startup time later.  I tried it, it didn't seem to help all that much and it was a pain to fit into the build process.

I later found [a page on MarkItUp about SGen.exe](http://markitup.com/Posts/Post.aspx?postId=e300699e-355d-4b04-9e6c-c43a2826faee).  It was a new feature in .net 2.0 that I remember hearing about.  Then I found [this post on kiwidude.com about how Visual Studio didn't call sgen correctly for him](http://www.kiwidude.com/blog/2007/02/vs2005-when-sgen-doesnt-work.html).  

I never noticed it before (maybe because I had to scroll down the properties page), but there was a simple drop down in Visual Studio for this.  Switching it from Auto to On built the assembly automatically!

![XmlSerialization](http://davidhogue.com/wp-uploads/2007/11/xmlserialization.png)



#### The end



Once enabled, build time became much longer and startup times were a little better.  The change wasn't as dramatic as I had hoped.  I think from here I'm going to create a much smaller, specialized web service since I have access to the web service machine and we're only using a handful of the 800 methods available.
