---
layout: default
title: Articles
permalink: /articles/
---

<div class="articles-list">
  {% for post in site.posts %}
    <article class="article-card">
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
