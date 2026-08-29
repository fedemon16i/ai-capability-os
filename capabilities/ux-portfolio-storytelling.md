# Capability: UX Portfolio Storytelling

**Domain:** design-execution  
**Status:** ADOPT  
**Delegation level:** 3 / 5  
**Score:** 58 / 80  
**Last updated:** 2026-08-29

---

## Problem class

When Federico needs to structure a case study, frame an animated showcase as a narrative, decide what to show vs skip, or write the copy that accompanies a portfolio project — without it reading as a feature list, a process dump, or AI-generated marketing copy.

The context: `beats.html` in `federico-os` — 47 beats across 6 projects. Each beat needs a narrative intent before any animation is written. The beat is not the story — the arc across beats IS the story.

---

## Underlying concept

Product UI animation without narrative structure is a demo reel. The viewer sees motion but doesn't understand what changed, why it mattered, or what the designer's role was.

Storytelling gives animation its purpose: each beat is one moment in an arc. When you know the arc, you know which moments to show, how long each should run, when to use a callout vs let the UI speak, and how to close.

**The Ponytail moment:** "Write the case study narrative for the EY Fabric project" → Claude produces a PFFR structure with real beat references, clean copy in Federico's voice (no "leveraged synergies"), and a pacing guide for the beat sequence — without Federico staring at a blank page.

---

## The three frameworks (research-backed)

### PFFR — Problem / Friction / Fix / Result
Best for: most projects. Maps cleanly to beats.
```
P → what was broken (user + business)
F → where specifically (data evidence: drop-off, rage clicks, NPS)
F → what decision was made and why (including what was NOT chosen)
R → what measurably changed (real range, not invented precision)
```

### SCQA (Minto Pyramid) — Situation / Complication / Question / Answer
Best for: projects where the brief changed during research. Shows that Federico shapes the brief, not just executes it.
```
S → established context (no drama yet)
C → what was discovered that contradicted it
Q → the question that forced
A → the design response
```

### Design Spine — Worst Moment / Intervention / Systemic Change
Best for: strategic or organizational work (design systems, research that changed roadmap direction). Senior-designer register.
```
Worst Moment → one specific painful user instance (concrete, not generalized)
Intervention → one design decision that addressed it
Systemic Change → how it changed the system or process beyond the screen
```

---

## Beat pacing rules

| Element | Duration |
|---------|----------|
| Problem frame (static, text) | 3–5s |
| One beat | 4–8s max |
| Annotation callout | 2–4s visible |
| Beat-to-beat transition | 0.3–0.5s |
| Max total per showcase section | <90s |

**One rule above all:** each beat has ONE thing that moves. Motion answers "what happened?" — not "can I animate this?"

---

## The annotated demo pattern

Presentation layer on top of real UI — not part of the product, not part of the animation:

```css
.annotation { position: absolute; pointer-events: none; opacity: 0; transition: opacity 200ms ease-out; }
.annotation.visible { opacity: 1; }
```

Appears after the UI element it references has settled. Visible for 2s. Disappears before the next event. This is how Figma and Stripe do it on release pages.

---

## AI-augmented work (2025–26 expectation)

By 2026: showing AI in the workflow is expected. Attribution matters more than the tool.

**Show:** where AI was used, what for, and what Federico changed and why.  
**Don't:** use "AI-assisted" as a blanket disclaimer. Claim AI decisions as design decisions.

---

## NDA'd work

1. Get permission (even verbal)
2. Swap client identity → generic descriptor
3. Change exact numbers → honest ranges
4. Password-protect what's sensitive
5. Focus on process and decision rationale, not screen copy
6. Abstract the UI surface without changing the interaction pattern

The interaction pattern is the work. The brand is not.

---

## What recruiter scans actually see (research-backed)

**First 5 seconds:** what you do, seniority, domain. If they can't tell, you've already lost them.  
**30 seconds of deeper attention:** problem statement, research evidence, measurable outcome, role attribution.  
**2025–26 shift:** AI screening tools parse heading structure. Semantic HTML and clear `<h1>` copy matter.

---

## When to use

- Writing case study copy for a project page
- Deciding which beats to include and in what order for a showcase
- Adding annotations to a beat sequence
- Structuring a verbal presentation around the portfolio

## When NOT to use

- Writing product copy for a client's product (different purpose)
- Writing resume bullets (different format, different audience)

---

## Federico's role

Choose the framework that fits the project. Provide: the problem as Federico lived it, the data evidence, the decision and the rejected alternatives, the outcome. Approve the voice and the framing.

## AI's role

Apply the framework structure. Write the first draft in Federico's voice (no buzzwords, no "leveraged," no "holistic approach," no invented precision). Map the narrative to the beat sequence. Draft annotation copy.

## Delegation level

**3/5** — Structure and first draft fully delegated. Federico owns the final voice and all factual claims. Nothing ships without Federico reading every sentence.

## Ponytail score

**6/10** — The blank-page problem is real. AI eliminates the blank page; Federico edits from a real draft.

---

## Related capabilities

- [Product UI Animation & Showcase](product-ui-animation.md) — the motion layer that serves this narrative
- [AI Coding Agent](ai-coding-agent.md) — builds the beats that the narrative describes
- [Design Automation & Visual QA](design-automation.md) — validates the final presentation

## Related sources

- [UX Storytelling Resources](../sources/ux-storytelling-resources.md)
- [UI Animation Resources](../sources/ui-animation-resources.md)

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| 2026-08-29 | Framework research — best case study structures | PFFR, SCQA, Design Spine identified | [source](../sources/ux-storytelling-resources.md) |

## Notes

- Federico's voice markers: impersonal/descriptive tone (no "I/yo" in copy), real numbers or honest ranges, tool names are instruments not identity, "measured outcomes" not the name of a specific tool.
- Copy red flags to catch before it ships: "leveraged," "holistic," "synergy," "user-centric," exact invented metrics, any claim that can't be sourced.
