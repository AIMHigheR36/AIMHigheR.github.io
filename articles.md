---
layout: default
title: Articles
permalink: /articles/
---

# Articles

{% for post in site.posts %}
- **[{{ post.title }}]({{ post.url }})** — {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
