---
layout: layouts/base.njk
title: Poetry
permalink: /works/poetry/
---

<ul>
{% for item in collections.poetry %}
  <li><a href="{{ item.url }}">{{ item.data.title }}</a></li>
{% endfor %}
</ul>
