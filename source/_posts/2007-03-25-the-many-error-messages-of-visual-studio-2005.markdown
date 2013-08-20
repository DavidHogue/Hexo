---
author: David Hogue
comments: false
date: 2007-03-25 00:51:33+00:00
layout: post
slug: the-many-error-messages-of-visual-studio-2005
title: The Many Error Messages of Visual Studio 2005
wordpress_id: 209
categories:
- Software Development
tags:
- old-blog
---

I've been using Visual Studio 2005 for over a year now, and in that time I've seen quite a few odd error messages come out of it.  After a while I started collecting screenshots.  So, that's about all this post is going to be: a collection of random errors from I've seen while using VS2k5.

<!-- more -->



* * *



![The build must be stopped before the solution can be closed.](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-buildmustbestopped.png)

I get this when I try to close and the solution is still compiling.  No problem, you'd think.  Just cancel the build right?  Nope, I get this if I build, cancel, then try to build again.  Nothing appears to happen building the second time.  I figure something is screwed up and try to restart, but I can't.  Every time I get this I had to kill Visual Studio with Task Manager.   These days I just don't use cancel.



* * *



![Output file objDebug***.Resources.resources is possibly corrupt](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-corruptresource.png)

Ah, corrupt resource files.  The solution to this has been: 1) open resource file 2) delete stuff!  One cause of this may be the vs designer serializing my classes into the resource file, but I think there is some other cause too.  ([here's how to keep the designer from serializing your classes](https://vorpal.cc/blog/category/development/vbnet/how-to-keep-the-visual-studio-designer-out-of-your-controls-properties.html))



* * *



![One or more errors encountered while loading the designer...](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-designerwackiness.png)

Random designer crash. The solution to this one is to close the document and reopen it.  Sometimes it works, sometimes not.



* * *



![Entering break mode failed for the following reason: Source file ... does not belong to the project being debugged.](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-failedtoenterbreakmode.png)

I don't have a clue what the cause of this was.  The source file did indeed belong to the project, and I did a clean and rebuild just before getting this.



* * *



![Cannot write to the output file objdebug*** The process cannot access the file *** because it is being used by another process](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-fileinusebyanotherprocess.png)

Here's a favorite.  Cannot write to the file.  Fine, I'll find what's using it and kill it.  According to [Process Explorer](http://www.microsoft.com/technet/sysinternals/utilities/ProcessExplorer.mspx), nothing but Visual Studio has the file open.  I have to restart Visual Studio every time I get this one.



* * *



![Class aaa must implement bbb.  bbb cannot implement bbb because there is no matching event on interface xxx](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-mustimplementcannotimplement.png)

This just confuses me: a class cannot implement an interface method because it doesn't exist, but it must implement the method.  I've gotten this several times and each time went and checked that the return and parameter types are correct, everything is spelled correctly, etc.  The fix: clean and rebuild.



* * *



![%2](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-oddfile.png)

No idea what happened here.  Opened a file and the tab shows %2!



* * *



![Pass exception on to program being debugged?](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-passexception.png)

Not sure what it's asking me.  The debugger had already stopped on the line in the program where the exception was thrown.  My answer didn't seem to make any difference.  With either yes or no, the exception continued.



* * *



![Microsoft (R) Visual Basic Compiler has encountered a problem and needs to close.  We are sorry for the inconvenience.](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-repeatedcompilercrashes.png)

Yay! the compiler crashed.  If this happened once in a while it would be fine.  However, this particular window comes up about 40 times in a row.  Click Don't Send or X and another shows up.  The compiler is screwed until Visual Studio is restarted.  This seems to have been fixed with the service pack.



* * *



![Error connecting to undo manager of source file ***](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-undomanager.png)

I didn't even know there was an undo manager...



* * *



![Visual Studio has encountered an unexpected error.](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-unexpectederror.png)

Oh, an unexpected error.  What, no more information?  This didn't seem to cause any problems.  I clicked ok and kept working.



* * *



![An error was encountered while opening associated documents the last time this solution was loaded.  Document load is being skipped during this solution load in order to avoid that error.](http://vorpal.cc/blog/wp-content/uploads/2007/03/vs-whoknows.png)

ok...



* * *



Anyway, just thought I'd share the random errors I see all the time.  I was kind of wondering if anyone else out there gets nearly as many errors as I do.  Many of these errors have occurred with vb.net.  C# seems a bit more stable.  The service pack seems to have helped a bit too.
