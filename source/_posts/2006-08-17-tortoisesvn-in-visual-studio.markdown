---
author: David Hogue
comments: false
date: 2006-08-17 02:44:25+00:00
layout: post
slug: tortoisesvn-in-visual-studio
title: TortoiseSVN in Visual Studio
wordpress_id: 142
categories:
- Software Development
tags:
- old-blog
---

**Update October 2 2007:** Someone posted a link to [Gary's Bit Patterns](http://garrys-brain.blogspot.com/2006/11/visual-studio-2005-and-tortoisesvn.html) where there is a settings file you can just import instead of doing all these manual steps.

I also fixed the quotes in the commands so they shouldn't cause trouble anymore.



* * *



Ever wanted to use [TortoiseSVN](http://tortoisesvn.net/) from [VisualStudio?](http://msdn.microsoft.com/vstudio/)  Well, now you can! 1



#### Contents






  1. Introduction


  2. Menu


  3. Toolbar


  4. Icons


  5. Done





#### Introduction



I have created a toolbar with Update, Log, Check, Revert, and Commit ![tortoise toolbar](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoisedone.png).  The commands work the same as if you right clicked the folder containing the solution.  Follow the steps below to get your own tortoise toolbar.



#### Menu



Select Tools > External Tools... from the Visual Studio menu.  Add a tool using the following info.

[![adding tortoise to the menu](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoisesetup.thumbnail.png)](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoisesetup.png)







FieldValue




 
#1



Title
Tortoise &Update



Command
C:Program FilesTortoiseSVNbinTortoiseProc.exe



Arguments
/command:update /path:"$(SolutionDir)" /notempfile




#2



Title
Tortoise &Log



Command
C:Program FilesTortoiseSVNbinTortoiseProc.exe



Arguments
/command:log /path:"$(SolutionDir)" /notempfile




#3



Title
Tortoise Check for &Modifications



Command
C:Program FilesTortoiseSVNbinTortoiseProc.exe



Arguments
/command:repostatus /path:"$(SolutionDir)" /notempfile




#4



Title
Tortoise Re&vert



Command
C:Program FilesTortoiseSVNbinTortoiseProc.exe



Arguments
/command:revert /path:"$(SolutionDir)" /notempfile




#5



Title
Tortoise &Commit



Command
C:Program FilesTortoiseSVNbinTortoiseProc.exe



Arguments
/command:commit /path:"$(SolutionDir)" /notempfile








  * $(SolutionDir) is the path to the directory the solution is in


  * /notempfile is required when running from the command line


  * The ampersands make that letter a shortcut for use in the menu



You should have the commands in your tools menu.  Try them out and make sure they all work. 

[![tools menu with tortoise commands](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoisemenu.thumbnail.png)](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoisemenu.png)



#### Toolbar



Add the toolbar by right-clicking your toolbar and select customize.  Make a new toolbar and call it Tortoise.  Close the customize window and right-click again, this time adding the tortoise toolbar.

Now go back to customize, select the commands tab, and scroll down to the tools category.  You should see a bunch of commands like External Command 1, External Command 2, etc.  Drag those on to your new toolbar.  This may require some trial and error.

You can rename the commands in the toolbar by selecting a button with the customize window open, then clicking the Modify Selection button, then Name:.

[![changing the toolbar names](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoisetoolbar.thumbnail.png)](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoisetoolbar.png)



#### Icons



Now to add the icons.  I haven't found an easy way to do this yet.  Here's what I did: 

Go to [http://tortoisesvn.tigris.org/svn/tortoisesvn/trunk/src/Resources/](http://tortoisesvn.tigris.org/svn/tortoisesvn/trunk/src/Resources/) (user guest, blank password).  Browse to the image you want then right click the image and select Copy Image (note: this was on Firefox).  With the customize window open right click the button and select Paste Button Image.

The pasted image won't be transparent, so you need to edit the image.  Right-click and select Edit Button Image.  Then erase all the black area.

[![erasing the transparent part of the icons](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoiseicons.thumbnail.png)](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoiseicons.png)



#### Done



Your toolbar should look something like this: ![tortoise toolbar](https://davidhogue.com/blog/wp-content/uploads/2006/08/tortoisedone.png)



* * *







  1. Well, you could have before if you wanted.  I'm sure I'm not the first to come up with this.  I know a few people already do this because it came up on the TortoiseSVN mailing list a while back.↩






[![kick it on DotNetKicks.com](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http%3a%2f%2fvorpal.cc%2fblog%2fdevelopment%2ftortoisesvn-in-visual-studio)](http://www.dotnetkicks.com/kick/?url=http%3a%2f%2fvorpal.cc%2fblog%2fdevelopment%2ftortoisesvn-in-visual-studio)
