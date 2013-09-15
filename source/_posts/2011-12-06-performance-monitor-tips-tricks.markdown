---
author: David Hogue
comments: true
date: 2011-12-06 23:46:58+00:00
layout: post
slug: performance-monitor-tips-tricks
title: Performance Monitor Tips & Tricks
wordpress_id: 758
categories:
- Software Development
tags:
- perfmon
- performance
- servers
- stats
---

I’ve been doing a lot of digging into performance monitor this last week or so and learned some new tricks. I thought I'd write this up and share what I found in case it's useful in the future:




	
  * Command line tools: logman.exe, relog.exe and typeperf.exe.

	
			
    * **Logman** can be used to create new logs. It has one option that the GUI doesn't have, and that is to run the same scheduled log each day.

			
    * **Relog** can be used to convert log files from the binary .blg into .csv or SQL. It can also let you pull only specific counters or time spans out of a .blg. Another use is combining counter logs from multiple files.

			
    * **Typeperf** can be used to get raw counter data from the command line.


			
    * There are some commands in PowerShell too, but for adding counters logman seems much less verbose.

	

	  


	
  * I have some productions servers logging from early morning until night and the files are only around 15MB or so.

		
		
    * They’re only logging selected counters and only logging data once a minute.

		
    * Some counter logs can get large very quickly because they grab a lot of data every few seconds, but the file size seems to be capped around 3GB.

		
    * Here is the list of counters I’m currently capturing. I’d love to hear any suggestions if there are useful ones I missed.`
\.NET CLR Exceptions(_Global_)\# of Exceps Thrown / sec
\.NET CLR Interop(_Global_)\# of Stubs
\.NET CLR Loading(_Global_)\Bytes in Loader Heap
\.NET CLR Loading(_Global_)\Current Assemblies
\.NET CLR Loading(_Global_)\Rate of Assemblies
\.NET CLR Memory(_Global_)\# Bytes in all Heaps
\.NET CLR Memory(_Global_)\# Induced GC
\.NET CLR Memory(_Global_)\% Time in GC
\.NET CLR Memory(_Global_)\Gen 0 heap size
\.NET CLR Memory(_Global_)\Gen 1 heap size
\.NET CLR Memory(_Global_)\Gen 2 heap size
\.NET CLR Memory(_Global_)\Large Object Heap size
\ASP.NET\Application Restarts
\ASP.NET\Request Execution Time
\ASP.NET\Request Wait Time
\ASP.NET\Requests Current
\ASP.NET\Worker Process Restarts
\ASP.NET Applications(__Total__)\Compilations Total
\ASP.NET Applications(__Total__)\Errors During Execution
\ASP.NET Applications(__Total__)\Request Execution Time
\ASP.NET Applications(__Total__)\Request Wait Time
\Memory\% Committed Bytes In Use
\Memory\Available MBytes
\Memory\Pages/sec
\PhysicalDisk(_Total)\Avg. Disk sec/Read
\PhysicalDisk(_Total)\Avg. Disk sec/Write
\Process(_Total)\Handle Count
\Process(_Total)\Virtual Bytes
\Processor(_Total)\% Processor Time
\Web Service(_Total)\Bytes Received/sec
\Web Service(_Total)\Bytes Sent/sec
\Web Service(_Total)\Get Requests/sec
\Web Service(_Total)\Post Requests/sec
`


	

	  


	
  * [![](https://davidhogue.com/wp-uploads/2011/12/PerfmonSettings-e1323212921916-150x51.png)](https://davidhogue.com/wp-uploads/2011/12/PerfmonSettings.png)There are a couple buttons in the toolbars for copying and pasting settings.

	
		
    * These can be used to paste the settings into notepad and edit it as XML.

		
    * It was useful for using the same settings on multiple servers as well as getting the names of counters for the command line.

		
    * The Windows 7 Performance Monitor has a Scale Selected Counter option in the right click menu that will automatically change the scale setting so that the graph fits in the window.

	




## Examples



As an example, here’s a couple graphs of a server I was testing a while ago. First, traffic to the server. It doesn’t look like it was all that busy, almost 5 requests a second on average:
![](https://davidhogue.com/wp-uploads/2011/12/PerfmonGraph1.png)

And here’s memory usage, you can see how the Gen 2 heap size grows and grows up to around 1.5GB when the app pool recycles:
![](https://davidhogue.com/wp-uploads/2011/12/PerfmonGraph2.png)
