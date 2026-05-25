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

<!-- Empty state message -->
<div class="articles-empty" id="articlesEmpty" style="display:none;">
  <p>Articles coming soon … <a href="#" id="showAllLink">read something that is available</a>.</p>
</div>

<!-- ===== Lets Connect Footer ===== -->
<footer class="site-footer">
  <p class="footer-text">Let's connect</p>
  <div class="badge-row">
    <a href="https://bs.linkedin.com/in/almill36" class="badge-link badge-linkedin" target="_blank" rel="noopener">LinkedIn</a>
    <a href="https://github.com/AIMHigheR36" class="badge-link badge-github" target="_blank" rel="noopener">GitHub</a>
    <a href="/" class="badge-link badge-website">aimhigher.dev</a>
    <a href="https://public.tableau.com/app/profile/alejandro.miller7081/vizzes" class="badge-link badge-tableau" target="_blank" rel="noopener">Tableau</a>
  </div>
</footer>

<script>
  (function() {
    const bar = document.getElementById('categoryBar');
    const leftArrow = document.getElementById('catArrowLeft');
    const rightArrow = document.getElementById('catArrowRight');
    const cards = document.querySelectorAll('.article-card');
    const btns = document.querySelectorAll('.cat-btn');
    const emptyMsg = document.getElementById('articlesEmpty');
    const showAllLink = document.getElementById('showAllLink');

    // ---- Filtering ----
    function filter(category) {
      let hasVisible = false;
      cards.forEach(card => {
        const cats = card.getAttribute('data-category').split(',');
        if (category === 'all' || cats.includes(category)) {
          card.style.display = '';
          hasVisible = true;
        } else {
          card.style.display = 'none';
        }
      });
      emptyMsg.style.display = hasVisible ? 'none' : 'block';
    }

    btns.forEach(btn => {
      btn.addEventListener('click', function() {
        btns.forEach(b => b.classList.remove('active'));
        this.classList.add('active');
        filter(this.getAttribute('data-category'));
        // Scroll the button into view within the category bar
        this.scrollIntoView({ behavior: 'smooth', block: 'nearest', inline: 'center' });
      });
    });

    showAllLink.addEventListener('click', function(e) {
      e.preventDefault();
      btns.forEach(b => b.classList.remove('active'));
      const allBtn = document.querySelector('.cat-btn[data-category="all"]');
      if (allBtn) {
        allBtn.classList.add('active');
        filter('all');
      }
    });

    // ---- Arrow scrolling ----
    function updateArrows() {
      const scrollLeft = bar.scrollLeft;
      const maxScroll = bar.scrollWidth - bar.clientWidth;
      leftArrow.style.visibility = scrollLeft <= 1 ? 'hidden' : 'visible';
      rightArrow.style.visibility = scrollLeft >= maxScroll - 1 ? 'hidden' : 'visible';
    }

    leftArrow.addEventListener('click', () => bar.scrollBy({ left: -200, behavior: 'smooth' }));
    rightArrow.addEventListener('click', () => bar.scrollBy({ left: 200, behavior: 'smooth' }));
    bar.addEventListener('scroll', updateArrows);
    window.addEventListener('resize', updateArrows);
    updateArrows();
    if (bar.scrollWidth <= bar.clientWidth) {
      leftArrow.style.display = 'none';
      rightArrow.style.display = 'none';
    }

    // ---- Initial filter from URL parameter ----
    const params = new URLSearchParams(window.location.search);
    const categoryParam = params.get('category');
    if (categoryParam) {
      // Find the button that matches the parameter
      const targetBtn = document.querySelector(`.cat-btn[data-category="${categoryParam}"]`);
      if (targetBtn) {
        // Activate that button and filter
        btns.forEach(b => b.classList.remove('active'));
        targetBtn.classList.add('active');
        filter(categoryParam);
        // Scroll the category bar so the button is visible
        targetBtn.scrollIntoView({ behavior: 'smooth', block: 'nearest', inline: 'center' });
      } else {
        // Unknown category – fallback to All
        const allBtn = document.querySelector('.cat-btn[data-category="all"]');
        if (allBtn) {
          allBtn.classList.add('active');
          filter('all');
        }
      }
    }
    // If no parameter, the All button is already active from the HTML, so do nothing extra.
  })();
</script>
