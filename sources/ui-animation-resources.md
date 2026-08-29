# Source: UI Animation Resources for Product Showcase

**Research date:** 2026-08-29  
**Research context:** Building `beats.html` — animated showcase of 47 product UI beats across 6 projects. Stack: vanilla HTML + CSS + JS, no frameworks, no build step.  
**Classification system:** ADOPT / LEARN / STUDY / REFERENCE / IGNORE

---

## Framework doc repos — evaluated

Source document: `product_ui_reconstruction_design_system_framework.md` (uploaded by Federico 2026-08-29).

### extract-design-system
- **URL:** https://github.com/arvindrk/extract-design-system
- **Stars:** 192 | **Commits:** 112 | **Last active:** recent
- **What it is:** TypeScript CLI + npm package. Crawls a live URL, extracts W3C-format design tokens (colors, typography, spacing, radius, shadows), outputs `tokens.json` + `tokens.css`.
- **Verdict: REFERENCE** — Real, working tool. Not needed for Federico's own portfolio (design system already defined). Valuable for client onboarding scenarios: `npx extract-design-system --url https://client.com` → instant token baseline.

### stylelift
- **URL:** https://github.com/sreenathmmenon/stylelift
- **Stars:** 0 | **Commits:** 11
- **What it is:** Chrome extension that scans a website and generates `DESIGN.md` + `tokens.json` + `theme.css`. The idea exactly matches Federico's workflow (give Claude the DNA of the product).
- **Verdict: REFERENCE** — Conceptually the closest fit to what Federico needs for client onboarding. Unproven (0 stars, sparse commits). Monitor for maturity. Do not install yet.

### uselayout/app
- **URL:** https://github.com/uselayout/app
- **Stars:** 13 | **Commits:** 1,230
- **What it is:** Full Next.js + Supabase + Docker SaaS. Extracts design context from Figma and live sites and turns it into AI-ready structured context.
- **Verdict: IGNORE** — Real product, heavy infra. Not worth the Docker + Supabase setup for Federico's current workflow. The concept is right; the tool is overkill.

### screenshot-to-design-system
- **URL:** https://github.com/WCF900905/screenshot-to-design-system
- **Stars:** 3 | **Commits:** 4
- **What it is:** Experimental Python scripts. Takes UI screenshots, attempts to extract design tokens.
- **Verdict: IGNORE** — 4 commits, experimental. Not reliable.

### html-figma
- **URL:** https://github.com/lgs/html-figma
- **Stars:** 11 | **Commits:** 103
- **What it is:** Thin wrapper over `@builder.io/html-to-figma`. Converts live HTML to Figma layers.
- **Verdict: IGNORE** — Use `@builder.io/html-to-figma` directly if this workflow ever becomes relevant. The wrapper adds nothing.

### HTML-to-Design
- **URL:** https://github.com/kimberlykuya/HTML-to-Design
- **Stars:** 3 | **Commits:** 3
- **What it is:** 3 commits. HTML → Figma conversion prototype.
- **Verdict: IGNORE** — Not functional end-to-end.

### mimic-ai
- **URL:** https://github.com/miapre/mimic-ai
- **Stars:** 13 | **Commits:** 149
- **What it is:** MCP server + Figma plugin. Enforces existing design system during AI-to-Figma operations — blocks raw hex values, enforces token usage.
- **Verdict: REFERENCE** — Published on npm, real code. The design-system enforcement concept is exactly right. Federico's stack doesn't need a Figma DS enforcer today (CLAUDE.md + DESIGN.md already fill this role). Revisit when Figma workflow becomes the primary source of truth.

### story-ui
- **URL:** https://github.com/southleft/story-ui
- **Stars:** 198 | **Commits:** 358
- **What it is:** AI-powered Storybook story generator. Uses your real components to generate Storybook stories.
- **Verdict: IGNORE** — Real, well-built tool. Requires Storybook + React. Irrelevant for Federico's stack.

### storysync
- **URL:** https://github.com/brendanciccone/storysync
- **Stars:** 66 | **Commits:** 50
- **What it is:** Syncs design system from code to Figma, diffs Figma vs code using Storybook MCP + Figma MCP.
- **Verdict: IGNORE** — Requires Tailwind + Storybook. Not applicable.

---

## Animation libraries — evaluated for product UI beats

### Anime.js
- **URL:** https://github.com/juliangarnier/anime
- **Stars:** 72,500 | **Active:** yes
- **CDN:** `https://cdnjs.cloudflare.com/ajax/libs/animejs/3.2.2/anime.min.js`
- **Why relevant:** `anime.timeline()` solves the `setTimeout` chain problem in beats. Staggers, offsets, spring easing all built-in. Works with vanilla JS, no framework needed.
- **Verdict: ADOPT** — Primary tool for beats with > 6 sequential animation steps.

### Motion One
- **URL:** https://motion.dev
- **Stars:** active, maintained
- **CDN:** Already in CLAUDE.md — `https://cdn.jsdelivr.net/npm/motion@10.16.4/dist/motion.js`
- **Why relevant:** `inView()` + `scroll()` for scroll-driven beats. Spring easing maps directly to `var(--spring)`.
- **Verdict: ADOPT** — Already approved CDN. Use for scroll-triggered reveals and scroll-driven sections.

### transition.css
- **URL:** https://github.com/argyleink/transition.css
- **Stars:** 2,000
- **What it is:** 46 CSS transitions via HTML attribute. Drop-in scene change wipes.
- **Verdict: REFERENCE** — Good for scene-transition between beats. Evaluate if the CDN is in the allowlist before using.

### Tabler
- **URL:** https://github.com/tabler/tabler
- **Stars:** 41,400
- **What it is:** Open-source admin UI template. Vanilla JS. Real dashboard HTML — KPI tiles, data tables, activity feeds, charts.
- **Why relevant:** Best available source of real dashboard DOM to use as reference when building EY/Skills beats. Study the HTML structure; apply Federico's animation patterns to it.
- **Verdict: REFERENCE** — Not a library to install. A DOM reference to study.

---

## Techniques extracted (ready to implement)

### 1. Staggered row reveal
```js
const rows = stage.querySelectorAll('.data-row');
rows.forEach((el, i) => {
  el.style.opacity = '0';
  el.style.transform = 'translateY(8px)';
  setTimeout(() => {
    el.style.transition = 'opacity 300ms ease-out, transform 300ms ease-out';
    el.style.opacity = '1';
    el.style.transform = 'none';
  }, i * 80);
});
```

### 2. Formatted counter
```js
function animateCounter(el, from, to, duration = 1400) {
  const start = performance.now();
  requestAnimationFrame(function tick(now) {
    const t = Math.min((now - start) / duration, 1);
    const ease = 1 - Math.pow(1 - t, 3);
    el.textContent = Math.round(from + (to - from) * ease).toLocaleString();
    if (t < 1) requestAnimationFrame(tick);
  });
}
```

### 3. Anime.js timeline for complex beats
```js
anime.timeline({ easing: 'easeOutExpo', duration: 400 })
  .add({ targets: '.kpi-tiles .tile', opacity: [0,1], translateY: [10,0], delay: anime.stagger(80) })
  .add({ targets: '.cursor-dot', translateX: 180, duration: 500, easing: 'easeInOutSine' }, '+=200')
  .add({ targets: '.drill-panel', scaleY: [0,1], transformOrigin: 'top center', easing: 'spring(1,80,10,0)' });
```

### 4. Motion One scroll-driven beat
```js
import { scroll, animate } from 'motion';
scroll(
  animate('.beat-info', { opacity: [0, 1], y: [20, 0] }),
  { target: document.querySelector('.beat-row'), offset: ['start end', 'start 60%'] }
);
```

### 5. Feature isolation timing
One element enters and settles (spring overshoot → rest) BEFORE the next starts.
Rule: next element begins 200ms AFTER the current one reaches its resting state — not 200ms after it starts.

```js
// Wrong: all start at 0ms, 100ms, 200ms (overlap during overshoot)
// Correct:
anime.timeline()
  .add({ targets: '.el1', scaleX: [0,1], duration: 400, easing: 'spring(1,80,10,0)' })
  .add({ targets: '.el2', opacity: [0,1], duration: 300 }, '+=200'); // starts 200ms AFTER el1 settles
```
