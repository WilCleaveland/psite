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

    <div class="upwork-testimonial">
      <p>"Wil has been very effective at maximizing revenue from our internal lists and generating winning funnel copy for all our brands — in both good times and bad.</p>
      <p>In a niche where we're constantly facing challenges to consistently scale on cold traffic, <strong>Wil's performance is one constant we've been extremely thankful to count on!</strong>"</p>
      <img src="{{ '/images/nate.webp' | relative_url }}" alt="Nathan Hopkins">
      <p class="source">— Nathan Hopkins, <a href="https://sicurobrands.com/">Sicuro Brands</a></p>
    </div>
    {% include theme/linkedin-recommendations.html show_divider=true offset=0 limit=2 %}
    <hr class="upwork-testimonial-divider">

    <div class="upwork-testimonial">
      <p><strong>"I've outsourced to other writers here and there, but Wil is my go-to guy when I need to outsource copy.</strong></p>
      <p>He has excellent research skills. He's self-motivated. He hits deadlines. And he writes damn good copy.</p>
      <p>I can toss him an idea and let him run with it without ever worrying if we're on the same page. He knows how to take feedback. He asks the right questions. Overall, he just "gets it."</p>
      <p>His abilities are quickly eclipsing "up-and-comer" status, and I strongly recommend you work with him. (In fact, I often send him referrals.)</p>
      <p>Just please don't send him too much work... I'd like to keep working with Wil for a long time. ;-)"</p>
      <img src="{{ '/images/ryan_healy.jpg' | relative_url }}" alt="Ryan Healy">
      <p class="source">— Ryan Healy, <a href="https://upsender.com/">Upsender</a></p>
    </div>
    {% include theme/linkedin-recommendations.html show_divider=true offset=2 limit=2 %}
    <hr class="upwork-testimonial-divider">

    <div class="upwork-testimonial">
      <p>"As a guy who built an affiliate company, solely through email, from $0 to $300,000 every month, if I could choose 1 guy to do it again with from scratch. 1 no nonsense writer. 1 entrepreneur to create compelling email, converting sales copy and day 1 profitable product funnels that can scale.</p>
      <p><strong>I'd choose Wil because he was with me and built it to those staggering numbers along side me.</strong></p>
      <p>There are just not that many people that have written, tested, and analyzed the amount of copy Wil has.</p>
      <p>There are even fewer who have critiqued thousands of cold traffic emails, and made them work, while leading a team of 8 writers to do the same.</p>
      <p>Frankly, copy is a key component that makes the rain inside any business. Most can't produce it. Less can analyze it. Less can teach it. Less can grow a profit line with it, day in and day out.</p>
      <p>Wil does all of that.</p>
      <p>Period."</p>
      <img src="{{ '/images/lou_cozzolino.jpg' | relative_url }}" alt="Lou Cozzolino">
      <p class="source">— Lou Cozzolino, <a href="https://lonesurvivalist.com/">Lone Survivalist</a></p>
    </div>
    {% include theme/linkedin-recommendations.html show_divider=true offset=4 limit=2 %}
    <hr class="upwork-testimonial-divider">

    <div class="upwork-testimonial">
      <p>"I'm super impressed with Wil's ability to <strong>deliver quality copy on time and on budget.</strong> He is easy to work with and gets things right the first time (e.g. doesn't require handholding or endless revisions)."</p>
      <img src="{{ '/images/drew_kossoff.jpg' | relative_url }}" alt="Drew Kossoff">
      <p class="source">— Drew Kossoff, <a href="https://rainmakeradventures.com/">Rainmaker Ad Ventures</a></p>
    </div>
    {% include theme/linkedin-recommendations.html show_divider=true offset=6 limit=2 %}
    <hr class="upwork-testimonial-divider">

    <div class="upwork-testimonial">
      <p>"I was referred to Wil by Ryan Healy, whose schedule was too full to accommodate our landing page project. Wil had just started freelancing full-time, so his portfolio wasn't quite as filled out as the other copywriters we looked at. <strong>But when we got back the first draft of our copy, we knew we'd made the right choice.</strong></p>
      <p>His process was seamless, and he got the tone and voice for our audience almost perfect right out of the gate. He even found a great clinical study for an ingredient in our product that we had yet to discover ourselves. Then he integrated it right into the copy.</p>
      <p>We're anxiously counting down till launch day so we can test it out!"</p>
      <img src="{{ '/images/ben_steuart.jpg' | relative_url }}" alt="Ben Steuart">
      <p class="source">— Ben Steuart, <a href="https://steuartsnatural.health/">Steuart's Natural Health</a></p>
    </div>
    {%- comment -%}
      LinkedIn recommendations are managed in _data/linkedin_recommendations.yml.
      The first 8 are interleaved between the five hardcoded testimonials
      above (2 + 2 + 2 + 2). This trailing include catches everything from
      offset 8 onwards — currently 2 cards, plus any future additions.
    {%- endcomment -%}
    {% include theme/linkedin-recommendations.html show_divider=true offset=8 %}
  </div>
</section>

<!-- ============================================================ -->
<!-- RESUME                                                        -->
<!-- ============================================================ -->
<section id="resume" class="upwork-section">
  <div class="container">
    <h2 class="upwork-section-title">Resume</h2>
    <iframe class="upwork-resume-frame" src="{{ '/images/wilcleavelandresume.pdf' | relative_url }}#toolbar=0"></iframe>
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
