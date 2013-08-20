---
author: David Hogue
comments: false
date: 2006-09-30 01:46:49+00:00
layout: post
slug: write-nunit-tests-for-your-bugs
title: Write NUnit Tests for Your Bugs
wordpress_id: 164
categories:
- Software Development
tags:
- old-blog
---

Today I ran into a method that would crash under certain conditions, but all tests passed.  The bug was very simple and I could have fixed it in under a minuteThis was re-written from memory and modified because I didn't want to post code that could get me in trouble:


    
    public void SaveUser(User u)
    {
        // ...
    
        if (u.Cards.Count >= 2)
        {
            AddParameter("USER_CARD2NAME", u.Cards[2]);
            // ...
        }
    
        // ...
    
        cmd.ExecuteNonQuery();
    
    }



And while in theory if we were using TDD perfectly this bug wouldn't have snuck inNote that TDD does not claim to prevent all bugs.  There are cases where you can't test every possible combination of inputs.  In this case however a user could have 0, 1, or 2 cards..  It did however sneak in and that told me that there wasn't a test for if a user had two cards.

So I wrote this test:


    
    [Test]
    SaveWith2Cards()
    {
        // arrange
        User user = new User();
        user.Cards.Add(new Card());
        user.Cards.Add(new Card());
        UserUtility util = new UserUtility();
        string sql;
    
        // act
        util.CreateSaveUserSql(user, sql, null);
    
        // assert
        Assert.IsTrue(sql.Contains("USER_CARD2NAME"), "sql should contain the USER_CARD2NAME field");
    }



And extracted a CreateSaveUserSql method from the SaveUser method:


    
    public void CreateSaveUserSql(User user, out string sql, out IDbDataParameter[] parameters)
    {
        // ...
    
        if (u.Cards.Count >= 2)
        {
            AddParameter("USER_CARD2NAME", u.Cards[1]);
            // ...
        }
    }
    
    public void SaveUser(User user)
    {
        // ...
    
        CreateSaveUserSql(user, sql, parameters);
    
        // ...
    
        cmd.ExecuteNonQuery();
    
    }



The advantage of this is that I now have a test for the bug and it the code won't break this way in the future.  It really didn't take me much longer than just changing it on the spot.

I also took the opportunity to do a little refactoring: [extract method](http://www.refactoring.com/catalog/extractMethod.html) and rename parameter.

The create CreateSaveUserSql method does pollute the public interface of the class a little.  I'm also not a big fan of the output parameters.

There's still improvements to be made:  I could move the method to a separate class, create a parameter object for it to return, etc.  But I'm taking it one step at a time.  This works for now, so I'll move on.
