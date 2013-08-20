---
author: David Hogue
comments: false
date: 2006-02-18 23:34:00+00:00
layout: post
slug: switching-a-webapp-to-net-20
title: Switching a WebApp to .net 2.0
wordpress_id: 337
categories:
- Software Development
tags:
- old-blog
---

With .net 2.0 out now, [we](http://www.smartz.com) are migrating some of our vs2003 web projects the new vs2005 model.  Here are some notes from my conversion of a fairly large project.  Hopefully someone out there will find this useful.


#### Main process





	
  1. Remove the project from the solution

	
  2. Delete the .vbproj file (or move it somewhere else)

	
  3. Add a web site to solution and select the folder where the .vbproj was

	
  4. Add references (there are 4 types of references now: GAC references in the web.config, file references in the bin folder with a .refresh file, project references in the solution, and dlls that you manually copy to the bin folder)

	
  5. Change codebehind="foo.aspx.vb" to codefile="foo.aspx.vb"

	
  6. Remove namespaces from code behind files change inherits="SmartSolutions.Bar.Foo" to inherits="Foo" (optional)

	
  7. Move non-codebehind classes to App_Code

	
  8. Build and make sure things work correctly




#### Optional steps





	
  * You can add the namespaces back (I removed them just to make the process a little easier. There is no default namespace for the project)

	
  * Add a deployment project (you need to [download the beta](http://msdn.microsoft.com/asp.net/reference/infrastructure/wdp/default.aspx) from Microsoft)

	
  * Setup a NAnt script


