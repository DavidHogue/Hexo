---
author: David Hogue
comments: false
date: 2007-11-16 18:48:22+00:00
layout: post
slug: 2-hours-with-castle-monorail
title: 2 Hours With Castle MonoRail
wordpress_id: 241
categories:
- Software Development
tags:
- castle
- monorail
- old-blog
---

[MonoRail](http://www.castleproject.org/monorail/index.html) is one of those frameworks that I've been watching for a while, but I've never spent the time to actually dig in and start messing with it. MonoRail, if you haven't heard, is a MVC framework for ASP.NET web applications, similar to [Ruby on Rails](http://www.rubyonrails.org/). Microsoft is also working on their own ASP.NET MVC framework, but it's not available yet (or it wasn't back when I wrote this.)

A little while ago I spent a couple hours with it, just reading the tutorial and trying stuff out. I figured I could make an interesting post on my experience with it. The following is just my rough notes from that. Some might even call it live blogging.



#### MonoRail


I started by downloading and running the msi installer of rc3.

I created a MonoRail app through the Visual Studio wizard as the [documentation](http://www.castleproject.org/monorail/gettingstarted/index.html) suggested. It gave me some NUnit tests, they ran quickly in Resharper's test runner. Hitting F5 started Visual Studio's server and brought me to a nice looking page offering examples and documentation.

Urls are interesting. It redirects me to /home/index.castle. It seems to do this in the generated Default.aspx. This implies that I might be able to throw some webforms pages into a MonoRail site. *.castle is mapped to MonoRailHttpHandlerFactory in the web.config. Looks like standardish, somewhat advanced, asp.net stuff so far. I'd probably have to add the .castle mapping in IIS.

Images, stylesheets, and JavaScript are in a folder called Content; seems to load the same as files any old ASP.NET site.

I'm looking at the rendered html and trying to figure out where it came from. There's a Views folder, inside that a Home folder and an Index.vm file. Index.vm seems to have a few snippets, but not the main bulk of the html. Ah, layouts/default.vm has a lot in it. There's some variable replacement going on $!{title} and $siteroot, I'll have to look up the syntax later. Hmm, there's a $!scripts in the layout and a #capturefor(scripts) in the home view. This is all probably NVelocity stuff. Just found rescue views, nice!

On to the login controller... I can see it works and how the controller code gives the form values to the view through a PropertyBag. How's it decide to show the form or the result? The form's action = /Login/Authenticate.caste, the form page is /Login/index.castle. Ah, and there's two different views.

Just noticed that Visual Studio tabs are confusing when you have three Index.vms open. I just noticed that it can build links to the various pages through $Url.Link(...).

The idea of the controllers seems familiar. I've taken a look at it before and I've tried to use the [MVP pattern](http://msdn.microsoft.com/msdnmag/issues/06/08/DesignPatterns/default.aspx) with webforms in a few projects. I wonder if the url is tied to the controller? Is there a way to separate it? I could live with it for an internal site, but I might want more control for a public site. For example the url of this post has a lot of info in it that I think might not be in the MonoRail urls. We'll see.

I really like having more control over the html than webforms gives you.

OK, processing forms, passing variables back to the view and then the browser, got it. Not sure where to go now. Ooh! DataBinding... OK, so it's different than webforms databind. It binds fields from a form to properties on a class, very nice.

The docs then go on to ActiveRecord. I've already used ActiveRecord, so I'm going to skip it. That's it for the getting started documentation. I think I might move on to Windsor.



#### Windsor


[Windsor](http://www.castleproject.org/container/index.html) while not part of MonoRail is related because they are both part of the Castle Project.Windsor is an [inversion of control](http://martinfowler.com/articles/injection.html) container.

Getting started part 2 & 3 are not done yet. It'd be nice if I didn't have to click the link to find that out... Anyway I've tried to use IoC before, I used [Spring.net](http://www.springframework.net/) to configure a project, and I thought I understood IoC, but I'm not so sure I really did.

The simple example of Windsor registering a form and getting it was neat, but doesn't show me how or why I would want this. Separation of concerns: nice and all, but can't I do that without a container? Just create my objects one by one, passing them into the constructor/setting properties myself. Does this get more useful as I get more classes? Where is it practical? If I only have 5 classes that interact, probably not. What about 50 classes and each takes a couple parameters? Assuming I'm not using the configuration features (yet).

When you add configuration, it seems like a handy configuration utility, but I know that isn't the main purpose of IoC



#### Wrapping up


Anyway, that's all the time I have for this. Hopefully someone will find this interesting or at least I can reread it whenever I attempt to use these libraries in a future project. They're interesting, well documented, and appear easy to use. I don't have a specific need for either, so I'll wait. I don't want to force them into an existing project just because they are cool. I'll wait until I need them.

Returning to the site just now, I noticed a "Using" link in the header. It looks like there is a lot of good info in here. Maybe it could be linked to from some of the documentation. Maybe a see here for some other useful info?
