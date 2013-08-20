---
author: David Hogue
comments: true
date: 2010-12-16 18:34:54+00:00
layout: post
slug: some-parameters-for-msdeploy-exe
title: Some Parameters for msdeploy.exe
wordpress_id: 12
categories:
- Software Development
tags:
- msdeploy
---

I've been trying to get msdeploy working for me at work.  Hopefully it will be able to replace some PowerShell/Robocopy scripts I have for updating our servers.

To deploy/update an existing site to local:
`msdeploy.exe -verb:sync -source:Package="<Package.zip>" -test:iisApp='<Website>'`

To deploy/update an existing site to a remote server:
`msdeploy.exe -verb:sync -source:Package="<Package.zip>" -test:iisApp='<Website>',computername=<Server>,userName='<Domain>\<Username>',password='<Password>'`

To recycle a local web:
`msdeploy.exe -verb:sync -source:recycleApp="<Website>" -dest:auto`

To recycle a remote web:
`msdeploy.exe -verb:sync -source:recycleApp -dest:recycleApp="<Website>\<App>",computername=<Server>,userName="<Domain>\<Username>",password="<Password>"`

And to make msdeploy not delete existing files when upgrading, add `-enableRule:DoNotDeleteRule`

Maybe this will help somebody out.  It took me quite a bit of poking around to get everything working like I wanted.
