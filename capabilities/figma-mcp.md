# Capability: Figma MCP (Design-to-Code)

**Domain:** design-execution  
**Status:** ADOPT  
**Delegation level:** 4 / 5  
**Score:** 66 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Federico has a design in Figma and needs it implemented as code — without manually transcribing measurements, colors, fonts, spacing, and structure from Figma into HTML/CSS.

Also: when Federico wants Claude to reference Figma design decisions (components, variables, styles) while implementing code, rather than working from verbal descriptions.

## Underlying concept

Figma MCP connects Claude directly to the Figma API. Claude can read frame structures, component properties, design tokens (variables), styles, and generate accurate HTML/CSS from what it reads — rather than from Federico's verbal description of what he designed.

The translation layer that used to exist (Federico describes a design → Claude guesses at the intent) disappears. Claude reads the actual design.

Additional direction: Claude can write designs back into Figma from code or intent. This makes the bridge bidirectional: Figma → code and code → Figma.

The Ponytail moment: "Implement this frame as a section in the portfolio" → Claude reads the Figma frame, extracts the layout, colors, typography, and spacing, and generates the HTML/CSS. Federico reviews the output, not the translation process.

## When to use

- Implementing a Figma frame as a new page section or component
- Auditing whether existing code matches the Figma design (design-code sync)
- Extracting design tokens (colors, spacing, type scales) from Figma variables
- Generating Figma components from code description (code-to-design direction)
- Referencing Figma when Claude needs to understand the design intent behind a code change

## When NOT to use

- When the design isn't in Figma — for sketches or verbal descriptions, Claude Code alone handles the implementation
- When the Figma frame uses components or styles not in the project's design system (risk of inconsistent output)
- For pixel-perfect matching of complex animations — Figma doesn't encode animation timing; those need to be specified separately

## Federico's role

Provide the Figma URL or frame reference. Define implementation constraints (which CSS variables to use, what existing patterns to follow). Review the output against the design.

## AI's role

Read the Figma frame via the MCP API. Extract layout, styles, and structure. Generate HTML/CSS that matches the design. Iterate on Federico's feedback.

## Current best implementation

**Tool:** Figma MCP (official Figma server)  
**Why chosen:** Official implementation from Figma. Full API coverage including variables, components, styles. Active maintenance. Already integrated in Federico's Claude Code session.  
**Docs:** https://www.figma.com/developers/mcp  
**License:** Proprietary (Figma) — available with Figma account

## Alternatives considered

| Tool | Why not selected |
|------|-----------------|
| Manual transcription | The baseline. High error rate, time-consuming, no longer necessary. |
| Figma Dev Mode | Browser-only. Good for reading specs, but not for feeding directly into a Claude session. Figma MCP is higher abstraction. |
| Token Studio | Better for systematic design token management (export tokens to CSS/JSON for a build pipeline). Complementary, not competing. LEARN. |

## Delegation level

**4/5** — Implementation is fully delegated. Federico still reviews output against design intent and adjusts for the portfolio's specific CSS patterns and design system rules.

## Ponytail score

**8/10** — Eliminates the entire transcription layer between Figma and code. The complexity of reading a Figma file (frame tree, component resolution, variable inheritance) disappears behind a Figma URL.

## Related capabilities

- [AI Coding Agent](ai-coding-agent.md) — executes the implementation once Figma context is loaded
- [v0 UI Prototyping](v0-ui-prototyping.md) — alternative when speed > design fidelity
- [Memory MCP](memory-mcp.md) — stores design decisions across sessions

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| | | | |

## Notes

- The Figma MCP is already active in Federico's session. This is the starting state, not an install action.
- Figma variables (design tokens defined in Figma) are readable via MCP. This is the bridge to systematic design token management — a future capability to develop.
- The Code Connect feature (maps Figma components to codebase components) is the next level of integration — worth exploring when the portfolio has stable, reusable components.
- For the portfolio: Figma MCP should reference the actual component URLs, not just file-level access, for more precise reads.
