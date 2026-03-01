---
layout: layouts/base.njk
title: Fatawa
permalink: /fatawa/
nav: true
---

<ul>
{% for item in collections.fatawa %}
  <li><a href="{{ item.url }}">{{ item.data.title }}</a></li>
{% endfor %}
</ul>
