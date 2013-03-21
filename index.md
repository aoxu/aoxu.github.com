---
layout: page
title: aoxu
tagline: 一个懂产品的工程师。
---
{% include JB/setup %}
<p>最新文章</p>
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



