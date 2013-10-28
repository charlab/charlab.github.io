---
layout: post
title: "Linking to Other Blog Posts"
description: ""
category: "tutorial"
tags: [tutorial, blog, jekyll]
author: jspjut
---
{% include JB/setup %}

A quick piece of information that might be useful, if you want to
link to another blog post on this web site, you should create a link
like this:

     [test link]({{ "{% post_url jspjut/2013-10-22-post-name " }}%})

where `test link` is the text you want the link to show up under.
