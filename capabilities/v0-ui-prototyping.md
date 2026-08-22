# Capability: UI Prototyping (v0 by Vercel)

**Domain:** design-execution  
**Status:** ADOPT  
**Delegation level:** 5 / 5  
**Score:** 67 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Federico needs a functional UI prototype for stakeholder alignment, user research, or concept validation — and needs it in under 10 minutes from a description, without involving engineering or writing code himself.

## Underlying concept

v0 by Vercel translates plain English descriptions into working React + Tailwind UI components with a live preview, deployable via a shareable link. No install. No terminal. Browser only.

The tool's strength is not the quality of its code (it outputs React/Tailwind, not Federico's portfolio stack) — it's the speed from idea to visual artifact. A stakeholder meeting is 30 minutes away and you need to show a concept. v0 solves this.

The Ponytail moment: "A dashboard that shows our funnel drop-off by step with a table on the right" → functional, interactive preview ready to share before the meeting starts.

The key mental model: v0 is a **communication tool**, not a production code tool. The output is a visual artifact for alignment. Whether the code is React or vanilla HTML doesn't matter — the stakeholder sees what you described.

## When to use

- Stakeholder meetings where a visual speaks more than a description
- User research sessions where participants need something to react to
- Validating a product concept before committing engineering time
- Generating component references that Claude Code then translates into Federico's actual stack
- Any situation where "working mockup" > "Figma frame"

## When NOT to use

- Production code for Federico's portfolio (it generates React/Tailwind, not vanilla HTML/CSS)
- Tasks where design system fidelity matters (the output won't match Federico's CSS variables)
- When Figma is sufficient — a static Figma frame takes less time than a v0 session for simple visual concepts
- Long-term maintainable code — v0 output is disposable prototype material

## Federico's role

Write a clear description of the UI (what it contains, what it does, what state it shows). Review and redirect if the output misses intent. Share the link.

## AI's role

Generate the component, handle interactivity, deploy the live preview, iterate based on Federico's redirects.

## Current best implementation

**Tool:** v0 by Vercel  
**Why chosen:** Highest Ponytail score for UI prototyping — one description, one working preview. No install. Browser-only. Live share link included. $20/month Premium tier.  
**URL:** https://v0.dev  
**License:** Proprietary (Vercel)

## Alternatives considered

| Tool | Why not selected |
|------|-----------------|
| Lovable | Full-stack app builder — better when the prototype needs a database, auth, or real data. Different use case from v0. LEARN separately. |
| Figma | Better for static design fidelity, component libraries, handoff. Not interactive by default. Use Figma for design, v0 for interaction. |
| Claude Code (HTML/CSS) | Better for production code in Federico's actual stack. Slower to a shareable link than v0. |
| Bolt.new | Similar to v0. Lower adoption and polish. v0 has stronger Vercel ecosystem integration. |

## Delegation level

**5/5** — Fully delegatable. Federico writes the description; the tool generates the working prototype.

## Ponytail score

**10/10** — Maximum encapsulation for this use case. The entire complexity of UI development (component structure, responsive behavior, interaction states, deployment) disappears behind a single description.

## Related capabilities

- [AI Coding Agent](ai-coding-agent.md) — translates v0 output references into production HTML/CSS if needed
- [Figma MCP](figma-mcp.md) — for design-system-faithful prototypes vs. v0's speed-first approach

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| | | | |

## Notes

- The friction point: v0 outputs React + Tailwind. Federico's portfolio uses vanilla HTML/CSS. These are incompatible stacks. Treat v0 output as disposable — use it for alignment, not as a code starting point.
- The share link from v0 is public by default. Don't prototype anything confidential without checking the privacy settings.
- Best prompting pattern: describe the **scenario** first ("a product manager reviewing weekly retention"), then the **data** ("shows week-over-week retention % with a 12-week sparkline"), then the **layout** ("table on the left, chart on the right, filter bar at top").
- v0's February 2026 update added backend connections (Supabase, Neon) — this enables prototypes with real data if needed.
