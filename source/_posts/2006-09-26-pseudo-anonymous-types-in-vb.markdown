---
author: David Hogue
comments: false
date: 2006-09-26 17:55:31+00:00
layout: post
slug: pseudo-anonymous-types-in-vb
title: Pseudo-Nullable Types in VB?
wordpress_id: 163
categories:
- Software Development
tags:
- old-blog
---

I just found out that in vb I can set value types (DateTime and Integer) to Nothing.  I can also test for equality with Nothing.

The following prints out "d is nothing / i is nothing":


    
    Public Shared Sub Main()
        Dim d As DateTime = Nothing
        Dim i As Integer = Nothing
        If d = Nothing Then
            Console.WriteLine("d is nothing")
        End If
        If i = Nothing Then
            Console.WriteLine("i is nothing")
        End If
    End Sub



Reflectoring the compiled code gave me this:


    
    Public Shared Sub Main()
          Dim time1 As DateTime = New DateTime
          Dim num1 As Integer = 0
          If (DateTime.Compare(time1, DateTime.MinValue) = 0) Then
                Console.WriteLine("d is nothing")
          End If
          If (num1 = 0) Then
                Console.WriteLine("i is nothing")
          End If
    End Sub



So, they aren't really nullable.  I guess it is just another "feature" of vb.
