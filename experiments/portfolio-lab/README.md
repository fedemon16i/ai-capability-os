# Portfolio Lab

Real-world test bench for capability validation.

**Repo:** `fedemon16i/federico-portfolio`  
**Stack:** Pure HTML + CSS + Vanilla JS. No frameworks, no build step.

---

## What this is

The portfolio is Federico's own site — a real product with real design decisions, real implementation history, and real issues. It serves as a safe, meaningful laboratory for testing capabilities before applying them to client or commercial work.

---

## Why it's a good lab

- Real codebase with real inconsistencies (not a toy example)
- Has an evolving design system (custom CSS variables, tokens, components)
- Has dark/light mode — a classic design system challenge
- Has animation and motion — tests easing and motion capabilities
- Has responsive behavior — tests responsive audit capabilities
- Has accessibility needs — tests a11y capabilities
- Federico knows it intimately — he can judge quality accurately

---

## Experiments run here

| Date | Capability tested | Result | Link |
|------|-----------------|--------|------|
| 2026-08 | Light mode fix — Skills player inner mock UI | SUCCESS | *(learning record pending)* |
| 2026-08 | Light mode fix — EY Fabric player | SUCCESS | *(learning record pending)* |
| 2026-08 | Blockchain player text slide contrast | SUCCESS | *(learning record pending)* |
| 2026-08 | Project navigation order correction | SUCCESS | *(learning record pending)* |

---

## Active test cases

Things in the portfolio that would be good test cases for future capabilities:

| Area | What to test | Good for capability |
|------|-------------|---------------------|
| Design system | Audit consistency of CSS vars | Design System Audit |
| Motion | Verify all animations use `--spring` correctly | Motion Audit |
| Accessibility | Run a11y audit across all pages | Accessibility Audit |
| Responsive | Verify 320/375/768/1024/1440/1920 breakpoints | Responsive Audit |
| Visual QA | Check for text-on-background contrast across themes | Visual QA |

---

## Rules

- Never break the portfolio to test a capability
- Run tests on a branch, never directly on main
- Document the experiment even if it fails
- A failed experiment is as valuable as a success — it tells us about capability limits
