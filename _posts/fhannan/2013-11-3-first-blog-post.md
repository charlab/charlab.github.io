---
layout: post
title: "First blog post"
description: ""
category: "tutorial"
tags: [tutorial, blog, jekyll]
author: fpjhannan
---
{% include JB/setup %}

{% highlight text %}
Hi! I'm Fabiha. This is my first post in the repository charlab.github.io. 

In terms of my research interests, I would like to focus on modeling digital architecture, through various mediums. I am also interested in working on parallel processors and GPUs. Although I would prefer using software to model hardware, I am fine with programming/coding.

Donghyeon explained using Github on Linux and the engineering server Tera. Like Eric, I downloaded the Github desktop application Windows and used both jekyll and Git Shell.

Although most tips seem to have been covered by Prof Spjut, Eric, and Donghyeon (I referred to their posts to make mine), here are some more basic tips that may help:

- Github does not allow empty folders. You can create a new file in a folder or the repository and add the new folder name when naming the file (in the directory statement above the file editor), like so:

charlab.github.io / _posts / ____ or cancel                                    *This is what you see initially.
charlab.github.io / _posts / fhannan or cancel                                 *Add/name the new folder.
charlab.github.io / _posts / fhannan / 2013-10-22-first-blog-post.md or cancel *You should see the folder added in blue and with a hyperlink. Name the file.


Eric also mentioned adding your name to config.yml. Here is the line to be edited (add your name to the array):

"author_ids: [jspjut, estorm, dhpark]" should be  "author_ids: [jspjut, estorm, dhpark, fhannan]" (I added my name to the list)

...
(later in the code)

fhannan :
    display_name : Fabiha Hannan
    job_title : B.S. Engineering 2016
    bio : 'Fabiha is taking E85.'
    email : fhannan@g.hmc.edu           <-- I added my email address
    web : 
    twitter : 
    github : fpjhannan                  <-- I added my Github username
    linkedin : 


Another edit to be made is in the index.html file in the 'blog' folder. I added my name in the following line:

blog_author_ids: [estorm, dhpark, jspjut] --> blog_author_ids: [estorm, dhpark, fhannan, jspjut]




I think that's it for the issues I had or points that I felt needed to be clarified. Good luck to everyone else on making their blog posts!
{% endhighlight %}
