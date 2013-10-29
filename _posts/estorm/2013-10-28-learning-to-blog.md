---
layout: post
title: "Learning to blog"
description: ""
category: "tutorial"
tags: [tutorial, blog, jekyll]
author: estorm
---
{% include JB/setup %}

Here's a test post that hopefully won't crash the site. I tried to install Jekyll on my Windows machine, but it is pretty tricky. I'll fiddle with it later and also try it out on Linux. 

***

If you are trying to create your own page, here's some tips I discovered. Disclaimer: I used Windows to do this, so your experiece could be different. Disclaimer 2: A lot of this may be repeated from Prof. Spjut's posts.
* I used the GitHub desktop application. It provides a GUI for a lot of stuff I would normally do with the command line.
* I also used Git Shell because you can't run git commands from cmd in Windows.
* To add something new, use `git add .`. You also have to run this even if you are just editing a file. This adds your files to the "staging area".
* Next you need to commit. This records a snapshot of all of your files. git requires that you make a comment for every commit. So if you just type `git commit`, it will open a text editor and ask you to make a comment there. I personally prefer to do inline comments, which you can do with the -m flag, so `git commit -m "This comment is made in-line"`
* Finally, you have to push your changes. You can do this with `git push`, but I opted to use the sync button on the GitHub desktop application rather than the command line. 
* You need to make changes to _config.yml. You need to add your username to the list of `author_ids` and I'd recommend at least adding your email to your post_authors entry.
* I repeatedly got an email from GitHub telling me that the page build failed. This was because I had not verified my email address on GitHub. It turns out it isn't enough to just make an account with your email address, you need to go through a quick verification process to ensure you are who you say you are. If you've done that, hopefully your changes will show up!
* If you don't see any initial changes, wait a few minutes and refresh the page and your content should show up. 
* The [markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)is really awesome if you are trying to figure out how to add formatting to your post.
