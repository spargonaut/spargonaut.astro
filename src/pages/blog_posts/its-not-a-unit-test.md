---
layout: ../../layouts/MarkdownPostLayout.astro

title: 'Its not a unit test - repost'
pubDate: 2019-01-26
tags: ['testing']
categories: []
---

This post is a reposting of one of my favorite blog posts about unit tests.  It was originally posted by one of my colleagues at ThoughtWorks, but it came down when he decided to redesign his blog.  I found it when I was starting out with unit testing and TDD and I think these rules really helped me to write some really good tests.  Small, fast, and easy to maintain.

I'm repositing here, without permission, because I think its a great post, with some good rules and descriptions of what unit tests _aren't_.  
Pablosan, if you're reading this, and want me to take it down, let me know.

Below is the post, unedited (except for the part about the comments).

-----

**Riffing on Jeff Foxworthy’s “…you might be a redneck”,  I present “…it’s not a Unit Test”:**  
SalientBlue by Pablosan  

**If it requires manual setup…** it’s not a Unit Test.  

**If it requires manual intervention...** it’s not a Unit Test.  

**If it requires a network connection...** it’s not a Unit Test.  

**If it requires a container...** it’s not a Unit Test.  

**If it requires a database...** it’s not a Unit Test.  

**If it accesses a file system...** it’s not a Unit Test.  

**If it requires a service to be available...** it’s not a Unit Test.  

**If it takes longer than a millisecond to run...** it’s not a Unit Test.  

**If it lacks assertions...** it’s not a Unit Test.  

**If it breaks on certain dates or at certain times...** it’s not a Unit Test.  

**If it requires a UI...** it’s not a Unit Test.  

**If it fails intermittently for an unknown reason...** it’s not a Unit Test.  

**If it passes intermittently for an unknown reason...** it’s not a Unit Test.  

**If it fails when you look at it funny...** it’s not a Unit Test.  

**If the mock setup code dwarfs the actual test code...** it’s not a Unit Test.  

**If you have to mock beyond immediate dependencies...** it’s not a Unit Test.  

I think that’s a pretty good start. What have I missed? Are there any that make you cringe?  
~~Let your voice be heard: leave a comment!~~  

-------  

I crossed out that last line b/c I don't have a comments section.  Feel free to give me some feed via other methods though!

I think they're some pretty good rules.  Not hard and fast rules, but really good guidelines to follow.  
Over the years they've helped me to write good, small _unit_ tests (fast too!). Hopefully, they'll help you too.

