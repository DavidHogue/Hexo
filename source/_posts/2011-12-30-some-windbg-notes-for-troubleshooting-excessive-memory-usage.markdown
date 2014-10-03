---
author: David Hogue
comments: true
date: 2011-12-30 17:45:43+00:00
layout: post
slug: some-windbg-notes-for-troubleshooting-excessive-memory-usage
title: Some WinDbg notes for troubleshooting excessive memory usage
wordpress_id: 806
categories:
- Software Development
tags:
- debugging
- memory
- servers
- windbg
---

![GCRoot](https://davidhogue.com/wp-uploads/2011/12/WinDbg-gcroot.png)

A little while ago I ran into some problems with the w3wp process gobbling up tons of memory. It ate up so much memory that after running for a few hours with high traffic, it would automatically get restarted by IIS.

WinDbg isn't the friendliest looking program, but if you know a few commands you can get quite a ways with it.

In my case the memory was used up by how we were pushing NHibernate to do some non-standard things. These same steps could be used to troubleshoot most generic memory usage problems.




### Here's the steps I followed to get through this:



![Performance Monitor](https://davidhogue.com/wp-uploads/2011/12/WinDbg-PerfMon.png)




  
  1. I have a memory dump I made with [Process Explorer](http://technet.microsoft.com/en-us/sysinternals/bb896653) on the server when it had been running for 3 hours and was about to be recycled.
  
  2. The Gen2 heap size was what was growing up to 1.4GB. The other heaps stayed about the same size for the life of the app. Which apparently is common when there is a memory leak. I was able to tell this with performance counters and then confirm it with windbg.
  
  3. The type taking up the most memory is strings, after that various types of arrays. Which also seems normal, even if there wasn't a leak.
  
  4. From a random sampling of strings, most look like SQL fragments, but some are HTML content. Makes sense, most of the strings in this particular app are going to be HTML or SQL.
  
  5. WinDbg did take a very long time to do some operations on the 3GB memory dump. Using an SSD helped, but I still had to be patient for some operations
  
  6. Finally it started looking like the NHibernate query cache was holding on to a bunch of data. There's a similar issue that was discovered [here](http://markmail.org/message/a3zftctucv65n27s#query:+page:1+mid:a3zftctucv65n27s+state:results).
  
  7. The data is rooted in a static property so it will never be garbage collected. Our code was written this way since the documentation said to only create each session factory once and store it.
  
  8. One NHibernate SessionFactory on its own isn¿t too bad, it only took up 34MB. Where it gets problematic is when we have a bunch of those in memory.
  
  9. <strike>In the near term, I think this can be fixed by using some [WeakReferences](http://msdn.microsoft.com/en-us/library/system.weakreference.aspx).</strike> Longer term I'd like to use only one or two SessionFactories.
  
  10. I found out that a [MemoryCache](http://msdn.microsoft.com/en-us/library/system.runtime.caching.memorycache.aspx) would be better than WeakReferences.
      
  * WeakReferences go away as soon as the garbage collector runs if nobody is using them, the cached items go away when memory is tight.
    
  * Even longer term, I'd like to get down to just a few or even one session factory. I think reading up on sharding might be the next step here.

    
  






### Links:






  
  * [SOS.dll (SOS Debugging Extension)](http://msdn.microsoft.com/en-us/library/bb190764.aspx)

  
  * [Bugslayer: SOS: It's Not Just an ABBA Song Anymore](http://msdn.microsoft.com/en-us/magazine/cc164138.aspx)

  
  * [WinDbg / SOS Cheat Sheet](http://geekswithblogs.net/.netonmymind/archive/2006/03/14/72262.aspx)

  
  * [Where's your leak at? [Using WinDbg, SOS, and GCRoot to diagnose a .NET memory leak]](http://blogs.msdn.com/b/delay/archive/2009/03/11/where-s-your-leak-at-using-windbg-sos-and-gcroot-to-diagnose-a-net-memory-leak.aspx)

  
  * [New commands in SOS for .NET 4.0 Part 1](http://blogs.msdn.com/b/tess/archive/2010/03/01/new-commands-in-sos-for-net-4-0-part-1.aspx)

  
  * [New Silverlight SOS.DLL Commands: !HeapStat and !GCWhere](http://blogs.microsoft.co.il/blogs/sasha/archive/2008/08/27/new-silverlight-sos-dll-commands-heapstat-and-gcwhere.aspx)








![DumpHeap -stat](https://davidhogue.com/wp-uploads/2011/12/WinDbg-DumpHeap-stat.png)

![DumpHeap -type System.String](https://davidhogue.com/wp-uploads/2011/12/WinDbg-DumpHeap-strings.png)







### Useful WinDbg & SoS commands:







  
  * `.loadby sos clr` -- loads SoS into windbg.
    
      
  * `.load C:\SomePath\sos.dll` -- can be used to load another version of sos.dll that was downloaded from the server.

  
  * `.prefer_dml 1` -- makes addresses in the output clickable to get more details.

  
  * `CTRL+Break` -- stops the currently running command.

  
  * `!Help` -- lists all SoS commands.

  
  * `!HeapStat` -- lists some stats on where memory is used.

  
  * `!EEHeap -gc` -- lists start and end addresses for each heap.

  
  * `!DumpHeap -stat [Begin] [End]` -- Gives stats on what types are using up memory. Begin and End come from !EEHeap -gc, I wanted only Gen2.

  
  * `!DumpHeap -Type <Type> [Begin] [End]` -- Lists all instances of a type, like System.String, between Begin and End.

  
  * `!DumpObj <Address>` -- Prints out details on an object.

  
  * `!GCWhere <Address>` -- Prints out what heap an object is in, it¿s address and size.

  
  * `!GCRoot -nostacks <Address>` -- Lists objects that have a reference to the object. The object at the root of the list is why the memory has not been garbage collected. This can take quite a while.

  
  * `!ObjSize [Address]` -- Lists the size of the object by adding up the size of all references. Can take a while if it needs to loop through a lot.






### Details:



Here's the output of !GCRoot 00000001805a8640 on a single string that contains a fragment of SQL. I also added some information on the total size while I was poking around.

```
DOMAIN(00000000001B4550):HANDLE(Pinned):73015e8:Root:  000000028010c068(System.Object[])->
  00000001c0180668(System.Collections.Generic.Dictionary`2[[System.Guid, mscorlib],[NHibernate.ISessionFactory, NHibernate]])-> (1272.6 MB!)
  000000020c29f578(System.Collections.Generic.Dictionary`2+Entry[[System.Guid, mscorlib],[NHibernate.ISessionFactory, NHibernate]][])-> (1272.6 MB!)
  00000002402b6208(NHibernate.Impl.SessionFactoryImpl)-> (34.6 MB)
  00000002402b6628(NHibernate.Engine.Query.QueryPlanCache)->
  00000002402b79c0(NHibernate.Util.SoftLimitMRUCache)->
  00000002402b7a60(NHibernate.Util.LRUMap)->
  00000002402b7ac0(System.Collections.Hashtable)->
  00000002402b7b18(System.Collections.Hashtable+bucket[])->
  00000001c08cecc8(NHibernate.Util.SequencedHashMap+Entry)->
  00000001c08a6628(NHibernate.Engine.Query.HQLStringQueryPlan)->
  00000001c08c9cf8(System.Object[])->
  00000001c08c9c90(NHibernate.Hql.Ast.ANTLR.QueryTranslatorImpl)->
  00000001c08ccc48(NHibernate.Hql.Ast.ANTLR.Tree.QueryNode)->
  00000001c08caa48(NHibernate.Hql.Ast.ANTLR.Tree.FromClause)->
  00000001c08cac58(NHibernate.Util.NullableDictionary`2[[System.String, mscorlib],[NHibernate.Hql.Ast.ANTLR.Tree.FromElement, NHibernate]])->
  00000001c08cac80(System.Collections.Generic.Dictionary`2[[System.String, mscorlib],[NHibernate.Hql.Ast.ANTLR.Tree.FromElement, NHibernate]])->
  00000001c08cb748(System.Collections.Generic.Dictionary`2+Entry[[System.String, mscorlib],[NHibernate.Hql.Ast.ANTLR.Tree.FromElement, NHibernate]][])->
  00000001c08cb538(NHibernate.Hql.Ast.ANTLR.Tree.FromElement)->
  00000001c08cb650(NHibernate.Hql.Ast.ANTLR.Tree.FromElementType)->
  0000000180481ef0(NHibernate.Persister.Collection.BasicCollectionPersister)->
  00000001805a83f0(NHibernate.Loader.Collection.BasicCollectionLoader)-> (34.6 MB)
  00000001805a87a0(NHibernate.SqlCommand.SqlString)-> (616 Bytes)
  00000001805a8740(System.Object[])->
  00000001805a8640(System.String) (200 Bytes)
```



