---
author: David Hogue
comments: false
date: 2006-08-29 05:29:53+00:00
layout: post
slug: why-im-not-a-fan-of-utility-classes
title: Why I'm Not a Fan of "Utility" Classes
wordpress_id: 152
categories:
- Software Development
tags:
- old-blog
---

All the time I run across classes with names like UserUtility, PartUtility, SectionUtility.  Every one of them is filled with barely related, mostly static, methods for doing all kinds of stuff with and to a thier related objects (User object, Part object, or Section object)





![diagram of a utility class](http://vorpal.cc/blog/wp-content/uploads/2006/08/badutility.png)

![diagram of a class with logic](http://vorpal.cc/blog/wp-content/uploads/2006/08/goodutility.png)





They start out innocent enough.  Often it starts as a collection of database methods like SaveUser(user), GetUser(id), or sometimes SaveUser(id, name, role, password, etc, etc, etc).  This is all fine and good.Except the versions that take only primitives can grow out of control, I've seen one that required 39 parameters with overloads that had 34, 32, and 22 parameters

Then they grow.  Let's say a programmer has a bit of code encrypt a user's password.  They see UserUtility and immediately think "I should add a EncryptPassword function to UserUtility!"  Eventually any logic that remotely relates to a User ends up in the UserUtility and the User class is just a dumb data bag.[Data bag](http://www.testdriven.com/modules/newbb/viewtopic.php?topic_id=3741&forum=6#forumpost21026): class that contains only fields and getters/setters, but no logic.  This is the only reference I could find, if you have a better link let me know.  I'd much prefer the encryption was done in the User class.  Or, maybe even in a Password class.

I think a big cause of this is the name.  A UserUtility could be just about anything.  If the class were called UserMapper or UserDatabase developers would be less likely to put non-database code in there.  Instead they might create a new class, or use the existing User class.

Another thing: in most utility classes I run across everything is static (Shared in vb).  This means I can't override methods, I can't substitute a different utility if I want to, say, save and load to a Firebird database instead of MS-SQL.  And since they are all static the entire codebase ends up very procedural and not very object oriented.

Anyway, I feel like I'm ranting; so I'll stop here for tonight.  I just view most utility classes as an [anti-pattern](http://en.wikipedia.org/wiki/Anti-pattern) and it bugs me when I see them.


