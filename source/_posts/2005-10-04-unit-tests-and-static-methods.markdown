---
author: David Hogue
comments: false
date: 2005-10-04 08:48:41+00:00
layout: post
slug: unit-tests-and-static-methods
title: Unit Tests and Static Methods
wordpress_id: 288
categories:
- Software Development
tags:
- old-blog
---

I am trying to add unit tests to some previously untested code.  Said code depends on these utility classes that consist entirely of static methods.  These methods do things like talk to the database, get configuration settings, etc.  The architecture is really much more procedural than object oriented. I am using [NUnit](http://www.nunit.org/) and [ NMock](http://www.nmock.org/).

The particular class I am working on depends on six or seven of these utility classes.  Since I want to isolate my test, I am trying to create a mock utility class.  My problem is that I don't know the best way to do this.  My options are:





  1. Add a non-static method to the utility for each method I need.  Then make an interface that matches and a mock oject.


  2. Create an interface with the methods I need and create a wrapper class that implements this interface and calls the static methods.



I don't like option 1 because I have to think up a new name for the same method and it clutters up the utility for the rest of the application.  Option 2 has some issues with it too.  Do I make an interface for each utility class I need or one interface with just the functions the class to be tested needs?  Where does the class get a reference to the interface?  I could pass it in to the constructor, but passing 6 or 7 arguments really bulks up the code.  I tried to make a [registry](http://www.martinfowler.com/eaaCatalog/registry.html) class that would hold a reference to each wrapper, but that also grew unweildy.

I'm starting to think that I need a single interface that only this class will use.  There will be the interface, a simple implementation that calls the static methods, and a constructor that takes an instance of the interface.  This lets me test the class with the least impact on the rest of the system.  The only thing that bugs me is that the interface is only used by this one class.  On the next class I will have to create another interface.

Option 1 looks like this:

    
    interface IFooUtil
    {
    	void DoSomethingWrapper();
    }
    
    class FooUtility: IFooUtil
    {
    	public static void DoSomething()
    	{}
    	public void DoSomethingWrapper()
    	{
    		DoSomething();
    	}
    }
    
    interface IBarUtil
    {
    	public int GetSomethingWrapper()
    }
    
    class BarUtility: IBarUtil
    {
    	public int GetSomething()
    	{}
    	public int GetSomethingWrapper()
    	{
    		return GetSomething();
    	}
    }



Option 2 looks like:

    
    interface IFooUtil
    {
    	void DoSomethingWrapper();
    }
    
    class FooUtility
    {
    	public static void DoSomething()
    	{}
    }
    
    class FooHelper : IFooUtil
    {
    	public void DoSomethingWrapper()
    	{
    		FooUtility.DoSomething();
    	}
    }
    
    interface IBarUtil
    {
    	public int GetSomethingWrapper()
    }
    
    class BarUtility
    {
    	public int GetSomething()
    	{}
    }
    
    class BarHelper : IBarUtil
    {
    	public int GetSomethingWrapper()
    	{
    		return BarUtility.GetSomething();
    	}
    }



or

    
    class FooUtility
    {
    	public static void DoSomething()
    	{}
    }
    
    class BarUtility
    {
    	public int GetSomething()
    	{}
    }
    
    interface IClassUtils
    {
    	void DoSomethingWrapper();
    	int GetSomethingWrapper()
    }
    
    class ClassUtilWrapper : IFooUtil
    {
    	public void DoSomethingWrapper()
    	{
    		FooUtility.DoSomething();
    	}
    	public int GetSomethingWrapper()
    	{
    		return BarUtility.GetSomething();
    	}
    }
