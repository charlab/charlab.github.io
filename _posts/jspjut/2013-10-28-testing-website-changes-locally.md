---
layout: post
title: "Testing Website Changes Locally"
description: ""
category: "tutorial"
tags: [tutorial, blog, jekyll]
author: jspjut
---
{% include JB/setup %}

You can run jekyll locally while writing your blog posts. This is
extremely useful for ensuring you don't break the web site by
uploading your blog post. Please note that sometimes, even if your
website works locally, it could break when uploaded to github (because
github uses a slightly different version of jekyll sometimes).
The following instructions are adapted from [the jekyll-bootstrap
quick start
guide](http://jekyllbootstrap.com/usage/jekyll-quick-start.html#toc_6)

First, to edit or add posts to the site, you will need to clone the
repository. If you are a member of the github organization group, then
you should clone the repository in authenticated mode with the
following command:

    git clone git@github.com/charlab/charlab.github.io.git

Which will create a new local repository in `charlab.github.io` in
whichever directory you invoked that command. Next you will need ruby
installed on your machine. Many systems come with it preinstalled, and
you can check for its existence by running `ruby --version` at the
command line.

This web site uses [jekyll](http://jekyllrb.com/) so you will want to
install it next. The recommended method is to use the following
command line:

    gem install jekyll

Once installed, you should change into the charlab repository:

    cd charlab.github.io

Finally, you should run the jekyll server:

    jekyll server -w

The `-w` argument tells the server to automatically update when it
sees changes to files, such as a new blog post being added. If you run
the server without `-w` then you will need to stop it (probably with
ctrl-c) and start it again each time you want to see the changes you
made.

One important note is that changes to the `_config.yml` file require
restarting the server to be seen, even if you run with the `-w`
argument.


