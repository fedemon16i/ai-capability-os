# Capability: Design Automation & Visual QA

**Domain:** design-execution  
**Status:** ADOPT  
**Delegation level:** 4 / 5  
**Score:** 60 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Federico needs to verify that a design implementation is correct — visually, accessibly, and responsively — across multiple viewports, without manually opening every browser size and running through a checklist. Also: when design tokens defined in Figma need to stay in sync with the CSS codebase.

## Underlying concept

Design QA has three layers: (1) does it match the design intent (visual regression), (2) is it accessible (a11y), and (3) does it work at every viewport (responsive). Each layer can be automated with a different tool — but for Federico's stack (vanilla HTML/CSS, no React, no build step), most tools in this space don't apply because they require Storybook, React, or a CI pipeline.

The minimum viable stack for Federico's context covers all three layers with zero framework dependency and under 2 hours total setup, at zero cost.

**The Ponytail moment:** "Audit the portfolio for visual regressions after this refactor" → Playwright runs screenshots at 6 viewports, diffs against baseline, and flags any pixel-level changes — without Federico opening a single browser tab.

## The minimum viable stack

| Layer | Tool | Setup | Cost |
|-------|------|-------|------|
| Design tokens | Figma Variables | 0 min (already in Figma) | Free |
| Accessibility (design) | Figma native AI checker | 0 min (built-in) | Free |
| Accessibility (code) | axe-core/playwright | 45 min | Free |
| Visual regression | Playwright `toHaveScreenshot()` | 60 min | Free |
| Responsive audit | Playwright device emulation | 0 min (same setup as above) | Free |
| Responsive (interactive) | Responsively App | 5 min | Free |

**Total: ~2 hours setup. Zero cost.**

## Design tokens approach

**For a solo designer without a developer consuming the output:** Figma Variables is the right level. Define color, spacing, and typography tokens directly in Figma — they map naturally to CSS custom properties and are readable by the Figma MCP. No external tool needed.

**If a handoff pipeline is ever needed:** Figma Variables → DTCG JSON → Style Dictionary v4 is the 2026 standard for teams. Style Dictionary is an engineering tool — Federico needs to know it exists and what it does, but shouldn't maintain it himself.

**Don't use:** Token Studio (setup overhead doesn't pay off without a developer consuming the output).

## Visual regression (Playwright)

Playwright's `toHaveScreenshot()` works against any live URL — no framework, no Storybook, no cloud account. Setup:

```bash
npm init playwright@latest
# adds playwright.config.ts and a tests/ directory
```

Basic visual test:
```typescript
test('homepage visual', async ({ page }) => {
  await page.goto('http://localhost:3000');
  await expect(page).toHaveScreenshot('homepage.png');
});
```

First run creates the baseline screenshots. Subsequent runs diff against them and fail on pixel-level changes — catching regressions automatically.

**Responsive audit:** add device projects to `playwright.config.ts` to run at 320/375/768/1024/1440/1920 in one command.

**Alternatives ruled out for this stack:**
- Chromatic: requires Storybook. Irrelevant.
- Percy: best if cross-browser proof becomes a client requirement (AI Visual Review reduces false positives). LEARN for that specific context.

## Accessibility (two-layer approach)

**Layer 1 — Design side (Figma native AI checker):**
- Built into Figma, zero setup
- Checks: contrast ratios, color blindness simulation, WCAG compliance in the design file
- Catches failures before anything goes to code — the cheapest point to fix them

**Layer 2 — Implementation side (axe-core + Playwright):**
```typescript
import AxeBuilder from '@axe-core/playwright';

test('homepage accessibility', async ({ page }) => {
  await page.goto('http://localhost:3000');
  const results = await new AxeBuilder({ page }).analyze();
  expect(results.violations).toEqual([]);
});
```
- Scans rendered HTML for WCAG violations that Figma can't see (missing alt text, broken ARIA, keyboard traps)
- Catches implementation drift from the design spec

Together, these two cover both sides of the design-to-code gap.

## Responsive audit (Playwright + Responsively App)

**Playwright device emulation:** configure once, run automatically on every audit:
```typescript
projects: [
  { name: '320', use: { viewport: { width: 320, height: 568 } } },
  { name: '375', use: { viewport: { width: 375, height: 667 } } },
  { name: '768', use: { viewport: { width: 768, height: 1024 } } },
  { name: '1024', use: { viewport: { width: 1024, height: 768 } } },
  { name: '1440', use: { viewport: { width: 1440, height: 900 } } },
  { name: '1920', use: { viewport: { width: 1920, height: 1080 } } },
]
```

**Responsively App:** free desktop app that renders any URL in all viewports simultaneously. Best for interactive visual exploration during development — faster than browser DevTools for the 6-viewport sweep Federico already does manually.

## When to use

- After any CSS change that touches shared.css or layout components
- Before releasing a new project page to main
- After a full design system refactor
- When verifying that a light/dark mode fix actually works at all viewports
- Any time Federico does the manual "open 6 browser sizes" check — automate it instead

## When NOT to use

- For individual text content changes or copy edits (no visual delta to catch)
- As a substitute for product judgment about visual design quality — Playwright catches regressions, not design taste problems
- For initial design exploration (use Figma + v0 for that)

## Federico's role

Write the initial test suite (one time, with AI assistance). Run the audit command before merging changes. Review flagged diffs and decide: intentional change (update baseline) or regression (fix it).

## AI's role

Generate the Playwright test files from a description of what to test. Debug failing tests. Interpret axe-core accessibility violations and suggest fixes. Update baselines when designs intentionally change.

## Delegation level

**4/5** — Test generation and interpretation fully delegated. Federico runs the command and reviews flagged diffs.

## Ponytail score

**7/10** — Playwright encapsulates cross-viewport, cross-concern testing behind a single command. The setup investment (2 hours) pays off on every subsequent audit.

## Related capabilities

- [AI Coding Agent](ai-coding-agent.md) — generates the test files and fixes failing tests
- [Figma MCP](figma-mcp.md) — design token source that should stay in sync with CSS
- [Agent Orchestration](agent-orchestration.md) — running full audits as an orchestrated sweep

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| | | | |

## Notes

- The portfolio already has a 6-viewport audit in the CLAUDE.md pre-commit checklist. Playwright automates exactly this checklist. The natural first test: take Federico's manual breakpoint check and translate it into a Playwright spec.
- Playwright is also the foundation for the Playwright MCP (LEARN) — the same install enables both visual regression and browser automation via Claude.
- Don't install Chromium separately if using Playwright on this Claude Code remote environment — it's pre-installed at `/opt/pw-browsers/chromium`.
- `axe-core/playwright` violations return a structured list of WCAG rule violations with impact (critical/serious/moderate/minor) — sort by critical first, ignore minor for now.
