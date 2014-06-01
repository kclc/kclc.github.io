---
layout: page
title: Home
---
{% include JB/setup %}

## About

このサイトは開成コンピュータ部の公式サイトです。

## Recent Updates

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


