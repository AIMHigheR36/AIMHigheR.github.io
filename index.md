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

<!-- ===== LATEST ARTICLES ===== -->
<section class="latest-articles">
  <h2 class="latest-title">Latest Articles</h2>
  <div class="latest-grid">
    {% for post in site.posts limit:3 %}
      <a href="{{ post.url }}" class="latest-card-square">
        <span class="latest-card-date">{{ post.date | date: "%b %d, %Y" }}</span>
        <h3 class="latest-card-heading">{{ post.title }}</h3>
      </a>
    {% endfor %}
  </div>
</section>

<!-- ===== FOOTER (quick links) ===== -->
<footer class="site-footer">
  <p class="footer-text">Let's connect</p>
  <div class="badge-row">
  <a href="https://bs.linkedin.com/in/almill36" class="badge-link badge-linkedin" target="_blank" rel="noopener">LinkedIn</a>
  <a href="https://github.com/AIMHigheR36" class="badge-link badge-github" target="_blank" rel="noopener">GitHub</a>
  <a href="/" class="badge-link badge-website">aimhigher.dev</a>
  <a href="https://public.tableau.com/app/profile/alejandro.miller7081/vizzes" class="badge-link badge-tableau" target="_blank" rel="noopener">Tableau</a>
</div>
</footer>
