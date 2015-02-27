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

<p><a href="/blog/">All blog posts</a></p>

<h2>Publications</h2>

<ul>
<li><a href="None">Dong-hyeon Park</a>, <a href="None">Akhil Bagaria</a>, <a href="None">Fabiha Hannan</a>, <a href="None">Eric Storm</a>, <a href="http://josef.spjut.me">Josef Spjut</a>;
<strong>Sphynx: A Shared Instruction Cache Exporatory Study</strong>,
<em>Tech Report, arXiv:1412.1140</em>,
December 3, 2014.
<a href="http://arxiv.org/abs/1412.1140">paper</a> <a class="ec" href="javascript:" onclick="e=document.getElementById('bibtr2').style;e.display=(e.display=='block'?'none':'block')">Bibtex</a><span id="bibtr2" class="b" style="display: none;"><pre>@inproceedings{parkbagaria14,
 author = { Dong-hyeon Park and Akhil Bagaria and Fabiha Hannan and Eric Storm and Josef Spjut },
 title = { {Sphynx: A Shared Instruction Cache Exporatory Study} },
 year = {2014},
 booktitle = {Tech Report, arXiv:1412.1140}
}
</pre></span></li>
</ul>
