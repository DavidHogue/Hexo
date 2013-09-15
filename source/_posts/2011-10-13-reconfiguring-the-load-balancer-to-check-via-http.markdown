---
author: David Hogue
comments: true
date: 2011-10-13 22:48:00+00:00
layout: post
slug: reconfiguring-the-load-balancer-to-check-via-http
title: Reconfiguring the load balancer to check via HTTP
wordpress_id: 91
categories:
- Software Development
tags:
- load balancing
- servers
---

So this comes from a work experience. For a project, I was looking into reconfiguring the load balancer we were using...

We're using [loadbalancer.org](http://loadbalancer.org/). Which uses [Linux-HA](http://www.linux-ha.org/wiki/Main_Page) which uses [ldirectord](http://linux.die.net/man/8/ldirectord) to monitor servers.

There are a few options for how it tests to see if a server is down. We had been using connect. What that does is it just opens a TCP connection on port 80. If it opens successfully, it assumes the server is alive. The problem with that was that the app pool was stopped, but other app pools were still running so IIS was still accepting TCP connections. 

What I want to do is change it to negotiate. What negotiate does is it sends an HTTP request and expects to get specific content back.

I tried negotiate last week on QA servers, and it immediately marked every server as unavailable. Not a good sign. What I finally realized is that it's sending the HTTP request to the server's primary IP and not the load balanced IP. As soon as I made the IIS web accept connections on that IP, it worked as advertised.

I've setup the web on our QA servers to accept connections on port 3333 with a specific host header. That way the load balancer can check if the app pool is running and the file can be stored in our project, but it's unlikely someone will accidentally browse to it. (I'm thinking about reversing this decision for production honestly.)

[![](https://davidhogue.com/wp-uploads/2011/10/Load-balancer-settings.png)](https://davidhogue.com/wp-uploads/2011/10/Load-balancer-settings.png)

After I made the changes to QA, I tried stopping app pools and causing crashes by changing the version of asp.net used. I never got any errors in my browser and the server was marked as non-nactive.

[![](https://davidhogue.com/wp-uploads/2011/10/Load-balancer-status.png)](https://davidhogue.com/wp-uploads/2011/10/Load-balancer-status.png)

This could use a little more testing, but I think it's a good solution.
