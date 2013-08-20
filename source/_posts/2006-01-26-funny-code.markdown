---
author: David Hogue
comments: false
date: 2006-01-26 06:10:57+00:00
layout: post
slug: funny-code
title: Funny Code
wordpress_id: 330
categories:
- Software Development
tags:
- old-blog
---

I followed some compiler warnings in a larger project and found a few interesting items.


    
    Dim dataset As DataSet
    
    If Not dataset Is Nothing
    	[code that works with dataset]
    End If




    
    Public Function SomeFunction(ByVal name As String) As String
    	Dim result As String
    	For Each item As CustomObject in someArray
    		If item.Name = name Then
    			result = item.Name
    			Exit For
    		End If
    	End For
    	Return result
    End Function



The first is just silly.  The second only returns exactly what you pass in.  And if you're thinking maybe it is to validate that an item exists: it isn't.  The results of this function are not checked for Nothing, just used later in the code which will crash if it is nothing.

Funny thing is I think I am responsible for the first and at least partially responsible for the second.  (In the first, dataset used to be a parameter to the function)

_Code has been rewritten from memory and slightly modified to avoid any issues in posting it._
