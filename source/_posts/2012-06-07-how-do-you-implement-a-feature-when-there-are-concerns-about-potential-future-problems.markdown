---
author: David Hogue
comments: true
date: 2012-06-07 22:31:47+00:00
layout: post
slug: how-do-you-implement-a-feature-when-there-are-concerns-about-potential-future-problems
title: How do you implement a feature when there are concerns about potential future
  problems?
wordpress_id: 941
categories:
- Software Development
---

Lets say you're tasked with writing some code to meet some requirements. Now either because of your past experience in the area, or because the requirements outline potential difficulties, you have some concerns. You might know that adding the feature has the potential to slow things down and you're already sensitive to this because users have complained in the past about things taking too long.

The way I see it, there are two schools of thought for how to handle this. The first option is to write simple, clean code while keeping the landmines in mind. Then testing to see how it goes. The second option is to bulk up the code making it more complex and possibly more resistant to the perceived problems. 

I've tried for a while now to make my code simple and understandable. I feel that's the best way to make sure it works as intended and is easy to modify by me or anyone else down the road. I've noticed lately that when I go for the simpler implementation of a feature, I get asked a lot questions.




### Implementation one: Minimal, with tests



I much prefer the route with the minimalistic clean code. Then through testing and profiling tools I can pinpoint exactly where problems are, if there are any. If there aren't, I saved myself some time. If there are bottlenecks or the code isn't flexible enough, I can build on top of the clean code.

I know the simple implementation works because I spent time testing it and I find it makes a pretty good guide for a more complex implementation. I can see where some people might say that I took more time than necessary by writing it twice. In my experience it feels like it's just as fast if not faster to write it once and rewrite it.





### Implementation two: Robust, but complex



This route would require more design and code up front. The idea being that it would be able to handle the potential problems better.

There's several things I don't like about this approach. First of all you're spending a lot of time and energy focusing on things like threading and caching when that could be better spent looking at the problem the code is trying to solve. Secondly, often times these concerns turn out to be non-issues, but the code now has all this complexity that's going to make future changes more error prone.



### Implementation three: something else?



Is there another approach I'm overlooking? I feel like the correct route is obvious, but I regularly questions or confusion. I'm not on the same page with everyone. Maybe I just need to spend more time discussing options and less time in Visual Studio.

So which seems like the safest bet to you? How do you handle a situation such as this?
