---
layout: layouts/base.njk
title: Fatawa
permalink: /fatawa/
nav: true
---

# Fatawa

<p class="page-sub">Rulings and responses from Shaykh Sulayman al-Alwan</p>

<p><a href="/fatawa/sessions/">Browse by session</a></p>

<div class="sort-toggle" id="fatawa-sort">
  <button type="button" data-order="new" class="active">Newest first</button>
  <button type="button" data-order="old">Oldest first</button>
</div>

<ul class="entry-list reversed" id="fatawa-list">
{% for s in collections.fatawa %}
  <li><a href="{{ s.url }}">
    {{ s.data.title }}
    {% if s.data.source %}<span class="entry-meta">{{ s.data.source }}</span>{% endif %}
  </a></li>
{% endfor %}
</ul>

<script>
  (function() {
    var list = document.getElementById('fatawa-list');
    var buttons = document.querySelectorAll('#fatawa-sort button');
    var saved = localStorage.getItem('alwan_fatawa_order') || 'new';

    function applyOrder(order) {
      list.classList.toggle('reversed', order === 'new');
      buttons.forEach(function(b) {
        b.classList.toggle('active', b.dataset.order === order);
      });
    }

    buttons.forEach(function(b) {
      b.addEventListener('click', function() {
        localStorage.setItem('alwan_fatawa_order', b.dataset.order);
        applyOrder(b.dataset.order);
      });
    });

    applyOrder(saved);
  })();
</script>
