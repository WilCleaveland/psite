---
layout: upwork
title: "Wil Cleaveland — Direct-Response Marketer & Copywriter"
permalink: "/"
description: "Appalachian direct-response and ecommerce marketer. $10M+ in revenue over the last 5 years."
meta_description: "Responsible for $10M+ in revenue in the past 5 years."
meta_title: "Wil Cleaveland — Marketer in Roanoke, VA"
---

<!-- ============================================================ -->
<!-- JUMP NAV (sticky, at very top of page)                        -->
<!-- ============================================================ -->
<nav class="upwork-jump-nav" id="home-jump-nav">
  <div class="container">
    <a href="#about" class="upwork-jump-item">About</a>
    <a href="#work" class="upwork-jump-item">Work Samples</a>
    <a href="#testimonials" class="upwork-jump-item">Testimonials</a>
    <a href="#resume" class="upwork-jump-item">Resume</a>
    <a href="#ebook" class="upwork-jump-item">Free Guide</a>
    <!-- The CTA pill is hidden by default; IntersectionObserver below
         adds .is-revealed to the parent nav once the hero CTA scrolls
         off-screen, fading this pill in as the persistent conversion
         shortcut. -->
    <a href="https://calendly.com/wccleaveland" target="_blank" rel="noopener"
       class="upwork-jump-item upwork-jump-item-cta upwork-jump-cta-reveal">
      Book a Call
    </a>
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
<!-- FREE EBOOK OPT-IN                                             -->
<!-- ============================================================ -->
<section id="ebook" class="upwork-section">
  <div class="container">
    <h2 class="upwork-section-title">Free Email-Copy Guide</h2>
    <p class="ebook-lede">Five lessons from $5M+ in email revenue — written for ecommerce operators and direct-response marketers who want to scale list income without burning out their audience. Drop your email and I'll send it over.</p>
    <div class="ebook-card">
      <img src="{{ '/images/ebook.png' | relative_url }}" alt="5 Lessons From $5M In Email Revenue" class="ebook-cover">
      <div class="ebook-form-wrapper">
        <script src="https://f.convertkit.com/ckjs/ck.5.js"></script>
        <form action="https://app.kit.com/forms/7785183/subscriptions" class="seva-form formkit-form" method="post" data-sv-form="7785183" data-uid="c28846bbbb" data-format="inline" data-version="5" data-options="{&quot;settings&quot;:{&quot;after_subscribe&quot;:{&quot;action&quot;:&quot;message&quot;,&quot;success_message&quot;:&quot;Success! Check your inbox. :) &quot;,&quot;redirect_url&quot;:&quot;&quot;}}}" min-width="400 500 600 700 800">
          <div data-style="clean">
            <ul class="formkit-alert formkit-alert-error" data-element="errors" data-group="alert"></ul>
            <div data-element="fields" data-stacked="false" class="seva-fields formkit-fields">
              <div class="formkit-field">
                <input class="formkit-input" name="email_address" aria-label="Email Address" placeholder="Your best email address" required="" type="email">
              </div>
              <button data-element="submit" class="formkit-submit formkit-submit">
                <div class="formkit-spinner"><div></div><div></div><div></div></div>
                <span>Send me the guide</span>
              </button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</section>

<!-- ============================================================ -->
<!-- WORK FILTER JS + DYNAMIC JUMP-NAV CTA REVEAL                  -->
<!-- ============================================================ -->
<script>
  (function () {
    const filterContainer = document.getElementById('uw-filter');
    const grid = document.getElementById('uw-grid');
    const cards = document.querySelectorAll('.uw-card-wrapper');
    if (!filterContainer || !cards.length) return;

    const validFilters = Array.from(filterContainer.querySelectorAll('button'))
      .map((b) => b.getAttribute('data-filter'));

    // Fisher–Yates shuffle, used so the matching cards always end up in a
    // visibly different order after a click — even if the same subset was
    // already on screen.
    function shuffle(arr) {
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        const t = arr[i]; arr[i] = arr[j]; arr[j] = t;
      }
      return arr;
    }

    function applyFilter(filter) {
      // Mark the active button immediately so the chip click feels responsive.
      filterContainer.querySelectorAll('button').forEach((b) => {
        b.classList.toggle('active', b.getAttribute('data-filter') === filter);
      });

      // Fade currently-visible cards out, then swap hidden state + shuffle
      // order on the new visible set, then fade back in.
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

    // Deep-link support: a URL like /?filter=sicuro-brands#work lands on
    // the homepage, jumps to the work section via the hash, and arrives
    // with that filter pre-selected. We apply the filter synchronously
    // (no 200ms fade) so the visitor never sees the unfiltered grid
    // flash through before the filter takes effect.
    const params = new URLSearchParams(window.location.search);
    const initialFilter = params.get('filter');
    if (initialFilter && validFilters.indexOf(initialFilter) !== -1) {
      filterContainer.querySelectorAll('button').forEach((b) => {
        b.classList.toggle('active', b.getAttribute('data-filter') === initialFilter);
      });
      cards.forEach((card) => {
        const cats = (card.getAttribute('data-categories') || '').split(' ').filter(Boolean);
        const show = initialFilter === 'all' || cats.indexOf(initialFilter) !== -1;
        card.classList.toggle('hidden', !show);
      });
    }
  })();

  // Reveal the Book a Call pill in the jump nav as soon as the user has
  // scrolled past the hero's actual Book a Call button. The IntersectionObserver
  // watches .upwork-cta (the hero's CTA wrapper); when it leaves the viewport
  // (accounting for the sticky jump nav's own height via rootMargin), we add
  // `.is-revealed` to the jump nav so the CSS fades the pill in. Scrolling
  // back up to the hero retracts the pill again.
  (function () {
    const heroCta = document.querySelector('.upwork-cta');
    const jumpNav = document.getElementById('home-jump-nav');
    if (!heroCta || !jumpNav || !('IntersectionObserver' in window)) return;

    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        jumpNav.classList.toggle('is-revealed', !entry.isIntersecting);
      });
    }, { rootMargin: '-72px 0px 0px 0px', threshold: 0 });

    observer.observe(heroCta);
  })();
</script>

<!-- ============================================================ -->
<!-- EBOOK SECTION STYLING                                         -->
<!-- ============================================================ -->
<style>
  .ebook-lede {
    max-width: 740px;
    margin: -16px auto 36px;
    text-align: center;
    font-size: 1.1rem;
    line-height: 1.6;
    color: var(--color-base-text-2);
  }
  .ebook-card {
    max-width: 820px;
    margin: 0 auto;
    background: var(--color-base-bg-2);
    border: 1px solid var(--color-base-bg-3);
    border-radius: 16px;
    padding: 40px;
    display: grid;
    grid-template-columns: 220px 1fr;
    gap: 40px;
    align-items: center;
    box-shadow:
      0 1px 2px rgba(63, 45, 20, 0.05),
      0 12px 28px -8px rgba(63, 45, 20, 0.14),
      0 6px 14px -4px rgba(63, 45, 20, 0.06);
  }
  .ebook-cover {
    width: 100%;
    height: auto;
    display: block;
    border-radius: 6px;
    box-shadow: 0 6px 18px rgba(63, 45, 20, 0.18);
  }
  .ebook-form-wrapper .formkit-form {
    max-width: 100%;
  }
  .ebook-form-wrapper .formkit-input {
    width: 100%;
    padding: 14px 16px;
    border: 1px solid var(--color-base-bg-3);
    border-radius: 8px;
    background: #ffffff;
    font-size: 1rem;
    color: var(--color-base-text);
    margin-bottom: 12px;
  }
  .ebook-form-wrapper .formkit-input:focus {
    outline: none;
    border-color: #9e4a2b;
  }
  .ebook-form-wrapper .formkit-submit {
    width: 100%;
    padding: 14px 28px;
    background: #9e4a2b;
    color: #ffffff;
    border: none;
    border-radius: 8px;
    font-weight: 600;
    font-size: 1.02rem;
    letter-spacing: 0.02em;
    cursor: pointer;
    transition: background 0.15s ease, transform 0.15s ease;
    box-shadow: 0 6px 16px rgba(63, 45, 20, 0.18);
  }
  .ebook-form-wrapper .formkit-submit:hover {
    background: #7a3920;
    transform: translateY(-1px);
  }
  .ebook-form-wrapper .formkit-submit > span {
    color: #ffffff;
  }
  /* Hide the ConvertKit-branded "powered by" footer for a cleaner look. */
  .ebook-form-wrapper .formkit-powered-by-convertkit-container { display: none; }

  @media (max-width: 640px) {
    .ebook-card {
      grid-template-columns: 1fr;
      padding: 28px 22px;
      gap: 24px;
      text-align: center;
    }
    .ebook-cover { max-width: 220px; margin: 0 auto; }
  }
</style>
