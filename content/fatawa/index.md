---
layout: layouts/base.njk
title: Fatawa
permalink: /fatawa/
nav: true
---

# Fatawa

<p class="page-sub">Rulings and responses from Shaykh Sulayman al-Alwan</p>

<p><a href="/fatawa/sessions/">Browse by session</a></p>

<ul class="entry-list">
{% for s in collections.fatawa | reverse %}
  <li><a href="{{ s.url }}">
    {{ s.data.title }}
    {% if s.data.source %}<span class="entry-meta">{{ s.data.source }}</span>{% endif %}
  </a></li>
{% endfor %}
</ul>
