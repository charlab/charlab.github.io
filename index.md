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

## Recent Blog Posts

  <ul class="posts">
  {% for post in site.posts limit:10 %}
    <li><span>{{ post.date | date_to_string }}</span> 
      <span>
	{% assign post_author = site.post_authors[post.author] %}
	<a href="{{ site.url }}/people.html#{{ post.author }}">
	  {{ post_author.display_name }}</a>
      </span>&raquo;
    <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>


