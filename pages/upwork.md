---
layout: upwork
title: "Wil Cleaveland — Marketer & Copywriter"
permalink: "/upwork/"
description: "Appalachian direct-response and ecommerce marketer. $10M+ in revenue over the last 5 years."
noindex: true
---

<!-- ============================================================ -->
<!-- JUMP NAV (sticky, at very top of page)                        -->
<!-- ============================================================ -->
<nav class="upwork-jump-nav">
  <div class="container">
    <a href="#about" class="upwork-jump-item">About</a>
    <a href="#work" class="upwork-jump-item">Work Samples</a>
    <a href="#testimonials" class="upwork-jump-item">Testimonials</a>
    <a href="#resume" class="upwork-jump-item">Resume</a>
  </div>
</nav>

<!-- ============================================================ -->
<!-- HERO                                                          -->
<!-- ============================================================ -->
<section id="about" class="upwork-section upwork-hero">
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-12 col-md-10">
        <img src="{{ '/assets/images/avatar/avatar.jpg' | relative_url }}" alt="Wil Cleaveland" class="avatar" width="120" height="120">
        <h1>I help online businesses move up and to the right.📈</h1>
        <p class="intro-copy">Press the easy-button for scaling across both owned and paid media with someone who's done it before. Here are two quick videos from my best long-term partners.</p>
        <div class="upwork-cta">
          <a href="https://calendly.com/wccleaveland" target="_blank" rel="noopener" class="status">
            <svg class="status-light" fill="#d4a744" viewBox="0 0 8 8">
              <circle cx="4" cy="4" r="3"></circle>
            </svg>
            <span class="status-text">Book a Call</span>
          </a>
        </div>
        <div class="video-stack">
          <div class="video-stack-item">
            <div class="ratio ratio-16x9">
              <iframe src="https://streamyard.com/e/d4tdg38dsezp" frameborder="0" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
            </div>
          </div>
          <div class="video-stack-item">
            <div class="ratio ratio-16x9">
              <iframe src="https://player.vimeo.com/video/1063842926?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write; encrypted-media" style="position:absolute;top:0;left:0;width:100%;height:100%;" title="Adam's Testimonial - Sicuro Brands"></iframe>
            </div>
          </div>
        </div>
        <script src="https://player.vimeo.com/api/player.js"></script>
      </div>
    </div>
  </div>
</section>

<!-- ============================================================ -->
<!-- WORK                                                          -->
<!-- ============================================================ -->
<section id="work" class="upwork-section">
  <div class="container">
    <h2 class="upwork-section-title">Work Samples</h2>

    {%- comment -%} Collect every unique category across all work items {%- endcomment -%}
    {% assign cards = site.work | sort: 'date' | reverse %}
    {% assign all_cats = "" | split: "" %}
    {% for card in cards %}
      {% for cat in card.categories %}
        {% unless all_cats contains cat %}
          {% assign all_cats = all_cats | push: cat %}
        {% endunless %}
      {% endfor %}
    {% endfor %}
    {% assign all_cats = all_cats | sort %}

    <div class="uw-filter" id="uw-filter">
      <button class="active" data-filter="all" type="button">All</button>
      {% for cat in all_cats %}
        <button data-filter="{{ cat | slugify }}" type="button">{{ cat }}</button>
      {% endfor %}
    </div>

    <div class="row" id="uw-grid">
      {% for card in cards %}
        {%- assign slugs = "" -%}
        {%- for cat in card.categories -%}
          {%- assign cat_slug = cat | slugify -%}
          {%- assign slugs = slugs | append: cat_slug | append: " " -%}
        {%- endfor -%}
        <div class="col-12 col-md-6 col-lg-4 mb-3 uw-card-wrapper" data-categories="{{ slugs | strip }}">
          {% include theme/card.html project=card %}
        </div>
      {% endfor %}
    </div>
  </div>
</section>

<!-- ============================================================ -->
<!-- TESTIMONIALS                                                  -->
<!-- ============================================================ -->
<section id="testimonials" class="upwork-section">
  <div class="container">
    <h2 class="upwork-section-title">Testimonials</h2>

    {%- comment -%}
      All testimonials (curated + LinkedIn) live in _data/testimonials.yml.
      Order on the page == order in that file.
    {%- endcomment -%}
    {% include theme/testimonials.html style="upwork" %}
  </div>
</section>

<!-- ============================================================ -->
<!-- RESUME                                                        -->
<!-- ============================================================ -->
<section id="resume" class="upwork-section">
  <div class="container">
    <h2 class="upwork-section-title">Resume</h2>
    {% include theme/resume-content.html %}
  </div>
</section>

<!-- ============================================================ -->
<!-- WORK FILTER JS                                                -->
<!-- ============================================================ -->
<script>
  (function () {
    const filterContainer = document.getElementById('uw-filter');
    const grid = document.getElementById('uw-grid');
    const cards = document.querySelectorAll('.uw-card-wrapper');
    if (!filterContainer || !cards.length) return;

    const validFilters = Array.from(filterContainer.querySelectorAll('button'))
      .map((b) => b.getAttribute('data-filter'));

    function shuffle(arr) {
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        const t = arr[i]; arr[i] = arr[j]; arr[j] = t;
      }
      return arr;
    }

    function applyFilter(filter) {
      filterContainer.querySelectorAll('button').forEach((b) => {
        b.classList.toggle('active', b.getAttribute('data-filter') === filter);
      });

      if (grid) grid.classList.add('is-filtering');

      setTimeout(() => {
        const visible = [];
        cards.forEach((card) => {
          const cats = (card.getAttribute('data-categories') || '').split(' ').filter(Boolean);
          const show = filter === 'all' || cats.indexOf(filter) !== -1;
          card.classList.toggle('hidden', !show);
          if (show) visible.push(card);
        });
        shuffle(visible);
        cards.forEach((card) => {
          const idx = visible.indexOf(card);
          card.style.order = idx >= 0 ? idx : '';
        });

        requestAnimationFrame(() => {
          if (grid) grid.classList.remove('is-filtering');
        });
      }, 200);
    }

    filterContainer.addEventListener('click', (e) => {
      const btn = e.target.closest('button');
      if (!btn) return;
      applyFilter(btn.getAttribute('data-filter'));
    });
  })();
</script>
