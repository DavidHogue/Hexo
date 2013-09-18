title: Arguments in favor of source control comments  
date: 2013-09-18 13:14:50  
tags:  
- source control  
- process  
- documentation  
categories: Software Development  
---



I recently wrote out some thoughts about why comments are important when checking in to source control (in this case Subversion, but git or any other system would be the same.) They weren't effective in changing any minds at the time, but I thought I'd put them online anyway.

None of this is new, in fact it's pretty basic stuff that most developers pick up before they ever get hired.



1.  Your company probably has a coding standars document that says to include some brief comments in the commit message about why the changes were made. And if you don't have a document, you should make one.

2.  Source control comments create a history for the code that can be referred to later to help in understanding why things were done the way they way they were. Even on personal projects where I will be the only one to ever see the code, I commit frequently and add comments for my own reference. For example, check out [this very small project from John Ressig][1], nobody else has committed or forked the repository, yet he still writes comments.

[1]: <https://github.com/jeresig/datacook/commits/master>

1.  The comments don't need to be lengthy, in fact shorter is usually better. All it should take is a few seconds to write one short sentence in the window that is already open. Something motivated you to make the change, type it in.

2.  [This page on MSDN][2] has this to say: "When something goes wrong, you can use good check-in comments to help identify where it went wrong and how to fix it more quickly. Even if nothing goes wrong, you'll be able to easily see what changes you made and why you made them."

[2]: <http://msdn.microsoft.com/en-us/library/ee371247(v=expression.30).aspx>



I feel that we all as developers would benefit by being able to see what everyone else is working on. The commit comments may not be ideal to dispel any mystery, but they do help, a lot. Even if we had meetings and extensive documentation, I would argue that the commit messages are useful for explaining details and tracking down why specifics in the code were implemented one way or another.


