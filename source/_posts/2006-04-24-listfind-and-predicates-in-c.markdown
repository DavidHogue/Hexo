---
author: David Hogue
comments: false
date: 2006-04-24 15:40:16+00:00
layout: post
slug: listfind-and-predicates-in-c
title: List.Find() and Predicates in C#
wordpress_id: 346
categories:
- Software Development
tags:
- old-blog
---

I've been finding all kinds of cool stuff in .net 2.0 that I didn't know about.  Today I discovered predicates.

I'm not sure how to explain it so I'll just give an example.  I have a List of Tasks and I want to return the task with the selected id.  Normally I would write a loop like the one below:


    
    int id = int.Parse(taskList.SelectedValue);
    foreach (Task t in AllTasks)
    {
    	if (t.Id == id)
    		return t;
    }



It's a common enough operation and I have written several loops just like it.  I never really enjoy writing the above code.  I would probably create a TaskCollection class and move the above loop into it eventually.

Now with .net 2.0 I can write the same thing in two lines:


    
    int id = int.Parse(taskList.SelectedValue);
    return AllTasks.Find(delegate(Task t) { return t.Id == id; });



And at first glance I like this _a lot_ better.  I'm a little concerned that this functionality could be abused to write some very ugly code.  I still think it should be moved to my TaskCollection class at some point, but I'm less likely to do so now because it is only one line.
