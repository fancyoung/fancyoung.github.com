---
layout: page
title: "笔记"
date: 2015-11-11 11:11
comments: false
sharing: true
footer: true
---
一些笔记与cheatsheet。

<ul>
{% for note in site.notes %}
  {% if note.url != '/notes/index.html' %}
  <li><a href="{{site.baseurl}}{{ note.url }}">{{ note.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>
