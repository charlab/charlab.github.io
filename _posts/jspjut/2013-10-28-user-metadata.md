---
layout: post
title: "User Metadata"
description: ""
category: "tutorial"
tags: [tutorial, blog, jekyll]
author: jspjut
---
{% include JB/setup %}

In [my other post]({% post_url jspjut/2013-10-22-how-to-create-a-blog-post %})
I discussed how to create a blog post. However, I
assumed that some meta data was already available. If you are new to
this research group and want to be able to create blog posts, then you
should create an author entry for the `_config.yml` file so that your
information is available for the web site to fill in. Below is the
example of my author information. If you don't include any particular
piece of information, then the field will not appear next to your
posts. The only required pieces of information are your name, title,
and a biography.

{% highlight text %}
  jspjut :
    display_name : Josef Spjut
    job_title : Professor
    bio : 'Josef is a professor of engineering at Harvey Mudd College
        and a consulting researcher for NVIDIA. He received his Ph.D. from
	University of Utah and his B.S in Computer Engineering from
    	University of California Riverside.'
    email : jspjut@g.hmc.edu
    web : http://jspjut.github.io/
    twitter : josefspjut
    github : jspjut
    linkedin : josefspjut
{% endhighlight %}

A recommended `job_title` for a student would be something like 
`"B.S. Engineering 2015"`.
If you want to put in the info yourself, you should edit the 
`_config.yml` file in the root directory of the website, otherwise you
can just send the information to Prof. Spjut and he'll enter it for
you.

