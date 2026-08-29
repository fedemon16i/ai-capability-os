# Source: UX Storytelling & Portfolio Presentation

**Research date:** 2026-08-29  
**Research context:** Animated product UI showcase — how to frame beats as narrative, how to structure case studies for senior UX roles, how to present NDA'd work.  
**Stack:** Vanilla HTML + CSS + JS. No frameworks. No build step.

---

## The recruiter scan — what actually happens

Research from NN/g, UX Design Institute, and UX Fol.io (2025–26):

**First 5 seconds answer three questions:**
1. What do you do?
2. What seniority are you?
3. What domain are you in?

**Critical failure mode:** no clear positioning on the homepage. If someone has to open a case study to understand your role, you already lost them.

**2025–26 shift:** 78% of recruiters use AI screening tools that parse heading structure and metadata — not just aesthetics. Semantic HTML and strong `<h1>` copy matter more than they used to.

**What gets 30 seconds of real attention:** the opening frame of each case study (not the index). Recruiters who want to go deeper look at:
1. The problem statement (do they understand the business + user problem?)
2. The research evidence (is there real data, or just personas?)
3. The outcome (is there a real measurable result, or just "improved usability"?)
4. The role attribution (did they actually do this, or lead a team?)

---

## The three storytelling frameworks

### 1. PFFR — Problem / Friction / Fix / Result

The most common structure in strong UX portfolios. Maps directly to beat sequences:

```
P — Problem
   What was broken from the user's perspective? (one sentence, no jargon)
   What was the business consequence?

F — Friction
   Where specifically did users fail?
   What did the data show? (drop-off, rage clicks, session length, NPS)
   What did research surface?

F — Fix
   What decision was made and why?
   What was the design intervention?
   What was NOT chosen and why?

R — Result
   What measurably changed?
   Real number or honest percentage range — never invented precision
   If NDA: "transaction success rate improved by ~30%" (range OK, exact wrong)
```

**When to use:** Most projects. Clean, fast to scan, maps well to animated beat sequences where each beat = one stage of the arc.

---

### 2. SCQA (Minto Pyramid) — Situation / Complication / Question / Answer

Increasingly cited in 2025–26 UX writing guides. Better for ambiguous problem spaces where the brief itself was wrong.

```
S — Situation
   What was the established context everyone agreed on?
   (No drama yet — just ground truth)

C — Complication
   What changed, was discovered, or contradicted the assumption?
   This is the pivot — where the interesting work began.

Q — Question
   What question did that complication force?
   (Explicit — "This meant we had to ask: are we solving the right problem?")

A — Answer
   The design response to that question.
   Not the solution — the answer. Solutions get described in the next section.
```

**When to use:** Complex projects with a pivot, where the brief changed during research. Good for senior storytelling — shows that you shape the brief, not just execute it.

---

### 3. Design Spine — Worst Moment / Intervention / Systemic Change

The senior-designer pattern. Closes on organizational or systemic impact, not just user outcome. Used in principal/director-level portfolios.

```
Worst Moment
   The most painful specific instance for a real user.
   Concrete, not generalized. ("A store manager in Medellín had to...")

Intervention
   The design decision that addressed that worst moment.
   Specific. One intervention, not a list.

Systemic Change
   How that intervention changed the system, the team, or the process —
   beyond the individual screen.
   ("This led to establishing a weekly instrumentation review across 3 teams.")
```

**When to use:** Strategic or organizational work (product operations, design systems, research that changed roadmap direction). Less suited for feature-level UI work.

---

## How to pace an animated showcase (beats)

Rules derived from how Apple WWDC feature segments, Figma release demos, and Stripe landing pages structure their UI showcases:

| Element | Duration | Rule |
|---------|----------|------|
| Problem frame | 3–5s | No animation — static, text-first |
| First beat | 4–8s | One thing happens, one thing settles |
| Transition between beats | 0.3–0.5s | Cross-fade or wipe, never slide unless spatial (step 2 of a flow) |
| Annotation / callout | 2–4s visible | Appears, readable, disappears — never fades in slower than 200ms |
| Max beat duration | 12s | If longer, split into two beats |
| Total per case study section | < 90s | If the viewer has to wait more than 90s to see the outcome, they won't |

**The anti-pattern to avoid:** "Demo reel" — every beat has a different transition, every element bounces in independently, there's ambient looping. This reads as "I'm showing off motion, not product thinking."

**The pattern that works:** Each beat has one thing that moves, everything else is static. The motion answers "what happened here?" — not "can I animate this?"

---

## How to present AI-augmented work (2025–26 expectation)

Consensus from UX hiring content: by 2026, showing AI in the workflow is expected, but attribution matters.

**Do:**
- Name specifically where AI was used and for what ("Used Claude Code to generate the beat animation scaffold, then tuned timing and pacing manually")
- Show before/after of AI output vs final decision ("AI suggested X — here's what I changed and why")
- Frame it as tool proficiency, not labor reduction

**Don't:**
- Use "AI-assisted" as a blanket disclaimer — it reads as covering a process you can't explain
- Claim AI tools as design decisions (the decision was yours; the tool was a means)
- Hide it — the question "did AI do this?" is now routine in interviews

---

## NDA'd work — the established playbook

From IxDF, UX Planet, UX Survival Guide:

1. **Get permission first** — even a verbal "you can show the process" matters
2. **Swap client identity** — "a Latin American retail network" not "DollarCity"
3. **Change exact numbers to ranges** — "~30% improvement" not "29.7%"
4. **Password-protect** — "available on request" for the most sensitive; use a simple password shared during interview process
5. **Focus on process over specifics** — research methodology, decision rationale, and outcome type survive NDA; exact screen copy often doesn't
6. **Abstract the UI** — redesign the surface without changing the interaction pattern (the interaction is the work; the brand is not)

---

## The annotated demo pattern

How Figma, Stripe, and Linear present UI features in release posts and case studies:

```
REAL UI → freeze → annotation appears (line + label) → hold 2s → annotation disappears → interaction continues
```

Implementation: absolutely positioned annotation layer over the beat stage, opacity animated via JS in the beat timeline. The annotation is NOT part of the product UI — it's a presentation layer.

CSS:
```css
.annotation {
  position: absolute;
  pointer-events: none;
  opacity: 0;
  transition: opacity 200ms ease-out;
}
.annotation.visible { opacity: 1; }
```

JS in beat timeline:
```js
setTimeout(() => {
  document.querySelector('.annotation-kpi').classList.add('visible');
  setTimeout(() => document.querySelector('.annotation-kpi').classList.remove('visible'), 2000);
}, 3500); // appears after the KPI value settles
```

---

## Resources to bookmark

| Resource | What it covers |
|----------|---------------|
| [NN/g: UX Portfolio Guidelines](https://www.nngroup.com/articles/ux-portfolio/) | Research-backed recruiter expectations |
| [UX Collective: Case study structure](https://uxdesign.cc/ux-case-study-template) | Template with real examples |
| [Stripe's product pages](https://stripe.com/payments) | Best example of UI storytelling in a landing page |
| [Linear changelog](https://linear.app/changelog) | Feature release narrative — precise, no fluff |
| [Apple WWDC 2024 session videos](https://developer.apple.com/wwdc24/) | Pacing reference for UI demo sequences |
| [Figma Config talks](https://www.figma.com/video/config/) | Design presentation patterns from design community |
| [web.dev: View Transitions](https://developer.chrome.com/docs/web-platform/view-transitions/) | Native shared-element morphing API |
