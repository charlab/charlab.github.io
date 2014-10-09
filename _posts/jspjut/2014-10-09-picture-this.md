---
layout: post
title: "Picture this!"
author: jspjut
description: "Pictures on the site"
category: "website"
tags: [website, blog]
---
{% include JB/setup %}

I added support for individuals to have pictures on the blog
today. It's relatively simple to add your picture if you're a charlab
member. First you need to be sure you have a subdirectory in the
`images` directory in the github repository, then you should upload an
image there. Finally, you should put the name of your image in the
`_config.yml` file so that the website will know where to find it.
For example, here is what the relevant part of my entry in the
`_config.yml` looks like:

```
post_authors :
  jspjut :
    display_name : Josef Spjut
    image : jspjut.jpg
```
