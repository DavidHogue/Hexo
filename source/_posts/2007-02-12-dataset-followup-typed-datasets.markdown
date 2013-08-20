---
author: David Hogue
comments: false
date: 2007-02-12 22:58:05+00:00
layout: post
slug: dataset-followup-typed-datasets
title: 'DataSet Followup: Typed DataSets'
wordpress_id: 191
categories:
- Software Development
tags:
- old-blog
---

It was suggested that I make my example DataSets in [this post](http://vorpal.cc/blog/category/development/c-sharp/good-dataset-bad-dataset.html) into typed DataSets.  

I haven't actually done much with typed DataSets, so I thought I'd go create one.  It was easy enough to create one with the Visual Studio designer.  Here's a small chunk of code that uses my DataSet:


    
    static void Main()
    {
        DataSet1 data = new DataSet1();
        data.User.AddUserRow(1, "bender", "00100100", "Bender", "Rodriguez");
        data.User.AddUserRow(2, "professor", "Pazuzu", "Hubert", "Farnsworth");
        Console.WriteLine(data.User.FindByid(1));
    }



While it is an improvement, I still think plain old objects beat datasets in many situations.  

Going back to my example with logging in a user, which of these three options would you like to work with?  (The example is not ideal: the code is in the page and tied directly to asp.net controls; it reveals to potential attackers whether a username exists...)


    
    // untyped DataSet
    if(!UserUtility.CheckPassword(data, userId, password.Text))
        error.Text = "Invalid password for user " + data.Tables[0].Select("userId = " + userId)[0]["userName"];
    
    // typed DataSet
    if(!UserUtility.CheckPassword(data, userId, password.Text))
        error.Text = "Invalid password for user " + data.User.FindByid(userId).userName;
    
    // plain old object
    if(!user.CheckPassword(password.Text))
        error.Text = "Invalid password for user " + user.UserName;



Some places DataSets (typed or untyped) work great: simple reporting, databinding, etc.  It would be silly to create a bunch of dumb objects just to hold data that is queried from a sql and written to a table.

[Adi](http://www.newoutput.com/) left a comment informing me that using DataSets isn't a good practice in SOA because they generate a ton of XML.  This definitely makes sense to me.  If we had more of an infrastructure with the webservices moving away from DataSets would probably be a good idea.  In this case the webservice was put up because the database server is on a different network from the web server and we needed a quick way to get data to the users.  Also, at least one of the two large data sets is compressed before it is sent.

I think they work well enough in quick cheap projects, but can quickly become a problem in larger codebases that need to last.
