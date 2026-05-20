# Harvest LinkedIn Recommendations — Bookmarklet

This is an internal-only doc (excluded from Jekyll's build via `_config.yml`).
The bookmarklet below scrapes the recommendations visible on **your own**
LinkedIn `/details/recommendations/` page and outputs a YAML block you can
paste into `_data/testimonials.yml` (the single source of truth for all
testimonials on the site). **For each pasted entry, add `source: linkedin`
on its own line** — that flag is what triggers the LinkedIn-blue accent
strip and corner badge on the rendered card.

Because the script runs on a page you're already viewing (logged-in,
authorized for your own data), it doesn't bypass any LinkedIn auth and
isn't doing anything LinkedIn's ToS prohibits — it's the same as right-
clicking → "View Source" and reading the markup yourself, just faster.

## One-time setup

1. Create a new bookmark in your browser's bookmarks bar.
2. Name it: **Harvest LinkedIn Recs**
3. For the URL, paste the entire single-line `javascript:...` blob in the
   "Bookmarklet (single line)" section below. Make sure no line breaks
   sneak in — most browsers reject multi-line bookmarklet URLs.

## How to use

1. Log in to LinkedIn.
2. Go to:
   `https://www.linkedin.com/in/wilcleaveland/details/recommendations/`
3. Make sure all your recommendations are visible. If LinkedIn shows a
   "Show more" button, click it until everything is on screen. (Scroll
   to the bottom in case any are lazy-loaded.)
4. Click the **Harvest LinkedIn Recs** bookmark.
5. You'll see an alert telling you how many recommendations were found.
   The YAML is copied to your clipboard (and also logged to the browser
   console — open with `Cmd+Opt+J` on Mac if you need to inspect).
6. Open `_data/testimonials.yml` and paste the YAML into the place where
   you want each new card to appear (order in the file == order on the
   page). **For each pasted entry, add a `source: linkedin` line** —
   without it, the card renders as a curated testimonial instead of a
   LinkedIn one.
7. Manually save headshots to `/images/linkedin/` if you want photos —
   right-click each recommender's photo on LinkedIn → "Save image as…" →
   save to `assets/images/linkedin/firstname-lastname.jpg`. Then add a
   `photo: /images/linkedin/firstname-lastname.jpg` line to that entry.
   (Photos are optional — entries without a `photo` field render with a
   LinkedIn-blue monogram circle instead.)

## Heads up

LinkedIn rewrites its DOM regularly. If the bookmarklet stops finding
recommendations (alert says "Found 0"), the selectors below need updating.
Open the LinkedIn page, inspect a recommendation card, and adjust the
selector list in `findRecCards()` or the field extractors below.

The recommendation body text on LinkedIn is sometimes truncated with a
"…see more" link until you click it. If you see truncated text in the
harvested YAML, expand each recommendation on LinkedIn first (click
"…see more" on each card) before running the bookmarklet.

## Bookmarklet (single line)

Paste this exact line as the bookmark's URL:

```
javascript:(async function(){var myHandle=(window.location.pathname.split('/in/')[1]||'').split('/')[0];var anchors=Array.from(document.querySelectorAll('a[href*="/in/"]'));var otherAnchors=anchors.filter(function(a){var p=a.pathname||'';var h=(p.split('/in/')[1]||'').split('/')[0];return h&&h!==myHandle;});if(otherAnchors.length===0){alert('No recommender profile links found. Open the console (Cmd+Opt+J) and verify you are on your /in/USERNAME/details/recommendations/ page with recommendations expanded.');return;}var seen=new Set();var recs=[];otherAnchors.forEach(function(anchor){var el=anchor;var container=null;for(var i=0;i<10&&el&&el!==document.body;i++){el=el.parentElement;if(!el)break;var fullText=(el.innerText||'').trim();if(fullText.length>180){container=el;break;}}if(!container||seen.has(container))return;var inLinks=container.querySelectorAll('a[href*="/in/"]');var distinctOthers=new Set();inLinks.forEach(function(a){var p=a.pathname||'';var h=(p.split('/in/')[1]||'').split('/')[0];if(h&&h!==myHandle)distinctOthers.add(h);});if(distinctOthers.size>1)return;seen.add(container);var nameSpan=anchor.querySelector('span[aria-hidden="true"]')||anchor;var name=(nameSpan.innerText||'').trim().split('\n')[0].trim();if(!name||name.length<2)return;var profile_url=anchor.href.split('?')[0].replace(/\/$/,'')+'/';var leafSpans=Array.from(container.querySelectorAll('span'));var longest='';leafSpans.forEach(function(s){if(s.children.length>0){var onlyBr=true;for(var j=0;j<s.children.length;j++){if(s.children[j].tagName!=='BR'){onlyBr=false;break;}}if(!onlyBr)return;}var t=(s.innerText||'').trim();if(t.length>longest.length)longest=t;});if(longest.length<60){var fallback=(container.innerText||'').trim();fallback=fallback.split('\n').filter(function(ln){return ln.trim()!==name.trim();}).join('\n').trim();if(fallback.length>longest.length)longest=fallback;}longest=longest.replace(/\s*…see more\s*$/i,'').replace(/\s*see more\s*$/i,'').trim();if(longest.length<60)return;var headline='';var hs=leafSpans;var jobRe=/\bat\b|\bCEO\b|\bCMO\b|\bCOO\b|\bdirector\b|\bmanager\b|\bfounder\b|\bowner\b|\bvp\b|\bhead of\b|\bpresident\b|\bcopywriter\b|\bmarketer\b|\bconsultant\b/i;for(var k=0;k<hs.length;k++){var t=(hs[k].innerText||'').trim();if(t.length>5&&t.length<200&&t!==name&&t!==longest&&jobRe.test(t)){headline=t;break;}}if(!headline){for(var m=0;m<hs.length;m++){var t=(hs[m].innerText||'').trim();if(t.length>10&&t.length<200&&t!==name&&t.length<longest.length/2){headline=t;break;}}}var relationship='';var dateStr='';var contextRe=/(worked|managed|reported|was|is)\s+(with|directly|on|to)/i;var dateRe=/([A-Z][a-z]+\s+\d{1,2},\s+\d{4}|[A-Z][a-z]+\s+\d{4})/;for(var n=0;n<hs.length;n++){var t=(hs[n].innerText||'').trim();if(t.length>10&&t.length<300&&t!==name&&t!==longest&&t!==headline){var dm=t.match(dateRe);var hasContext=contextRe.test(t);if(dm||hasContext){if(dm){dateStr=dm[1];t=t.replace(dm[1],'').replace(/[·\s]+$/,'').trim();}if(hasContext){relationship=t;}break;}}}recs.push({name:name,headline:headline,relationship:relationship,date:dateStr,text:longest,profile_url:profile_url});});if(recs.length===0){console.log('Diagnostic — anchors to other profiles:',otherAnchors.length);console.log('Otheranchors:',otherAnchors.slice(0,3).map(function(a){return{href:a.href,text:(a.innerText||'').slice(0,80)};}));alert('Found '+otherAnchors.length+' profile links but no recommendation bodies. Open Cmd+Opt+J console for diagnostics, then share output with Wil/the dev.');return;}function yq(s){return (s||'').replace(/"/g,'\\"');}var yaml=recs.map(function(r){var lines=['- name: "'+yq(r.name)+'"'];if(r.headline)lines.push('  headline: "'+yq(r.headline)+'"');if(r.relationship)lines.push('  relationship: "'+yq(r.relationship)+'"');if(r.date)lines.push('  date: "'+yq(r.date)+'"');if(r.profile_url)lines.push('  profile_url: "'+yq(r.profile_url)+'"');lines.push('  text: |');var paragraphs=r.text.split(/\n\s*\n+/);paragraphs.forEach(function(p,idx){p.split('\n').forEach(function(ln){if(ln.trim())lines.push('    '+ln.trim());});if(idx<paragraphs.length-1)lines.push('');});return lines.join('\n');}).join('\n\n');console.log('=== LinkedIn Recommendations YAML ===\n\n'+yaml+'\n\n=== End ===');try{await navigator.clipboard.writeText(yaml);alert('Found '+recs.length+' recommendation(s). YAML copied to clipboard. (Also in console — Cmd+Opt+J)');}catch(e){alert('Found '+recs.length+' recommendation(s). Clipboard blocked — open Cmd+Opt+J console to copy the YAML manually.');}})();
```

## Bookmarklet (readable version — for editing later)

This version is **structure-agnostic**: instead of relying on LinkedIn's
class names (which change every few months), it walks the DOM looking for
anchors that link to *other* LinkedIn profiles, then bubbles up to find the
nearest container that holds substantial body text. That makes it resilient
to LinkedIn refactors.

```js
javascript:(async function () {
  var myHandle = (window.location.pathname.split('/in/')[1] || '').split('/')[0];

  // Step 1: find every <a> on the page that links to someone else's
  // /in/ profile (not yours). Each recommendation has one of these.
  var anchors = Array.from(document.querySelectorAll('a[href*="/in/"]'));
  var otherAnchors = anchors.filter(function (a) {
    var p = a.pathname || '';
    var h = (p.split('/in/')[1] || '').split('/')[0];
    return h && h !== myHandle;
  });

  if (otherAnchors.length === 0) {
    alert('No recommender profile links found. Open the console (Cmd+Opt+J) and verify you are on your /in/USERNAME/details/recommendations/ page with recommendations expanded.');
    return;
  }

  // Step 2: for each "other profile" anchor, walk up the DOM until we hit
  // an ancestor that contains > 180 chars of text (the recommendation
  // body lives somewhere in that subtree).
  var seen = new Set();
  var recs = [];

  otherAnchors.forEach(function (anchor) {
    var el = anchor;
    var container = null;
    for (var i = 0; i < 10 && el && el !== document.body; i++) {
      el = el.parentElement;
      if (!el) break;
      var fullText = (el.innerText || '').trim();
      if (fullText.length > 180) { container = el; break; }
    }
    if (!container || seen.has(container)) return;

    // Reject containers that hold multiple recommenders (we walked too far up).
    var distinctOthers = new Set();
    container.querySelectorAll('a[href*="/in/"]').forEach(function (a) {
      var p = a.pathname || '';
      var h = (p.split('/in/')[1] || '').split('/')[0];
      if (h && h !== myHandle) distinctOthers.add(h);
    });
    if (distinctOthers.size > 1) return;
    seen.add(container);

    // Step 3: extract fields.
    var nameSpan = anchor.querySelector('span[aria-hidden="true"]') || anchor;
    var name = (nameSpan.innerText || '').trim().split('\n')[0].trim();
    if (!name || name.length < 2) return;
    var profile_url = anchor.href.split('?')[0].replace(/\/$/, '') + '/';

    // Body: longest leaf-ish <span> in the container (or whole text minus name).
    var leafSpans = Array.from(container.querySelectorAll('span'));
    var longest = '';
    leafSpans.forEach(function (s) {
      // Treat as leaf if its children are only <br>
      if (s.children.length > 0) {
        var onlyBr = true;
        for (var j = 0; j < s.children.length; j++) {
          if (s.children[j].tagName !== 'BR') { onlyBr = false; break; }
        }
        if (!onlyBr) return;
      }
      var t = (s.innerText || '').trim();
      if (t.length > longest.length) longest = t;
    });
    if (longest.length < 60) {
      var fallback = (container.innerText || '').trim();
      fallback = fallback.split('\n').filter(function (ln) { return ln.trim() !== name.trim(); }).join('\n').trim();
      if (fallback.length > longest.length) longest = fallback;
    }
    longest = longest.replace(/\s*…see more\s*$/i, '').replace(/\s*see more\s*$/i, '').trim();
    if (longest.length < 60) return;

    // Headline (job title)
    var jobRe = /\bat\b|\bCEO\b|\bCMO\b|\bCOO\b|\bdirector\b|\bmanager\b|\bfounder\b|\bowner\b|\bvp\b|\bhead of\b|\bpresident\b|\bcopywriter\b|\bmarketer\b|\bconsultant\b/i;
    var headline = '';
    for (var k = 0; k < leafSpans.length; k++) {
      var t = (leafSpans[k].innerText || '').trim();
      if (t.length > 5 && t.length < 200 && t !== name && t !== longest && jobRe.test(t)) {
        headline = t; break;
      }
    }
    if (!headline) {
      for (var m = 0; m < leafSpans.length; m++) {
        var t = (leafSpans[m].innerText || '').trim();
        if (t.length > 10 && t.length < 200 && t !== name && t.length < longest.length / 2) {
          headline = t; break;
        }
      }
    }

    // Relationship + date — look for short context-y or date-y line
    var contextRe = /(worked|managed|reported|was|is)\s+(with|directly|on|to)/i;
    var dateRe = /([A-Z][a-z]+\s+\d{1,2},\s+\d{4}|[A-Z][a-z]+\s+\d{4})/;
    var relationship = '';
    var dateStr = '';
    for (var n = 0; n < leafSpans.length; n++) {
      var t = (leafSpans[n].innerText || '').trim();
      if (t.length > 10 && t.length < 300 && t !== name && t !== longest && t !== headline) {
        var dm = t.match(dateRe);
        var hasContext = contextRe.test(t);
        if (dm || hasContext) {
          if (dm) { dateStr = dm[1]; t = t.replace(dm[1], '').replace(/[·\s]+$/, '').trim(); }
          if (hasContext) relationship = t;
          break;
        }
      }
    }

    recs.push({ name: name, headline: headline, relationship: relationship, date: dateStr, text: longest, profile_url: profile_url });
  });

  if (recs.length === 0) {
    console.log('Diagnostic — anchors to other profiles:', otherAnchors.length);
    console.log('Sample anchors:', otherAnchors.slice(0, 3).map(function (a) {
      return { href: a.href, text: (a.innerText || '').slice(0, 80) };
    }));
    alert('Found ' + otherAnchors.length + ' profile links but no recommendation bodies. Open Cmd+Opt+J console for diagnostics.');
    return;
  }

  function yq(s) { return (s || '').replace(/"/g, '\\"'); }

  var yaml = recs.map(function (r) {
    var lines = ['- name: "' + yq(r.name) + '"'];
    if (r.headline)     lines.push('  headline: "'     + yq(r.headline)     + '"');
    if (r.relationship) lines.push('  relationship: "' + yq(r.relationship) + '"');
    if (r.date)         lines.push('  date: "'         + yq(r.date)         + '"');
    if (r.profile_url)  lines.push('  profile_url: "'  + yq(r.profile_url)  + '"');
    lines.push('  text: |');
    var paragraphs = r.text.split(/\n\s*\n+/);
    paragraphs.forEach(function (p, idx) {
      p.split('\n').forEach(function (ln) {
        if (ln.trim()) lines.push('    ' + ln.trim());
      });
      if (idx < paragraphs.length - 1) lines.push('');
    });
    return lines.join('\n');
  }).join('\n\n');

  console.log('=== LinkedIn Recommendations YAML ===\n\n' + yaml + '\n\n=== End ===');
  try {
    await navigator.clipboard.writeText(yaml);
    alert('Found ' + recs.length + ' recommendation(s). YAML copied to clipboard. (Also in console — Cmd+Opt+J)');
  } catch (e) {
    alert('Found ' + recs.length + ' recommendation(s). Clipboard blocked — open Cmd+Opt+J console to copy the YAML manually.');
  }
})();
```
