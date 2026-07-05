---
layout: layouts/base.njk
title: Sciences
permalink: /sciences/
---

# Sciences

<p class="page-sub">Browse works and fatawa by subject</p>

<ul class="entry-list">
{% for s in collections.sciences %}
  <li><a href="{{ s.url }}">{{ s.data.title }}</a></li>
{% endfor %}
</ul>
