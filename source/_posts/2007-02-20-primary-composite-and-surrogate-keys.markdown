---
author: David Hogue
comments: false
date: 2007-02-20 07:05:39+00:00
layout: post
slug: primary-composite-and-surrogate-keys
title: Primary, Composite, and Surrogate Keys
wordpress_id: 192
categories:
- Software Development
tags:
- old-blog
---

I have been catching up on my feed reader's backlog and I found some interesting posts on primary keys in sql that I thought I'd share:

[Meaningless Keys](http://jonathanlewis.wordpress.com/2006/12/29/meaningless-keys/)
[keys, more keys and nothing but keys...](http://dbasrus.blogspot.com/2007/01/keys-more-keys-and-nothing-but-keys.html)
[Primary Keyvil, Part I](http://blogs.ittoolbox.com/database/soup/archives/primary-keyvil-part-i-7327) (checkout parts 2 and 3 also)
[Composite keys are evil](http://codebetter.com/blogs/jeremy.miller/archive/2007/02/01/Composite-keys-are-evil.aspx)
[Surrogate Key != Primary Key](http://www.chrisholmesonline.com/2007/02/03/surrogate-key-primary-key/)

I don't have any real strong opinions on the subject, just some thoughts:

I do think composite keys are a pain in most situations.  And not because of any ORM tools as implied in some comments in the above links.  Most of the database code I write is still straight sql: sometimes stored procedures, sometimes parameterized queries.

In the databases I work on, nearly every table has an id field that is an auto-incrementing integer.  This works well I think.  It's consistent, which is always good.  Joins are easy.  The sql is easy (sometimes)

When designing a table I have a concept in my head of what makes a record unique.  I don't think of it as a "key" usually.  A key, at least the way most tools and books talk about it, is a single field; usually meaningless outside the database.  The tools never seem to push the term "surrogate key."  Just primary keys and foreign keys.

Any information that is determined to be unique to a record is enforced with a constraint, but it's not referred to as a primary key.  At least going by how I see the tools used.

Is it just a difference in terminology?  Or, is there more to it?  I don't think I'd do anything fundamentally differently if I thought in terms of primary-composite keys and surrogate keys.  It's something I'll have to keep in mind next time I'm creating a table.
