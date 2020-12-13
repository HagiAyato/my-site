---
layout: page
title: Tags
permalink: /tags/
---

<h3>タグ一覧</h3>
{% for post in site.posts %}
  {% if post.tags contains page.tag %}
    <li><span>{{ post.date | date:"%Y-%m-%d" }}</span>
    <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endif %}
{% endfor %}