---
author: David Hogue
comments: false
date: 2006-08-04 04:58:49+00:00
layout: post
slug: unit-testing-winforms-20-databinding
title: Unit Testing WinForms 2.0 Databinding
wordpress_id: 139
categories:
- Software Development
tags:
- old-blog
---

In a some recent code I was databinding a custom business object to simple controls like TextBoxes and Labels.  While I'm not a huge fan of databinding, I am a huge fan of unit testing and TDD.  

I would usually prefer to set and get the Text property on my own, but we are using databinding pretty heavily in this project.  It made sense to do it this way for consistency's sake.

It is also an area of .net that I am not familiar with.  As far as I know there is some magic voodoo going on.  I thought using databinding from nUnit would be a good learning experience.

So my initial test looked something like this:


    
    [Test ()] _
    Public Sub ReadsPartNumber
        ' arrange
        Dim part As New Part()
        part.PartNumber = "1234"
        Dim panel As New PartPanel()
    
        ' act
        txtPartNumber.DataBindings.Add("Text", part, "PartNumber")
    
        ' assert
        Assert.AreEqual("1234", panel.txtPartNumber.Text)
    End Sub



and that didn't work.  That failed with a expected '1234', but was null message.

Huh, why isn't it set?  No idea; so I ask a few coworkers to take a look at it.  One suggested maybe databinding doesn't work if the control isn't visible (but I want to test it from nUnit!).  Other than that they saw nothing wrong with it.  Off to Google!

I found CodeBetter.Com article: [Writing unit tests for Windows Forms to test DataBinding](http://tableadapter.codebetter.com/blogs/ranjan.sakalley/archive/2006/04/16/Unit_test_for_Databinding.aspx).  Perfect! Almost the problem I have except he is writing data from the control to the object where I am reading.  

It might still work:


    
    [Test ()] _
    Public Sub ReadsPartNumber
        ' arrange
        Dim part As New Part()
        part.PartNumber = "1234"
        Dim panel As New PartPanel()
    
        ' act
        Dim b As Binding = txtPartNumber.DataBindings.Add("Text", part, "PartNumber")
        b.ReadValue()
    
        ' assert
        Assert.AreEqual("1234", panel.txtPartNumber.Text)
    End Sub



No dice.  At this point I got frustrated and found something else to work on.

When I came back I started looking through the Binding class and found an IsBinding property.  It returned false in my test.  Unfortunately it's read only.  I tried a few different things here: panel.Show(), panel.Focus(), anything that might work.

Then I thought "What if I put the panel in a form and show() it?"


    
    [Test ()] _
    Public Sub ReadsPartNumber
        ' arrange
        Dim part As New Part()
        part.PartNumber = "1234"
        Dim panel As New PartPanel()
        Dim form As New Form()
        form.Controls.Add(panel)
        form.Show()
    
        ' act
        Dim b As Binding = txtPartNumber.DataBindings.Add("Text", part, "PartNumber")
    
        ' assert
        Assert.AreEqual("1234", panel.txtPartNumber.Text)
    End Sub



It worked!  After the test was working I pulled most of the "arrange" part out into setup or a ShowControl function.  I spent most of the day learning databinding and trying to get this to work.  Very frustrating.

Moral of the story: listen to your coworkers.
