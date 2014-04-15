---
layout: post
title: "Example Blog Post Errors"
description: ""
category: "tutorial"
tags: [jekyll, blog]
author: jspjut
---
{% include JB/setup %}

This morning I noticed an issue preventing some of the blog posts to
show up correctly on the live website. 
These errors happened mostly because some of the blog authors use the
github in-browser editor to create posts rather than testing locally
using jekyll before pushing the updates to the live site. 
This time, there were 3 errors with 3 different levels of severity.

## Blog post location
This was the most critical error that caused `jekyll` to throw up. The
issue was that one of the blog posts had be placed in the root
directory instead of being placed inside the `_posts` directory where
it belongs. You can place blog posts in any subdirector structure
within `_posts` that you want, but a post with the filename formatted
like the following should not be in the root directory:
`2014-04-15-example-blog-post-errors.md`

## Spaces in blog post filename
This error was serious and caused the blog posts affect to show in the
blog list, but the contents of the file would only generate an error
when viewed.
There should not be spaces in the blog post file name. To avoid errors
like this, I use the rakefile to create new blog posts and just fill
in the blanks. A post file should be
`2014-04-15-example-blog-post-errors.md` and **NOT**
`2014-04-15-example blog post errors.md`.

## Block Text
This error would just result in a slightly worse formatted post while
all the content was available, and I'd consider it a more minor
issue. The important thing to realize is that blocks of text or code
should use the tripple \` rather than a tripple ' character. That is
the backtick to the left of the `1` key on most American keyboards.
