---
author: David Hogue
comments: true
date: 2011-08-08 15:24:26+00:00
layout: post
slug: changing-which-conversation-an-email-is-grouped-in-with-outlook-2010
title: Changing which conversation an email is grouped in with Outlook 2010
wordpress_id: 65
categories:
- Technology
tags:
- email
- outlook
---

Outlook 2010 has a conversation grouping feature that can be pretty handy when you have a lot of different conversations headed to your inbox.  However sometimes it gets confused.

Unfortunately it's pretty poor at handling a few situations: when several different threads have the same subject and when the subject line is changed.  In theory, there should be a way for Outlook to work around those limitations using standard emails headers, but it doesn't.  Maybe in 2012...

Recently I had several different email threads going at once with tens of emails a day for the same project.  Unfortunately one of the participants had a spam filter that would append [!!SPAM] to nearly every subject line.  If I didn't correct the subject, we'd eventually get a subject like RE: [!!SPAM] Re: [!!SPAM] RE: You get the idea.

While you _can_ change the subject of an email in your inbox, it's still grouped into a separate conversation.

So I went looking and eventually found a tool called [MFCMAPI](http://mfcmapi.codeplex.com/) that will let you poke into all kinds of hidden fields in Outlook.  Make sure you get the 64bit version if you're using the 64bit Outlook.

After starting a session and connecting, it gave me a list of mailboxes:
[![](http://davidhogue.com/wp-uploads/2011/08/MFCMAPI-x64-Build-Mailbox-David-Hogue.png)](http://davidhogue.com/wp-uploads/2011/08/MFCMAPI-x64-Build-Mailbox-David-Hogue.png)

Double clicking my mailbox brought up this:
[![](http://davidhogue.com/wp-uploads/2011/08/Mailbox-David-Hogue-Inbox.png)](http://davidhogue.com/wp-uploads/2011/08/Mailbox-David-Hogue-Inbox.png)

And double clicking on my inbox brought up a list of emails.  If I double clicked on an email, it would open up in Outlook.  However, just selecting the email would show a list of properties below:
[![](http://davidhogue.com/wp-uploads/2011/08/Inbox-Display-Name-Not-Found.png)](http://davidhogue.com/wp-uploads/2011/08/Inbox-Display-Name-Not-Found.png)

I ended up editing PR_CONVERSATION_TOPIC and PR_SUBJECT:
[![](http://davidhogue.com/wp-uploads/2011/08/Property-Editor.png)](http://davidhogue.com/wp-uploads/2011/08/Property-Editor.png)

The PR_CONVERSATION_TOPIC field is used by Outlook to group emails into the same conversation.  As far as I can tell it can be nearly any unique string.  I just changed it to remove the [!!SPAM] and the RE: since that's what other messages already in the conversation used.

This has helped me quite a bit to get organized when I was being overwhelmed with emails.  It's probably not foolproof, so be careful what you change.  I only changed the two fields and I'm not even sure what half the other ones are.

Now that I know which fields to change I was hoping to find or make a plugin that would do this from within Outlook automatically.
