---
author: David Hogue
comments: false
date: 2007-01-11 05:03:43+00:00
layout: post
slug: exceptions-exceptions-exceptions
title: Exceptions, Exceptions, Exceptions
wordpress_id: 184
categories:
- Software Development
tags:
- old-blog
---

I know this is old, but I keep running across code that uses exceptions in weird, wrong, or just plain funky ways.  I'm putting this up in the hopes that it will make a small difference for someone out there.  

I guess it's sort of a list of exception anti-patterns.  

Some not so exceptional exception handling.  Exception handling that should be the exception...  ok, so that's enough of that.



#### The timebomb







    
    try {
        //...
    } catch {
    }





    
    Try
        '...
    Catch
    End Try





These cause some of the most aggravating bugs I've ever seen.  When a program silently fails without any signs it can continue failing for months before anyone notices.  All the while corrupting users, losing orders, etc.  Exceptions caught in this way can be very hard to track down because you have no _idea_ where the problem could be.  

If I find code like this I immediately add at least a log entry, if not completely remove the try/catch.

This also causes problems with unit tests.  Not because they fail or take forever, but because the tests pass when there really is a problem.




#### The catch all







    
    try {
        //...
    } catch(Exception ex) {
        return false;
    }





    
    Try
        '...
    Catch ex As Exception
        Return False;
    End Try





Ideally you should catch a specific type of exception.  For example: catch an ArgumentException instead of an Exception.  If you catch Exception or don't include an exception type then you will catch exceptions you are not expecting.  

Sure an SmtpException might need to be trapped so you can tell the user that they can't email the data right now.  But what if the exception is a NullReferenceException because you got passed some bad data?  You wouldn't want to tell the user that their email isn't setup correctly in this case.

Sometimes this is valid.  For example if you have a windows service that batch processes data in the middle of the night you might put a try catch around each item in the batch.  That way a single bad record won't kill the whole process.  But please log the exceptions and have it email someone.



#### The dreaded MessageBox







    
    try {
        //...
    } catch(WebException ex) {
        MessageBox.Show("Couldn't open file");
    }





    
    Try
        '...
    Catch ex As WebException
        MessageBox.Show("Couldn't open file")
    End Try





This wreaks havoc with unit tests.  Nothing worse than having your build server sit there for hours only to find out it's waiting for someone to click OK in a failed test.

It's also bad practice to open up a MessageBox like this from a library or other code that is not in the presentation level.  What if the code needs to be reused and put into a web application or a windows service?



#### Unnecessary catching







    
    try {
        File.Open(path);
    } catch(IOException ex) {
        return "Could not open the file " + path;
    }





    
    Try
        File.Open(path)
    Catch ex As IOException
        Return "Could not open the file " + path
    End Try





This is just silly and more often than not just programmer laziness.  Most exceptions can be prevented.  In this case the code monkey could have used a if(File.Exists(path)) first.  In theory exception prevention will be faster in many cases as exceptions are generally slow. (but slow is very relative)



#### Finally confused







    
    try {
        conn.Open();
        //...
    } catch(Exception ex) {
    } finally {
        conn.Close();
    }





    
    Try
        conn.Open()
        '...
    Catch ex As Exception
    Finally
        conn.Close()
    End Try





I've run into this a few times now where there is an empty catch block followed by a finally block.  The catch is usually there because the author assumed that every try needed a catch.  This is not the case with finally.

Finally blocks are good.  Finally is your friend.  Need to make sure that the cursor is reset, even if there is an exception? _Use finally._  Anything in a finally will absolutely happen every time exception or not.

I try to use more try/finally blocks than try/catch blocks.

See also: the using keyword.



#### The End


So, that's what I got.  Any other exception anti-patterns out there?.

One other thing I should mention: most code should not be interested in exceptions.  If there is an exception it's rare that you can or should do anything at the low level code that generated it.  

Far better to use a global exception handler that will log the exception and give the user a message that won't scare them away.  These global handlers are easy to setup for a windows forms and asp.net applications.

I was going to put up a bad example followed by the right way to do it, but I got lazy.  Plus that would make this post even longer than it already is.
