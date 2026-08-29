# Capability: Product UI Animation & Showcase

**Domain:** design-execution  
**Status:** ADOPT  
**Delegation level:** 4 / 5  
**Score:** 62 / 80  
**Last updated:** 2026-08-29

---

## Problem class

When Federico needs to animate real product UI — dashboards, data tables, mobile flows, form interactions — as part of a portfolio showcase, case study presentation, or stakeholder demo. This is NOT about abstract motion graphics or AI-generated imagery: it is about orchestrating DOM elements that represent real product states, telling the story of how a product works without a live instance or a screen recording.

The context: `beats.html` in `federico-os` — a showcase of 47 beats across 6 projects (EY, Skills, DollarCity, Blockchain, Chek, Customs), each being an animated reconstruction of a real product screen.

---

## Underlying concept

A product UI beat is NOT a screenshot with a fade-in.

It is a DOM reconstruction of the real product state — the same HTML structure, the same CSS classes, the same component hierarchy — orchestrated through time with animations that show:
- what was visible first
- what changed
- where the user's attention was
- what the outcome was

The key distinction: **DOM is the product. Animation is the narrator.**

This means the beat must reach visual parity with the real product BEFORE any animation is added (Phase A), and only then layer the narrative motion on top (Phase B). AI should never jump from screenshot to animation — it must understand the system first.

**The Ponytail moment:** "Animate the dashboard to show the metric being clicked and the drill-down appearing" → Claude reconstructs the HTML structure, applies spring transitions to the expanding panel, and times a formatted counter to increment while the table rows stagger in — without Federico touching a single timer or keyframe.

---

## When to use

- Building a new beat in `beats.html` (portfolio showcase)
- Creating a case study walkthrough that needs motion
- Animating a KPI dashboard, data table, or mobile flow for a presentation
- Extracting animation patterns from real product interactions to showcase in the portfolio

## When NOT to use

- Abstract motion graphics or generative visual art — different domain entirely
- Video post-production — if it needs to be a video export, use ScreenFlow/Loom on top of the running beat
- Marketing animation — that's closer to After Effects territory; this capability is specifically for product UI in code

---

## The animation vocabulary (non-negotiable)

Always name the animation type before writing the code. A beat should use AT MOST 3 types:

| Name | Trigger | Easing |
|------|---------|--------|
| `reveal` | element appears from hidden | `var(--spring)` if it grows, opacity fade if text |
| `cursor-move` | scripted cursor navigating the UI | linear segments, easeInOut at stops |
| `state-change` | button/tab/card switches state | 150ms `ease-out` |
| `emphasis` | glow, ring, shake — "look here" | 300ms spring → decay |
| `zoom` | camera-in on a specific element | ease-in-out, no abrupt stops |
| `scene-transition` | beat-to-beat crossfade | 300ms opacity |
| `counter` | number animates to final value | easeOutQuart, ~1400ms, formatted mid-flight |
| `stagger` | list rows/cards cascade in | 80ms delay offset per element |

**Spring rule (from the design system):**  
`var(--spring)` = `cubic-bezier(.34, 1.56, .64, 1)` — anything that GROWS must use this.  
`cubic-bezier(.22, 1, .36, 1)` = travel (slide, fade) — no overshoot.  
Never mix them up. This has caused regressions before.

---

## Evaluated tools (Cycle #1 — 2026-08-29)

See `sources/ui-animation-resources.md` for full evaluation. Summary:

### ADOPT — use these

**Anime.js** (72.5k ★)  
`anime.timeline()` is the right tool for beats with more than 8 sequential steps. Sequences, staggers, and offsets are far cleaner than `setTimeout` chains. CDN:
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/animejs/3.2.2/anime.min.js"></script>
```
Specific pattern for beats:
```js
anime.timeline({ easing: 'easeOutExpo' })
  .add({ targets: '.kpi-tile', opacity: [0,1], translateY: [12,0], delay: anime.stagger(80) })
  .add({ targets: '.cursor', translateX: 200, duration: 600 }, '+=300')
  .add({ targets: '.drill-panel', scaleY: [0,1], transformOrigin: 'top', easing: 'spring(1,80,10,0)' });
```

**Motion One** (already in CLAUDE.md CDN allowlist)  
`inView()` for scroll-triggered beat reveals. `scroll()` for scroll-driven drift (ties panel opacity/translateY to scroll position — "movie" feel without autoplay).
```js
import { inView, animate } from 'motion';
inView('.beat-stage', () => animate('.kpi-value', { opacity: [0,1] }, { duration: 0.4, easing: [.34,1.56,.64,1] }));
```

**CSS IntersectionObserver + stagger**  
For simple staggered reveals (no library needed):
```js
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.querySelectorAll('.row').forEach((el, i) => {
        el.style.animationDelay = `${i * 80}ms`;
        el.classList.add('reveal');
      });
    }
  });
});
```

**Formatted counter animation**  
For KPI tiles — number increments AND formats mid-flight (commas, decimals):
```js
function animateCounter(el, from, to, duration = 1400) {
  const start = performance.now();
  requestAnimationFrame(function tick(now) {
    const t = Math.min((now - start) / duration, 1);
    const ease = 1 - Math.pow(1 - t, 3); // easeOutCubic
    el.textContent = Math.round(from + (to - from) * ease).toLocaleString();
    if (t < 1) requestAnimationFrame(tick);
  });
}
```

**transition.css** (2k ★ — argyleink)  
46 drop-in CSS transitions via HTML attributes. Good for "scene change" wipes between beat states:
```html
<div class="beat-container" transition-style="in:wipe:right">
```
CDN: `https://unpkg.com/transition-style` — but check the CLAUDE.md allowlist first before adding any new CDN.

### REFERENCE — know it, don't install

**Tabler** (41.4k ★) — The best open-source source of real dashboard HTML patterns (charts, KPIs, tables, activity feeds). Not an animation library — use it as reference for what real dashboard DOM looks like, then apply animation to it. Useful when building new EY/Skills beats.

### OVERKILL for Federico's stack

| Tool | Why skip |
|------|---------|
| GSAP (full) | Free tier adds "GreenSock" branding. Only worth it for scroll-storytelling sections with ScrollTrigger. Use Anime.js for beat timelines. |
| Framer Motion | React only |
| Lottie | After Effects pipeline — Federico isn't in that workflow |
| Rive | Same — game/app-level, requires separate tool |

### OUTDATED / MISSING (from framework doc)

| Repo | Verdict | Why |
|------|---------|-----|
| extract-design-system | USEFUL for clients | Real TypeScript CLI, 192 ★. Extracts W3C tokens from live URLs. Not needed for Federico's own portfolio (DS already defined), but valuable for client onboarding. |
| stylelift | REFERENCE | 0 stars, 11 commits — unproven. Chrome extension → DESIGN.md output is the right idea, but wait for maturity. |
| mimic-ai | REFERENCE | MCP + Figma plugin that enforces DS compliance at write-time. Interesting, but Federico's workflow doesn't need a Figma DS enforcer right now. |
| screenshot-to-design-system | IGNORE | 4 commits, Python scripts, unreliable |
| html-figma / HTML-to-Design | IGNORE | Thin wrappers, 3 commits each, not production-ready |
| story-ui / storysync | IGNORE | Storybook/React dependencies — irrelevant for this stack |
| uselayout/app | IGNORE | Full SaaS with Docker + Supabase — massive setup for zero gain |

---

## The two-phase rule

**Phase A — RECONSTRUCT:** build the DOM first. CSS parity with the real product. No animation yet. This is where most time should go.

**Phase B — ORCHESTRATE:** add the 3-animation vocabulary. Never more than 3 types per beat. Time the sequence so it reads like a narrated walkthrough, not a demo reel.

**AI should never skip Phase A.** If Federico sends a screenshot, the first job is DOM reconstruction, not animation.

---

## Blockchain exception

Blockchain player uses Three.js (WebGL). For native beat reconstruction (Option B):
- **City 3D canvas:** use a static screenshot of the city state as background image. The Three.js city is atmosphere, not the story — the iOS overlay IS the story.
- **iOS overlay:** animate natively with CSS class toggling + spring transitions.
- This avoids 4× parallel WebGL contexts that would compete for resources.

---

## Federico's role

Define what the beat should show (the narrative intent). Identify the 3 key moments in the screen. Approve timing after seeing the first draft.

## AI's role

Reconstruct the DOM from the player code. Name the animation vocabulary for this specific beat. Implement the timeline using Anime.js or Motion One. Tune spring values and stagger delays.

## Delegation level

**4/5** — DOM reconstruction and animation implementation fully delegated. Federico approves the narrative timing and visual parity.

## Ponytail score

**8/10** — Writing `setTimeout` chains by hand is exactly the kind of low-leverage work AI absorbs completely.

---

## Related capabilities

- [Design Automation & Visual QA](design-automation.md) — Playwright for visual regression on beats
- [AI Coding Agent](ai-coding-agent.md) — the executor for DOM reconstruction
- [Figma MCP](figma-mcp.md) — source of real product component structure when DOM isn't available

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| 2026-08-29 | 47-beat postMessage timing race — beats not activating reliably | Diagnosed: 260ms fixed delay, no ACK. Two fix options documented. | [BEATS-LOG](../../federico-os/context/BEATS-LOG.md) |

## Notes

- The beats system in `federico-os` is the lab for this capability. Every pattern proved there is promotable to this file.
- `Anime.js` spring easing: `spring(mass, stiffness, damping, velocity)` — `spring(1,80,10,0)` is a tight, fast spring close to `var(--spring)`.
- Beat timing gut-check: if a beat takes longer than 8 seconds to auto-play, it needs cutting — not more animation.
- Real product UI from open source: Tabler is the best HTML reference for EY-style dashboards; no other open-source project matches it for DOM realism.
