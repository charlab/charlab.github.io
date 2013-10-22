---
layout: page
title: CHAR Lab
tagline: Computing Research
---
{% include JB/setup %}

The CHAR Lab was established by Professor Josef Spjut to give
undergraduate students a chance to participate in research before
completing their degree.
While all areas of computing are of interest to the group, in
particular we have focused on Computer Architecture and developing
classwork and projects for new undergraduate learning experiences.
This website exists as a way for the participating students to post
updates as they make progress.

This website is still in progress...
    
## Sample Posts

This blog contains sample posts which help stage pages and blog data.
When you don't need the samples anymore just delete the `_posts/core-samples` folder.

    $ rm -rf _posts/core-samples

Here's a sample "posts list".

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



