---
layout: default
title: Articles
permalink: /articles/
---

# Articles

Here I write about finance, systems thinking, and building things that last.

{% if site.posts.size > 0 %}
  {% for post in site.posts %}
    <article class="post-preview">
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
      <p>{{ post.excerpt | strip_html }}</p>
      <a href="{{ post.url }}">Read more →</a>
    </article>
  {% endfor %}
{% else %}
  <p>No articles yet. Check back soon!</p>
{% endif %}
