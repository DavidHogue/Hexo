---
author: David Hogue
comments: false
date: 2005-12-30 19:51:53+00:00
layout: post
slug: linuxs-logical-volume-management
title: Linux's Logical Volume Management
wordpress_id: 318
categories:
- Technology
tags:
- old-blog
---

So, as I sit here waiting for the error reporting dialog to finish from my most recent Visual Studio crash, I think to myself what could I do with the time.  I know!  I'll write on my blog that I haven't updated in over a week.*  Today I am going to write about Logical Volume Management or LVM in Linux

For a while now I've had this little computer that I wanted to turn into a file server.  I had big plans for a SATA RAID controller and a bunch of large drives...  Lately it has become apparent that I am never going to get it all in one big chunk.  Instead I have decided to slowly grow it by adding one drive at a time.

For Christmas I asked for and received a new drive.  I put this in the server and started it up.  Now normally I would make a partition on the disk format it and be on my way.  The trouble with that is that I end up with several different partitions and I have to balance my files between these partitions.  I can't put all my files in the same folder structure which is annoying

LVM to the rescue!  What LVM does is create a volume group (VG) that can span partitions and disks.  Then you can create logical volumes (LVs) inside it.  The logical volumes behave much like partitions on a standard disk. You need to format them with a filesystem ext3 or reiserfs.  You can add, delete, and resize the logical volumes provided you can resize the filesystem.

Now, when I get a new drive I just need to connect it, add it to the volume group, and expand the logical volume.  Most of the common filesystems can grow to fill the new space.  Reiserfs can do it with a single command while mounted.

The downside to all of this is that I have no redundancy at all.  If any of the drives fail I will probably lose everything.  However, LVM can be run on top of a standard hardware or software raid setup.  I can also remove a disk from the volume group if I suspect it is going bad.

All the tools I needed came with Ubuntu.  They commands are logical enough (vgcreate, vgdisplay, lvcreate, and lvresize for example) There is a thorough faq at [tldp.org](http://www.tldp.org/HOWTO/LVM-HOWTO/).  I've another good link around here somewhere that I'll post it if I can find it.

_*I've been busy, OK?  As an aside: I have trouble focusing on one topic here._



