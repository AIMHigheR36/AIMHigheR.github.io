---
layout: default
title: Articles
permalink: /articles/
---

<!-- ===== Category Filter Bar ===== -->
<div class="category-bar-wrapper">
  <button class="cat-arrow cat-arrow-left" id="catArrowLeft" aria-label="Scroll categories left">&#8249;</button>
  <div class="category-bar" id="categoryBar">
    <button class="cat-btn active" data-category="all">All</button>
    <button class="cat-btn" data-category="the-person">The Person</button>
    <button class="cat-btn" data-category="the-technical-craft">The Technical Craft</button>
    <button class="cat-btn" data-category="the-bridge">The Bridge</button>
    <button class="cat-btn" data-category="the-platform">The Platform</button>
    <button class="cat-btn" data-category="book-reflections">Book Reflections</button>
  </div>
  <button class="cat-arrow cat-arrow-right" id="catArrowRight" aria-label="Scroll categories right">&#8250;</button>
</div>

<!-- ===== Article Cards ===== -->
<div class="articles-list" id="articlesList">
  {% for post in site.posts %}
    <article class="article-card" data-category="{{ post.categories | join: ',' }}">
      <h2 class="article-card__title">
        <a href="{{ post.url }}">{{ post.title }}</a>
      </h2>
      <p class="article-card__date">{{ post.date | date: "%B %d, %Y" }}</p>
      {% if post.excerpt %}
        <p class="article-card__excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
      {% endif %}
      <a href="{{ post.url }}" class="article-card__read-more">Read more →</a>
    </article>
  {% endfor %}
</div>

<!-- ===== Filtering & Scroll Script ===== -->
<script>
  (function() {
    const bar = document.getElementById('categoryBar');
    const leftArrow = document.getElementById('catArrowLeft');
    const rightArrow = document.getElementById('catArrowRight');
    const cards = document.querySelectorAll('.article-card');
    const btns = document.querySelectorAll('.cat-btn');

    // ---- Filtering ----
    function filter(category) {
      cards.forEach(card => {
        const cats = card.getAttribute('data-category').split(',');
        if (category === 'all' || cats.includes(category)) {
          card.style.display = '';
        } else {
          card.style.display = 'none';
        }
      });
    }

    btns.forEach(btn => {
      btn.addEventListener('click', function() {
        btns.forEach(b => b.classList.remove('active'));
        this.classList.add('active');
        filter(this.getAttribute('data-category'));
      });
    });

    // ---- Arrow scrolling ----
    function updateArrows() {
      const scrollLeft = bar.scrollLeft;
      const maxScroll = bar.scrollWidth - bar.clientWidth;
      // show/hide left arrow
      leftArrow.style.visibility = scrollLeft <= 1 ? 'hidden' : 'visible';
      // show/hide right arrow
      rightArrow.style.visibility = scrollLeft >= maxScroll - 1 ? 'hidden' : 'visible';
    }

    leftArrow.addEventListener('click', () => {
      bar.scrollBy({ left: -200, behavior: 'smooth' });
    });

    rightArrow.addEventListener('click', () => {
      bar.scrollBy({ left: 200, behavior: 'smooth' });
    });

    bar.addEventListener('scroll', updateArrows);
    window.addEventListener('resize', updateArrows);

    // Initial check
    updateArrows();

    // If bar content doesn't overflow, hide arrows completely
    if (bar.scrollWidth <= bar.clientWidth) {
      leftArrow.style.display = 'none';
      rightArrow.style.display = 'none';
    }
  })();
</script>
