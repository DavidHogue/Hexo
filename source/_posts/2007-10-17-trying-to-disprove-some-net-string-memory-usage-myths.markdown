---
author: David Hogue
comments: false
date: 2007-10-17 19:39:35+00:00
layout: post
slug: trying-to-disprove-some-net-string-memory-usage-myths
title: Trying to disprove some .net string memory usage myths
wordpress_id: 235
categories:
- Software Development
tags:
- old-blog
---

I've run into a few string/constants myths repeatedly and I thought I'd try to disprove them.  Myth 1: constants use less memory.  Myth 2: inline strings are always bad.  Myth 3: String.Empty doesn't create an object while "" does.

I'm just running a bunch of different pieces of code and dumping memory statistics before and after to measure.  The trimmed output of sos's !dumpheap -stat command are included after each line.

Thanks to [Pale Musings](http://blog.palehorse.net/) for the [sos memory leaks article](http://blog.palehorse.net/2007/03/02/troubleshooting-memory-leaks-in-net/).



#### Contents







  * Steps to reproduce


  * Simple inline string


  * Enum to lower case string


  * Second enum to string


  * Constant defined in the same class


  * Using the same string repeatedly inline


  * Two different inline strings


  * Appending constants with +


  * Quote quote ("")


  * String.Empty


  * Conclusion





#### Steps to reproduce:






  1. Create console app.


  2. Go to project properties, enable unmanaged debugging.


  3. In main add (changing the first line each time)

`            string value = "span";
            Console.WriteLine(value);
            Console.ReadKey(true);`

  4. Put breakpoints on lines 1 and 2.


  5. Run app with debugger (F5).


  6. In the immediate window type `.load sos`


  7. In the immediate window type `!dumpheap -stat`


  8. Run to next breakpoint (F5).


  9. In the immediate window type `!dumpheap -stat`


  10. Compare output from dumpheap.


  11. Change line 1 and repeat.





#### Simple inline string



code: `string value = "span";`

before:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2038       129792 System.String
    Total 2085 objects
    



after: 

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2038       129792 System.String
    Total 2085 objects
    





#### Enum to lower case string



code: `string value = HtmlTextWriterTag.Span.ToString().ToLower();`

before:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     4825       264628 System.String
    Total 4875 objects
    



after:

    
    
     Count    TotalSize Class Name
    ...
    790f9244     4932       267760 System.String
    Total 5177 objects
    





#### Second enum to string


I thought the above might be unfair.  Maybe I was counting memory usage from loading the System.Web assembly or the HtmlTextWriterTag for the first time.

code: `span.ToString().ToLower();`

before:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     4825       264628 System.String
    Total 4875 objects
    



after:

    
    
          MT    Count    TotalSize Class Name
    790f9244     4932       267760 System.String
    Total 5177 objects
    





#### Constant defined in the same class



code: `string value = span;` (span is a constant of the class)

before:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2038       129792 System.String
    Total 2085 objects
    



after:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2038       129792 System.String
    Total 2085 objects
    





#### Using the same string repeatedly inline



code: `string value = "span"; 
string value2 = "span"; 
string value3 = "span"; 
string value4 = "span"; 
string value5 = "span";`
before:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2038       129792 System.String
    Total 2085 objects
    



after:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2038       129792 System.String
    Total 2085 objects
    





#### Two different inline strings



code: `string value = "span a"; 
string value2 = "span b";`

before:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2039       129828 System.String
    Total 2086 objects
    



after:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2039       129828 System.String
    Total 2086 objects
    





#### Appending constants with +



code: `string value = span + a; 
string value2 = span + b;` (span, a, b are constants)

before:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2039       129828 System.String
    Total 2086 objects
    



after:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2039       129828 System.String
    Total 2086 objects
    





#### Quote quote ("")



code: `string value = "";`

before:

    
    
          MT    Count    TotalSize Class Name
    
    790f9244     2038       129784 System.String
    Total 2085 objects
    



after:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2038       129784 System.String
    Total 2085 objects
    





#### String.Empty



code: `string value = String.Empty`

before:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2037       129764 System.String
    Total 2082 objects
    



after:

    
    
          MT    Count    TotalSize Class Name
    ...
    790f9244     2037       129764 System.String
    Total 2082 objects
    






#### Conclusion



So: using inline strings is no better than constants as far as memory or performance are concerned.  Enums are worse than constants or inline.  String.Empty did save me one object instance and a whole 20 bytes.

For readability and maintainability, constants can help.  Personally I find code where _everything_ is a constant even if it is only used once annoying, but that's just me :)

There's probably other pages on the net that go into exactly why this all is.  At the moment I'm too lazy to go searching for them.  Go ahead and open the code in reflector to see what it's getting compiled to if you want.

The actual difference in any of these is probably so small you'll never notice it, so go with whatever is easiest and most readable for you.
