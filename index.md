---
layout: page
title: aoxu
tagline: 一个懂产品的攻城狮。
---
{% include JB/setup %}
###最新文章
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

###[订阅源](http://feeds.uri.lv/aoxu)

