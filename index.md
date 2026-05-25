---
layout: default
---

<!-- ===== HERO ===== -->
<section class="hero" markdown="0">
  <div class="hero-content">
    {% if site.author-image %}
      <img src="{{ site.author-image }}" alt="Alejandro Miller" class="hero-photo" width="120" height="120">
    {% endif %}
    <h1 class="hero-name">Alejandro Miller</h1>
    <p class="hero-tagline">A quietly determined financial professional who builds systems that outlast him.</p>
  </div>
</section>

<!-- ===== ABOUT ===== -->
<section class="about" markdown="0">
  <h2 class="about-title">About</h2>
  <p class="about-text">
    I'm a financial professional turning data into lasting systems. I currently work at Scotiabank, 
    building the skills to become a Financial Data Architect. I believe in quiet competence, 
    thoughtful analysis, and technology that serves people over time.
  </p>
</section>

<!-- ===== LATEST ARTICLE ===== -->
<section class="latest-article">
  <h2 class="latest-title">Latest Article</h2>
  {% assign latest = site.posts.first %}
  {% if latest %}
    <article class="latest-card">
      <h3 class="latest-heading">
        <a href="{{ latest.url }}">{{ latest.title }}</a>
      </h3>
      <p class="latest-date">{{ latest.date | date: "%B %d, %Y" }}</p>
      <p class="latest-excerpt">{{ latest.excerpt | strip_html | truncatewords: 25 }}</p>
      <a href="{{ latest.url }}" class="latest-read-more">Read more →</a>
    </article>
  {% else %}
    <p class="latest-empty">No articles yet. Check back soon.</p>
  {% endif %}
</section>

<!-- ===== FOOTER (quick links) ===== -->
<footer class="site-footer">
  <p class="footer-text">Let's connect</p>
  <div class="badge-row">
    <a href="https://bs.linkedin.com/in/almill36" class="badge-link badge-linkedin" target="_blank" rel="noopener">LinkedIn</a>
    <a href="https://github.com/AIMHigheR36" class="badge-link badge-github" target="_blank" rel="noopener">GitHub</a>
    <a href="/" class="badge-link badge-website">aimhigher.dev</a>
  </div>
</footer>
