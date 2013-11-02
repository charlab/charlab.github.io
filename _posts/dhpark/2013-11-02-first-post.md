---
layout: post
title: "Setting up Git on Tera"
description: ""
category: "tutorial"
tags: [tutorial, blog, Tera]
author: dhpark
---
{% include JB/setup %}

Since Eric went over using git on Windows, I'll talk about setting up git on Linux, more specifically on Tera. Knowing how to use Linux comes in quite handy, especially if you are interested in Digital. Even if you are not strictly programming, lot of the software tools for digital circuits seem to run in Linux based on my observation. Unfortunately, working in command line environment isn't someting that get taught often at Mudd. Even some of my CS friends don't know how to do things in command line.


If you are not familar with *Tera* `tera.eng.hmc.edu`, it is the Engineering compute server with **96** cores of Intel Xeon CPU. If you can manage to setup an account for clinic or a class, it can come in handy for running some programs or simulations. Once you have a tera account, you can ssh into it using [PUTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) and [Xming](http://sourceforge.net/projects/xming/).


Once you are on, you want to setup the git repository on your directory. First generate an SSH key for your tera account using the instructions [here](https://help.github.com/articles/generating-ssh-keys#platform-linux).

Next, get the **SSH clone URL** from Charlab's github site. It should be: `git@github.com:charlab/charlab.github.io.git`. Now clone the charlab repository by running:
```
git clone git@github.com:charlab/charlab.github.io.git
```
This should have cloned the charlab files onto the directory you ran the code.


If all the files were grabbed successfully, then go into the folder using `cd charlab.github.io/`. You can 
look at the folders in the directory using `ls` command:
```
[dhpark@tera blog]$ cd charlab.github.io/
[dhpark@tera charlab.github.io]$ ls
404.html      categories.html   images      people.html  README.md
archive.html  changelog.md      _includes   _plugins     rss.xml
assets        _config.yml       index.md    _posts       sitemap.txt
atom.xml      _drafts           _layouts    project      tags.html
blog          History.markdown  pages.html  Rakefile
[dhpark@tera charlab.github.io]$ ls
404.html      categories.html   images      people.html  README.md
archive.html  changelog.md      _includes   _plugins     rss.xml
assets        _config.yml       index.md    _posts       sitemap.txt
atom.xml      _drafts           _layouts    project      tags.html
blog          History.markdown  pages.html  Rakefile
[dhpark@tera charlab.github.io]$
```


Navigate into `_posts` folder with `cd _posts`, create your a folder with `mkdir <filename>`. Pick your favorite text editor and start blogging! I recommend `gedit` since it is very similar to your traditional text editor with all the GUI interface. I am trying to get used to using `gvim` right now since it has a GUI interface with the functionality of `vim`. 


You use the exact same commands for adding and commiting files on git.
