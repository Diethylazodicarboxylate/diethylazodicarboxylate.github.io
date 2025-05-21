---
layout: default
title: Writeups
permalink: /writeup/
---

# Writeups

<ul>
  {% for item in site.writeup %}
    <li><a href="{{ item.url }}">{{ item.title }}</a> — {{ item.date | date: "%Y-%m-%d" }}</li>
  {% endfor %}
</ul>

