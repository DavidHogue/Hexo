---
author: David Hogue
comments: false
date: 2006-07-23 19:01:18+00:00
layout: post
slug: why-does-vbnet-let-you-do-this
title: Why does vb.net let you do this?
wordpress_id: 354
categories:
- Software Development
tags:
- old-blog
---

What possible use could there be for this?  It just makes things harder and more confusing.  Code is often confusing enough without writing classes like this:


    
    Public Interface IExample
        Function SomeFunction() As String
    End Interface
    
    Public Class Confusing
        Implements IExample
        Public Function SomeFunction() As String
            Return "In Confusing.SomeFunction"
        End Function
    
        Public Function Huh() As String Implements IExample.SomeFunction
            Return "In Confusing.Huh"
        End Function
    End Class
    
    Public Class Program
        Public Shared Sub Main()
            Dim instance As IExample
            instance = New Confusing()
            Console.WriteLine("instance.SomeFunction: {0}", instance.SomeFunction)
            Console.WriteLine("CType(instance, Confusing).SomeFunction: {0}", CType(instance, Confusing).SomeFunction)
        End Sub
    End Class



This prints instance.SomeFunction: In Confusing.SomeFunction, CType(instance, Confusing).SomeFunction: In Confusing.Huh.  Notice that the method that actually gets called differs depending on the type that you cast to.

I guess it could be used if your class implements two interfaces that happen to have methods or properties with the same name.  However, in that case I think you'd be better off with two classes.  One could be an [adapter](http://www.dofactory.com/Patterns/PatternAdapter.aspx) that implements the second interface and calls the first if necessary.

How I usually see this happening is if I have an existing interface and classes.  Then I go and rename some method in the interface or class.  Then I forget to change the name of the class method to match the name of the interface method.  Then I get odd bugs because the code that uses the class isn't calling the method that it says it is calling.

I much prefer the [C#/Java way of implementing an interface](http://msdn2.microsoft.com/en-us/library/ms173156.aspx) where you don't have to specify what interface and method every method you write is implementing.  It just uses the name of the method.  Much less typing, much cleaner, easier to read, easier to debug, and harder to make mistakes.  I know you can use the [InterfaceName.MethodName syntax](http://msdn2.microsoft.com/en-us/library/44a9ty12.aspx), but I have mostly the same opinion of that.
