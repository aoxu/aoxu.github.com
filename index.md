---
layout: page
title: Hello World!
tagline: Supporting tagline
---
{% include JB/setup %}
<h2> {{ page.title }}</h2>
<p>recent posts</p>
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



