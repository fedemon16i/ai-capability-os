# Capability: UI Integrity Guardian

**Domain:** design-execution  
**Status:** ADOPT  
**Delegation level:** 5 / 5  
**Score:** 62 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When AI-generated or rapidly-written code introduces subtle UI quality regressions — inconsistent padding, broken button wrapping, misaligned elements, design token violations, spacing scale drift — that aren't caught by visual regression tests (which only compare against a baseline) or accessibility checks (which focus on ARIA, not design quality).

The specific risk in AI-assisted coding ("vibe coding"): the agent generates structurally correct code that technically works but doesn't respect the design system's rules — wrong spacing values, hardcoded colors instead of CSS variables, font weights outside the allowed range.

## Underlying concept

UI integrity is the set of properties that make a UI feel coherent — not correct in the functional sense, but correct in the design sense:
- Every spacing value comes from the scale (`--space-*` variables)
- No hardcoded colors (unless intentional brand exceptions)
- No font weights outside the allowed range (400, 600, 700, 800)
- No text overflows or unexpected line breaks in buttons/labels
- All grid columns use `auto-fit`, never fixed counts
- All cards and boxes use consistent internal structure (flex column)
- No horizontal scroll caused by layout overflow

The UI Integrity Guardian is an automated check that runs after any UI code is generated or modified, scanning for violations against these rules.

**The Ponytail moment:** run one command after a code generation session → get a report of UI integrity violations with file locations and fix suggestions, before the browser is even opened.

## What it checks

### Spacing & layout
- [ ] All `padding`, `margin`, `gap` values use `var(--space-*)` tokens (not hardcoded `px` or `rem`)
- [ ] Grid layouts use `repeat(auto-fit, ...)` not fixed column counts
- [ ] Card internal structure is `display: flex; flex-direction: column`
- [ ] Tables use `padding: 14px 20px` on `th`/`td`
- [ ] Responsive: below 768px → 1 column; below 480px → reduced padding

### Typography
- [ ] No `font-weight: 300` anywhere
- [ ] No font-family overrides (Syne + DM Sans only)
- [ ] Font weights within allowed set (400, 600, 700, 800)

### Color
- [ ] No hardcoded hex colors in general CSS (brand colors in project pages are acceptable exceptions)
- [ ] All colors via CSS vars (`--text`, `--bg-base`, `--accent`, etc.)
- [ ] No dark-green-on-dark combinations
- [ ] Card rest state: solid color (no gradient). Gradient only on hover.

### Animation
- [ ] Growing elements use `var(--spring)` = `cubic-bezier(.34,1.56,.64,1)`
- [ ] No `cubic-bezier(.22,1,.36,1)` on elements that grow (no overshoot — wrong curve)
- [ ] Hover animations with size change have `pointerleave` debounce (~70ms)
- [ ] `prefers-reduced-motion` is respected

### Buttons & interactive elements
- [ ] No button text overflows or unexpected line breaks
- [ ] All buttons use `.btn` class variants, not inline styles
- [ ] Clickable areas have sufficient size (min 44×44px touch target)

### Structural integrity
- [ ] No `overflow-x` on body
- [ ] First child of `<body>` is `.skip-link` on every page
- [ ] All `<img>` have descriptive `alt` attributes
- [ ] No new class name conflicts (grep before creating)

## Implementation

### As a Claude Code pre-commit check

The guardian runs as a structured analysis prompt:

```
You are a UI Integrity Guardian for a design system with these rules:

[Paste the relevant sections of CLAUDE.md: Design System, CSS Conventions, Animation rules, Do Not section]

Review the following code changes:
[Paste the diff or the modified file]

Check for violations in these categories:
1. Spacing — hardcoded values instead of CSS variables
2. Typography — forbidden font weights, wrong font families
3. Color — hardcoded hex, wrong use of dark colors
4. Animation — wrong easing curves, missing debounce, missing prefers-reduced-motion
5. Layout — fixed grid columns, non-flex card structure
6. Buttons — overflow, wrong class usage
7. Structural — overflow-x, missing skip link, missing alt text, class name conflicts

For each violation:
- File and line number (if provided)
- What the violation is
- Why it matters
- The fix (specific code change)

Rate severity: CRITICAL (breaks something) / WARNING (design system violation) / INFO (style preference).

Only report real violations. Do not flag correct code.
```

### As a Playwright test

For runtime violations (things that only manifest in the rendered DOM):

```typescript
import AxeBuilder from '@axe-core/playwright';

test('UI integrity check', async ({ page }) => {
  await page.goto('http://localhost:3000');
  
  // Check no overflow-x on body
  const bodyOverflow = await page.evaluate(() => 
    getComputedStyle(document.body).overflowX
  );
  expect(bodyOverflow).not.toBe('scroll');
  
  // Check skip link exists as first child
  const firstChild = await page.$('body > :first-child');
  const firstChildClass = await firstChild?.getAttribute('class');
  expect(firstChildClass).toContain('skip-link');
  
  // Check no images missing alt
  const imgsWithoutAlt = await page.$$eval('img:not([alt])', imgs => imgs.length);
  expect(imgsWithoutAlt).toBe(0);
  
  // Check no inline color styles (basic heuristic)
  const inlineColors = await page.$$eval('[style*="color:"]', els => els.length);
  expect(inlineColors).toBe(0);
});
```

### As a CSS lint scan

For static file checks without a browser:

```bash
# Check for hardcoded font weights below 400
grep -rn "font-weight: [123]" --include="*.css" --include="*.html"

# Check for hardcoded colors (non-variable)
grep -rn "color: #" --include="*.css" --include="*.html"

# Check for wrong spring curve
grep -rn "cubic-bezier(.22,1,.36,1)" --include="*.css" --include="*.html"

# Check for fixed grid columns
grep -rn "repeat([0-9]" --include="*.css" --include="*.html"
```

## Severity model

| Severity | Definition | Action |
|----------|-----------|--------|
| **CRITICAL** | Breaks functionality or accessibility (overflow on body, missing skip link, broken ARIA) | Block — fix before commit |
| **WARNING** | Violates the design system explicitly (hardcoded color, wrong font weight, wrong easing) | Fix before commit |
| **INFO** | Stylistic drift that doesn't break rules but diverges from convention | Fix if time allows |

## When to use

- After every AI code generation session that touches CSS or layout
- Before committing any UI changes
- After a design system refactor (verify no regressions)
- When a new page or component is added
- When reviewing a PR from an AI agent

## When NOT to use

- For logic/backend code changes (no UI impact)
- For content-only changes (copy edits, text updates)
- As a substitute for actual visual QA in the browser — the guardian catches code violations, not design taste problems

## Federico's role

Trigger the guardian check (one command or prompt). Review the violation report. Decide severity overrides where the "violation" is intentional (e.g., a hardcoded brand accent color). Commit only after CRITICAL and WARNING violations are resolved.

## AI's role

Run the static analysis. Identify violations by category and severity. Provide exact fix code for each violation. Flag ambiguous cases and ask for a decision.

## Delegation level

**5/5** — Fully automated. Federico triggers it and reviews the report. No manual CSS scanning required.

## Ponytail score

**8/10** — Encapsulates the entire design system rulebook into an automated check. The complexity of knowing all the rules, applying them consistently, and catching edge cases disappears into a single command.

## Related capabilities

- [Design Automation & Visual QA](design-automation.md) — complementary: visual regression catches pixel-level changes; UI Integrity Guardian catches code-level violations
- [AI Coding Agent](ai-coding-agent.md) — the source of generated code that needs to be checked
- [User Story → Product Spec](user-story-to-spec.md) — the spec defines what "correct" UI looks like; guardian verifies implementation matches it

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| | | | |

## Notes

- **Integration point with CLAUDE.md:** the guardian's rulebook is the CLAUDE.md design system section + animation rules + Do Not section. When CLAUDE.md is updated, the guardian's rules update automatically — no separate maintenance.
- **5 recurring bugs in CLAUDE.md:** the guardian specifically checks for the 5 documented recurring bugs (class name collision, code inside `if(!reduced && matchMedia...)` block, dead CSS collision, `position:fixed` + `transform` offset, shared media query side effects). These are the highest-priority checks.
- **False positive handling:** some "violations" are intentional (brand accent colors hardcoded in project pages, per CLAUDE.md). The guardian should be prompted with this exception context to avoid false positives.
- **Automation path:** long-term, this can run as a GitHub Action pre-merge check — any PR that introduces a UI violation fails CI before it reaches Federico for review.
