---
author: David Hogue
comments: false
date: 2006-04-29 03:48:13+00:00
layout: post
slug: woot-quickbooks-is-a-royal-pain
title: Woot! / QuickBooks Is a Royal Pain
wordpress_id: 348
categories:
- Software Development
tags:
- old-blog
---

So, I'm trying to write some code that will talk to QuickBooks.  All I want to do for the moment is enter some test data in the weekly time sheets area.  There's an SDK, many code samples, and loads of documentation.  It shouldn't be that hard right?  Ha!

To start with I don't really like QuickBooks.  It's slow, it's ugly, and the non standard widgets barely work.  And I've tried, unsuccessfully, to work with the SDK before.  So I knew this wasn't going to be that simple.  I already knew that QuickBooks actually had to be running and there was some security stuff.

Anyway here's my code that will simply open the file and enter some time:

    
    [Test]
    public void TestEnterTime()
    {
    	RequestProcessor2 rp = new RequestProcessor2();
    	rp.OpenConnection2("", "IDN CustomerAdd C# sample", QBXMLRPConnectionType.localQBD);
    	string ticket = rp.BeginSession("C:\Documents and Settings\david\Desktop\Widgets Inc.QBW", QBFileMode.qbFileOpenDoNotCare);
    	string response = rp.ProcessRequest(ticket, "< ?xml version="1.0"?>" +	// the < ?xml line is required!
    		"" +
    		"<qbxml>" +
    		" <qbxmlmsgsrq onerror="stopOnError">" +
    		"  <timetrackingaddrq requestid="1">" +
    		"   <timetrackingadd>" +
    		"    <txndate>2006-04-28</txndate>" + // CCCC-MM-DD, 0 padded
    		"    <entityref><fullname>David Hogue</fullname></entityref>" +
    		"    <customerref><fullname>test2</fullname></customerref>" +
    		"    <itemserviceref><fullname>test</fullname></itemserviceref>" +
    		"    <duration>PT0H30M</duration>" +
    		"   </timetrackingadd>" +
    		"  </timetrackingaddrq>" +
    		" </qbxmlmsgsrq>" +
    		"</qbxml>");
    	rp.CloseConnection();
    	Assert.IsFalse(response.Contains("error"), response);
    }



Even though there is tons of documentation, it isn't clear what syntax the api wants.  There is a validator, but I had many times where my code validated correctly and QB didn't like it.  (It gave me a useless "error parsing xml" message).  Finally I figured out that the < ?xml version="1.0"?> line is required.

Once I added the top line it gave me some more errors.  Errors such as the record must be locked before it can be edited (translation: close the time entry window), a customer must be specified to enter billable time, etc.

Their COM based API is also very odd.  It has a hundred or so enumerations, a couple hundred interfaces, and two or three public classes.  Everything is created with factory methods.  You can't set any properties equal to a value, there's always a SetValue method that takes a string.  Not very .netified.

I don't think many people are really using the SDK.  I only found a few hits on google for common errors and peices of the xml like TimeTrackingAddRq.  I predict that I'll be in the top few results by next week.
