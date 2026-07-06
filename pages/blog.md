---
layout: basic
title: "Blog"
description: "Notes on direct-response email, lifecycle marketing, and building AI-augmented marketing systems."
permalink: "/blog/"
align: "center"
---

<div style="max-width: 640px; margin: 0 auto;">
{% assign posts = site.posts | sort: 'date' | reverse %}
{% if posts.size == 0 %}
  <p style="text-align:center;">First post coming soon.</p>
{% endif %}
{% for post in posts %}
  <article style="margin-bottom: 32px;">
    <h3 style="margin-bottom: 4px;"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
    <p style="color: var(--color-base-text-2); font-size: 0.9rem; margin-bottom: 8px;">{{ post.date | date: "%B %-d, %Y" }}</p>
    <p>{{ post.description | default: post.excerpt | strip_html | truncate: 180 }}</p>
  </article>
{% endfor %}
</div>
