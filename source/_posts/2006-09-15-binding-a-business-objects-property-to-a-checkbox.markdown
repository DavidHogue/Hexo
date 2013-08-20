---
author: David Hogue
comments: false
date: 2006-09-15 20:34:13+00:00
layout: post
slug: binding-a-business-objects-property-to-a-checkbox
title: Binding a Business Object's Property to a Checkbox
wordpress_id: 159
categories:
- Software Development
tags:
- old-blog
---

At work I am currently developing a windows forms application that makes heavy use of custom business objects and data binding.

What I was trying to do was bind a custom control to these objects.  The control behaves similar to a checkbox, when clicked it's state changes from locked to unlocked.  I have several of these controls and wanted to bind boolean properties on my objects to them.

So, not knowing how data binding works in .net 2.0 with windows forms, I created a test project.  ([zip available.](http://vorpal.cc/blog/wp-content/uploads/2006/09/checkboxbinding.zip))  The project is very small and has lots of Debug.WriteLines.

My actual binding consists of a single line: 

    
    checkBox1.DataBindings.Add("Checked", data, "Enabled");



Here's the order of events that I found:




  
  * Click the checkbox
    
      
    1. OnCheckedChanged

      
    2. OnCheckStateChanged

    
  

  
  * Tab off the checkbox
    
      
    1. OnValidating

      
    2. set property to checkbox status

      
    3. get property

      
    4. get property

      
    5. OnValidated

  

  
  * Change the property when the object implements [INotifyPropertyChanged](http://msdn2.microsoft.com/en-us/library/system.componentmodel.inotifypropertychanged.aspx)
    
      
    1. set property

      
    2. get property

      
    3. OnCheckedChanged

      
    4. OnCheckStateChanged

    
  

  
  * Change the property without INotifyPropertyChanged
    
      
    1. set property

    
  



This tells me a couple things: 1) Without INotifyPropertyChanged my control won't show the new object's state, and 2) the object isn't updated until focus leaves the control (or it raises a OnValidating event)

With [Reflector](http://www.aisto.com/roeder/dotnet/) I found two methods in the System.Windows.Forms.Binding class called Target_PropertyChanged and Target_Validate.  These two methods seem to support my findings.  I also discovered that the control doesn't use it's bindings directly.  The binding subscribes to these two events to do all it's stuff.

Data binding is seeming a little less like voodoo after this.
