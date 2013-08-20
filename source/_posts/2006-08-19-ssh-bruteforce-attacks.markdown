---
author: David Hogue
comments: false
date: 2006-08-19 22:24:22+00:00
layout: post
slug: ssh-bruteforce-attacks
title: SSH Bruteforce attacks
wordpress_id: 148
categories:
- Technology
tags:
- old-blog
---

Anyone who runs a server on *nix probably gets a fair number errors in their ssh logs from invalid logins.  A couple weeks ago I got curious and decided to see what username and password combinations are being attempted.  My logs looked something like this:


    
     User www-data from 203.101.80.210 not allowed because not listed in AllowUsers : 1 time(s)
     User backup from 203.101.80.210 not allowed because not listed in AllowUsers : 1 time(s)
     User games from 203.101.80.210 not allowed because not listed in AllowUsers : 1 time(s)
     User mail from 203.101.80.210 not allowed because not listed in AllowUsers : 1 time(s)
     User danny from 203.101.80.210 not allowed because not listed in AllowUsers : 1 time(s)
     User uucp from 165.132.32.79 not allowed because not listed in AllowUsers : 3 time(s)
     User bin from 165.132.32.79 not allowed because not listed in AllowUsers : 3 time(s)
     User root from 67.108.254.49.ptr.us.xo.net not allowed because not listed in AllowUsers : 5 time(s)
     User root from 218.247.185.242 not allowed because not listed in AllowUsers : 66 time(s)



This server gets hundreds of connection attempts per day.  Almost every one of them are from ssh bruteforce scripts.  Now I'm not too worried about my server.  It's fairly locked down.  More on that later.



#### How I logged the passwords






  1. Go get [this SSH patch](http://www.notatla.org.uk/SOFTWARE/SSH_mods_2004-08-06.txt)


  2. Get [OpenSSH](http://www.openssh.com/) [3.8.1p1](ftp://ftp.openbsd.org/pub/OpenBSD/OpenSSH/portable/openssh-3.8.1p1.tar.gz).  _3.8 is over 2 years old and may not be secure!_


  3. Apply patch, configure, make


  4. Change the port my real sshd listens on by putting a "Port 12345" in my sshd_config (to connect to the real ssh use "ssh servername -p 12345")


  5. Set my new ssh to listen on "Port 2222" and add an iptables redirect from 22 to 2222 (this is so that the daemon can run as an unprivileged user)


  6. Run my new sshd with the command "./sshd -f sshd_config -D -e 2>&1 | tee -a -i sshd.log"


  7. Wait 5 days



Here's a small sample of what I got:

    
    www-data/1
    www-data/123
    www-data/1234
    www-data/12345
    www-data/123456
    www-data/123456
    www-data/123456
    www-data/admin
    www-data/admin123
    www-data/adminadmin
    www-data/changeme
    www-data/changeme
    www-data/data
    www-data/letmein
    www-data/newpass
    www-data/passwd
    www-data/passwd123
    www-data/password
    www-data/password
    www-data/q1w2e3r4t5
    www-data/qwerty
    www-data/test
    www-data/test123
    www-data/www
    www-data/www-data



I've zipped up the full list in case anyone is curious: [passwords.zip](http://vorpal.cc/blog/wp-content/uploads/2006/08/passwords.zip).  There are 63,377 passwords there collected August 6th to the 11th.  A total of 5 days.  And this is certainly not a busy server.



#### Locking down SSH


Here's why I'm not concerned by this:




  1. My password for ssh on this server is very strong: 15 characters upper, lower, numbers, symbols, and punctuation.


  2. I have "PermitRootLogin no" in my sshd_config


  3. "AllowUsers david": the only valid username for ssh is mine


  4. "PasswordAuthentication no" or "ChallengeResponseAuthentication no": The only way to log through ssh is with my private ssh key (id_dsa)


  5. My private key is encrypted and needs a password


  6. I am the only user on the box with a valid password.  /etc/shadow looks like this: "root:*:13313:0:9999:7:::"


  7. I have [Logwatch](http://www.logwatch.org/) sending me daily notices of anomalous log activity



Moral of the story: **Use strong passwords**, especially on anything that is accessable from the internet.  My password is probably a bit overkill.  However because I use a private key to login, I've only needed to use it twice; both when it was off the network.
