---
author: David Hogue
comments: false
date: 2007-02-07 02:02:20+00:00
layout: post
slug: good-dataset-bad-dataset
title: Good DataSet, Bad DataSet
wordpress_id: 189
categories:
- Software Development
tags:
- old-blog
---

I recently had to work on an older project that used DataSets for almost all it's in memory data.  The code used to look like this:


    
    public void Page_Load(object Sender, EventArgs e)
    {
        SomeWebService service = new SomeWebService();
        DataSet data = service.GetData(userId);
        grid.DataSource = data;
        grid.DataBind();
    }



I needed to change it to call the service multiple times, combine all the data, and sort it:


    
    public void Page_Load(object Sender, EventArgs e)
    {
        SomeWebService service = new SomeWebService();
        DataSet data = new DataSet();
        foreach(int userId in userIds)
            data.Merge(service.GetData());
        grid.DefaultView.Sort = "date";
        grid.DataSource = data;
        grid.DataBind();
    }



Surprisingly this actually worked.  DataSets worked really well here because it was a reporting application with lots of tabular data that used webservices and datagrids.  This is what DataSets were designed for.

I have seen many other times where a DataSet is used instead of a collection of objects and the result is just ugly.  Sometimes it ends up like this:


    
    public void Page_Load(object Sender, EventArgs e)
    {
        SomeWebService service = new SomeWebService();
        DataSet data = service.GetData();
        if(UserUtility.CheckPassword(data, userId, password.Text))
            error.Text = "Invalid password for user " + data.Tables[0].Select("userId = " + userId)[0]["userName"]
    }



Code dealing with users can't go in the User class because it doesn't exist, so a UserUtility class with all static methods is created.  The code often makes a lot of assumptions: the number of tables, the names of fields, etc.  These assumptions could easily be broken.  the code is very fragile.  If there was a User class in this case you would get better compile time errors, the code would be cleaner and better organized, and would probably be more reusable.

DataSets have their place and they work well, just learn to recognize when a DataSet is the wrong solution to a problem.  It seems like a lot of technologies in the .net world are pushed way past what they were designed to do and I'm not sure why that is.  Is Microsoft to blame?  The developers?  The platform?  Marketing?  Who knows.

If all you have is a hammer...
