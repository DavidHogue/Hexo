---
author: David Hogue
comments: false
date: 2007-03-09 04:26:32+00:00
layout: post
slug: an-example-of-the-proxy-design-pattern
title: An Example of the Proxy Design Pattern
wordpress_id: 199
categories:
- Software Development
tags:
- old-blog
---

As I sit here waiting for Visual Studio to reinstallVisual Studio 2005 Service Pack 1 takes so long to install.  I mean, come on, what's it need to do other than copy a few hundred megs from one spot on my drive to another?  Why is it so damn slow?  It's been half an hour and still "Gathering required information...", I thought I'd write up a recent experience with the proxy design pattern.

A little while ago I was working with a class that I wanted to make disposable so that I could "reset" the system.  I wanted to do this for two reasons: 



	
  1. to speed up the unit tests and stop some cross-test interference

	
  2. so that the user of the app could change a setting without restarting



Here is the code I started withrewritten from memory, not actual production code (hopefully obvious, but thought I'd note it anyway):


    
    public class Widget
    {
        private string name;
        public string Name
        {
            get { return name; }
            set { name = value; }
        }
    
        public void SomeMethod()
        {
            //...
        }
    
        public string SomeOtherMethod()
        {
            //...
        }
    }
    
    public class WidgetService
    {
        private static Widget defaultWidget;
    
        public static Widget DefaultWidget()
        {
            LoadWidgets();
            return defaultWidget;
        }
    
        private static void LoadWidgets()
        {
            if(defaultWidget != null)
                return;
            //...
        }
    }



![The original code](http://vorpal.cc/blog/wp-content/uploads/2007/03/proxybefore.png)

Now, the problem was: many objects all over the system had a reference to the default widget.  They would call DefaultWidget it once and just hold on to it forever.  This meant that even if I had DefaultWidget return a new widget, the old one would be out there somewhere still.  It would be a lot of work to change all that code.  Plus, I couldn't prevent new code from holding on to the widget.

After thinking about it for a while I thought: maybe if I can control the references to the widget, I can replace it.  How do I do that?  Easy, don't give anyone the widget.  Ok, that won't quite work.  How about I give them a widget that just passes the calls through to my widget that I want to replace?

That sounded familiar.  Maybe there's a pattern for something like that.  I googled, but found nothing.

The next day...

Maybe I'm searching with the wrong words.  What I'm really doing is proxying the calls through to my real object.  Hey, there's a [proxy pattern](http://www.dofactory.com/Patterns/PatternProxy.aspx).  That's what I was looking for.  I knew I'd seen this before.

Below is the updated code with the proxy.  It's not exactly the same as the proxy from dofactory, but that's why it's called a pattern right?


    
    public class Widget : IDisposable
    {
        private string name;
        // methods and properties are now marked virtual
        public virtual string Name
        {
            get { return name; }
            set { name = value; }
        }
    
        public virtual void SomeMethod()
        {
            //...
        }
    
        public virtual string SomeOtherMethod()
        {
            //...
        }
    
        public void Dispose()
        {
            // do my cleanup
        }
    }
    
    public class WidgetService
    {
        private static WidgetProxy proxy = new WidgetProxy();
    
        public static Widget DefaultWidget()
        {
            LoadWidgets();
            // return the proxy as the default, the client code won't know the difference
            return proxy;
        }
    
        private static void LoadWidgets()
        {
            if(proxy.Target != null)
                return;
    
            Widget defaultWidget;
            //...
            proxy.Target = defaultWidget;
        }
    
        public static void ResetWidgets()
        {
            Widget oldTarget = proxy.Target;
            proxy.Target = null;
            oldTarget.Dispose();
            LoadWidgets();
        }
    
        private class WidgetProxy : Widget
        {
            private Widget target;    // the real widget
            public Widget Target
            {
                get { return target; }
                set { target = value; }
            }
    
            // just pass all the calls through to the target
            public override string Name
            {
                get { return target.Name; }
                set { target.Name = value; }
            }
    
            public override void SomeMethod()
            {
                target.SomeMethod();
            }
    
            public virtual string SomeOtherMethod()
            {
                target.SomeOtherMethod();
            }
        }
    }



![After the proxy](http://vorpal.cc/blog/wp-content/uploads/2007/03/proxyafter.png)

The great thing about this is that I didn't have to change _any_ client code.  In fact the public interface hardly changed: I made the Widget implement IDisposable and made the methods virtual.

Now the only thing that has a reference to the real widget is the proxy and the proxy is hidden from the rest of the system.  That means I can replace the proxy's target whenever I want and don't have to worry about what has a reference to it.

I ran all the tests, everything worked and I haven't had any problems with it since.  A nice easy solution to what could have been large problem.
