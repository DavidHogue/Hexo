---
author: David Hogue
comments: true
date: 2011-10-21 16:31:33+00:00
layout: post
slug: stupid-router-tricks-or-how-to-use-dd-wrt-to-extend-the-range-of-a-network
title: Stupid Router Tricks (or how to use DD-WRT to extend the range of a network)
wordpress_id: 97
categories:
- Technology
tags:
- networking
- routers
---

I recently found myself in a situation where I had no direct internet connection where I was staying. I did find a public wifi signal, but it was very weak.

At first I tried sitting over on the side of the room near the window and raising my laptop up higher to get a better signal. Even with that, the signal was still barely usable. It might have worked for sending an email or loading a single web page, but I needed to get some real work done.

After fighting with it for a while, it occurred to me that I had an old wifi router with me. A good old Linksys WRT54-GL.

Originally I had Tomato on it, so I connected it to my laptop with an ethernet cable and got to work. I was able to get it to find the network and connect. Now I could put the router in the top corner of the window where the signal was best and run a wire over to my laptop.

Being hardwired worked, but it still wasn't ideal. So I got to wondering if I could simply extend the range of the network. To make a long story short, I couldn't figure out how to do it with Tomato. There is a way, but you need to setup both routers to get it to work.

So I installed DD-WRT. It has a feature I've never seen on any other router: it supports virtual wireless interfaces. This meant I could have it connect to the public wifi while at the same time being another access point.

So I set it up to repeater mode, gave it everything it needed to connect to the wifi signal, and added a virtual interface:

[![](https://davidhogue.com/wp-uploads/2011/10/Wifi-Repeater.png)](https://davidhogue.com/wp-uploads/2011/10/Wifi-Repeater.png)

Before I was done, I wanted to go and setup some security. It was nice I could do this separately for each interface:

[![](https://davidhogue.com/wp-uploads/2011/10/Wifi-Repeater-Security.png)](https://davidhogue.com/wp-uploads/2011/10/Wifi-Repeater-Security.png)

After doing all this and rebooting a few times, it worked! I had a router that would essentially use a hotspot as a wan port. It was a little finicky at first, but once it started working it was rock solid.

I was still able to setup my own network, run a DHCP server, and do everything else like normal. The router would NAT everything to the hotspot as if it were my ISP. I'm assuming that the hotspot was also running it's own NAT as well, but that didn't matter to me.

After I got all that to work, I setup a VPN and tunneled all my traffic through it. Just in case someone malicious was also using the hotspot. It also opened up a lot of possibilities for me like forwarding a port on a public IP back to me or someday running IPv6.


