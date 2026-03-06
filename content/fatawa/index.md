---
layout: layouts/base.njk
title: Fatawa
permalink: /fatawa/
nav: true
---

# Fatawa

<ul>
{% for s in collections.fatawa | reverse %}
  <li><a href="{{ s.url }}">{{ s.data.title }}</a></li>
{% endfor %}
</ul>
