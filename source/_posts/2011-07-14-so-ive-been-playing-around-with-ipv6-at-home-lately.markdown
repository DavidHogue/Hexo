---
author: David Hogue
comments: true
date: 2011-07-14 16:44:22+00:00
layout: post
slug: so-ive-been-playing-around-with-ipv6-at-home-lately
title: So I've been playing around with IPv6 at home lately
wordpress_id: 35
categories:
- Technology
tags:
- ipv6
- networking
---

IPv6, if you haven't heard, is supposed to be the future protocol of the internet.  Currently we're all using IPv4 to talk to servers and such online.  IPv4 has a limited number of addresses and there's enough computers online these days that we're running out.  IPv4 has the familiar address format like 192.168.1.1, where IPv6 supports many more addresses and has a format like fe80::202:b3ff:fe1e:8329.  The [Wikipedia article](http://en.wikipedia.org/wiki/IPv6) might be a good place to start if you'd like to know more.

Thanks to [Linode](http://blog.linode.com/2011/05/03/linode-launches-native-ipv6-support/), I now have a native IPv6 address on my server.  (You should be able to load this site over IPv6 if have it or you could use a [proxy](https://davidhogue.com.ipv4.sixxs.org/blog/2011/07/so-ive-been-playing-around-with-ipv6-at-home-lately/).)

I checked with my ISP to see if they had any kind of IPv6 trial going on, but no luck there.  Not too surprising really.

So I decided to see if my new [ASUS RT-N16](http://www.asus.com/Networks/WiFi_Networking/RTN16/) could do IPv6 through a tunnel.  I'd installed the [TomatoUSB](http://tomatousb.org/) firmware on it and heard some talk about IPv6 with it, but found no settings for it.  I finally downloaded a pre-release build of the firmware and that had settings.

[![](https://davidhogue.com/wp-uploads/2011/07/Tomato_IPv6-300x229.png)](https://davidhogue.com/wp-uploads/2011/07/Tomato_IPv6.png)

The image I used specifically was tomato-K26USB-NVRAM60K-1.28.9055MIPSR2-git-13042011-Ext.trx from [http://manveru.pl/tomato/index.html](http://manveru.pl/tomato/index.html)

**6to4**

I found an IPv6 tab under the Basic category and decided to try 6to4 Anycast Relay and checked Enable Router Advertisements.  I went to [ipv6.google.com](http://ipv6.google.com/) and it worked!  I was surprised it was that easy.

Then I learned how 6to4 works.  It sets up a tunnel to the hardcoded address 192.88.99.1.  Apparently there are a handful of providers out there operating at this address and my traffic got routed to the nearest one.

Now 6to4 did have a few problems.  1) I could not ping back to my router's address or any internal address from the public internet. And 2) modern operating systems try to avoid 6to4 if they can.  By that I mean that if a website has both an IPv4 and an IPv6 address, it'll use the IPv4 address every time.  Apparently this is because the tunnel is not entirely reliable (and will likely be slower.)  This makes sense and it's designed to not annoy end users.

**6in4**

So after that I decided to see if I could do any better.  Another option TomatoUSB had was 6in4 Static Tunnel.  For this to work I had to setup a tunnel with a company and enter in a bunch of numbers.  I used [tunnelbroker.net](http://tunnelbroker.net/).  After I registered a tunnel, it was a simple matter of copying all the addresses into TomatoUSB.  After I did that it all worked!

I could ping any public IPv6 address, any public IPv6 address could ping any of my internal machines.  And my laptop would prefer IPv6 if the site supported it.
