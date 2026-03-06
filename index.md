---
layout: layouts/base.njk
title: Ta'weel
---

This project aims to preserve knowledge with clarity, attribution, and transparency.

<div class="search-container">
  <input type="search" id="search-input" placeholder="Search scholars, fatawa, poetry…" autocomplete="off">
  <div class="search-results" id="search-results"></div>
</div>

<script>
(function () {
  const input = document.getElementById('search-input');
  const results = document.getElementById('search-results');
  let index = null;

  input.addEventListener('input', function () {
    const q = this.value.trim().toLowerCase();
    results.innerHTML = '';
    if (!q) return;
    if (!index) {
      fetch('/search-index.json')
        .then(r => r.json())
        .then(data => { index = data; render(q); });
    } else {
      render(q);
    }
  });

  function render(q) {
    const hits = index.filter(item => item.title.toLowerCase().includes(q)).slice(0, 10);
    if (!hits.length) {
      results.innerHTML = '<p class="search-result">No results.</p>';
      return;
    }
    results.innerHTML = hits.map(item =>
      `<a class="search-result" href="${item.url}"><span class="result-type">${item.type}</span>${item.title}</a>`
    ).join('');
  }
})();
</script>
