---
author: David Hogue
comments: true
date: 2012-11-28 18:38:09+00:00
layout: post
slug: selenium-page-objects-for-an-ajax-admin-page
title: Selenium Page Objects for an AJAX Admin Page
wordpress_id: 1142
categories:
- Software Development
tags:
- patterns
- selenium
- tests
---

So before I begin, I wanted to mention something about how I haven't been keeping this site up to date much lately. And I think part of that has to do with getting tired of code and getting burned out on putting in development time after hours. I used to have a lot of free time and energy for that, but now it feels like I'm not learning much new and interesting. It gets tiring looking at the same tools and languages all the time. I'm just working day to day and trying to get some enthusiasm back. Hopefully writing more will get me looking at some new stuff and get me some practice organizing my thoughts.



### On to the tests


Having said that, I'm spending a lot of time with Selenium lately and I love how much it's grown up since the early days. I'm using Selenium WebDriver (aka Selenium 2.0) and Selenium Grid in C# with NUnit.

The tests I inherited were doing okay, but some were needlessly complex. Often looping through elements (which got very slow by the way) and not cleaning up after themselves. I cleaned up lot of that complexity with better selectors trimming out code that wasn't really needed. Even after that many tests were still long and repetitive due to the complexity of working with a real application using AJAX and backed by a SQL database.



### Page Objects


That's when I happened on this pattern called Page Objects. Essentially the idea is to create a class representing your page with methods to interact with that specific page. You might create properties for page's textboxes and a Submit() function to click the submit button. This Page Object Class would contain a reference to the driver instead of the test. Before I found this pattern, I had started pulling common operations out to functions that lived inside the test's class.

Well I started experimenting with the idea, but my application under test uses one html page for admin. Data is loaded in dynamically and the user can navigate to other parts of admin by clicking tabs. So I came up with something that makes my test code look a bit like this:


    
    
    var users = admin.GoToUsers();
    var roles = users.GoToRoles();
    roles.AddNewRole("test");
    
    // Alternatively as a single line:
    admin.GoToUsers().GoToRoles().AddNewRole("test");
    



I was going for a fluent api with this, where I could chain function calls one after another. Each function like GoToUsers() above is a few lines looking something like this:


    
    
    public AdminUsers GoToUsers()
    {
        Driver.FindElement(By.Id("usersTab")).Click();
    
        // Common utility function that waits until a loading image is gone from the page.
        WaitForAjax();
    
        return new AdminUsers(Driver);
    }
    



It does just a little bit of work and then returns a new object. The test can use this new object to navigate farther into the page.

So far my implementations all assume that if you have a reference to the object, that you've already opened the page and navigated to the right area.



### Thoughts



I think these utility functions/classes help keep the tests readable even if you don't know anything about the page or much about Selenium at all. And I'm hoping once there is enough to cover most of the page, that it'll be a simple process for anyone to follow the examples already there and add another one if it's missing.

I'm still trying this out and only a handful of tests are using it now. I think it has a lot of potential. Do you have any experience with Page Objects in your tests? Or do you see any potential issues with the direction I'm pushing these in?
