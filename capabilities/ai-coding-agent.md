# Capability: AI Coding Agent

**Domain:** ai-engineering  
**Status:** ADOPT  
**Delegation level:** 5 / 5  
**Score:** 68 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Federico needs to modify code across multiple files, fix bugs, build new sections, audit a codebase for issues, or execute any implementation task that would otherwise require hands-on coding.

## Underlying concept

A coding agent reads a full codebase, understands its structure and patterns, and executes multi-step implementation tasks autonomously — editing files, running git commands, and iterating on its own output without Federico writing a single line of code.

The key distinction from autocomplete tools: autocomplete suggests the next line while Federico types. An agent plans an entire task, executes it across multiple files, verifies the result, and reports back. Federico provides intent ("fix the overflow bug on mobile") and receives a finished, committed result.

The Ponytail moment: Federico describes what the code should do. The agent figures out how to make it do that, which files to touch, what edge cases to handle, and what to test.

## When to use

- Modifying the same pattern across multiple files (e.g., applying a new card style to all 6 project pages)
- Fixing a bug whose source isn't immediately obvious
- Building a new section or component from a design or description
- Running an audit (accessibility, responsive, CSS consistency)
- Any git workflow: commit, branch, push
- Translating a Figma design into working HTML/CSS
- Refactoring without knowing exactly what to change

## When NOT to use

- When the change is one line and the location is obvious — just open the file directly
- When the task requires product judgment ("should this button exist?") — that's Federico's call, not an implementation task
- When the output is for a stakeholder meeting and fidelity matters more than correctness (use v0 instead)

## Federico's role

Provide: the problem description, design intent, acceptance criteria, and final review. Approve or redirect. Make product decisions when the agent hits a fork.

## AI's role

Plan the implementation, make all file edits, handle edge cases, run git operations, iterate if needed, flag ambiguities.

## Current best implementation

**Tool:** Claude Code  
**Why chosen:** Deepest integration with Federico's exact stack (vanilla HTML/CSS/JS, GitHub Pages, no build step). 1M token context window handles entire codebase in one pass. CLAUDE.md carries design system rules directly into every session, eliminating repeated context setup. Already active.  
**Docs:** https://claude.ai/code  
**License:** Proprietary (Anthropic) — included in Claude Max / Pro plans

## Alternatives considered

| Tool | Why not selected |
|------|-----------------|
| Cursor | Requires switching editing environment. Overlaps with Claude Code. Lower value if Claude Code is already active. STUDY for awareness. |
| GitHub Copilot Coding Agent | Best for teams using VS Code + GitHub Issues workflow. Less direct for Federico's solo setup. REFERENCE. |
| Aider | CLI-only, no web UI, requires more manual setup. Lower Ponytail score. |
| Lovable | Better for full-stack app demos, not for refining an existing codebase. Different use case. |

## Delegation level

**5/5** — Full implementation tasks delegated end-to-end. Federico provides intent and approves output. No code written by Federico required.

## Ponytail score

**7/10** — Encapsulates multi-file planning, git operations, and pattern-matching across a codebase. Federico describes what he wants; the agent handles how. Not a full 10 because complex design decisions still require Federico's judgment as a redirect.

## Related capabilities

- [Memory MCP](memory-mcp.md) — gives Claude Code persistent context across sessions
- [GitHub MCP](github-mcp.md) — extends coding agent to full GitHub collaboration
- [Agent Orchestration](agent-orchestration.md) — fan-out pattern for parallel tasks
- [Figma MCP](figma-mcp.md) — design input for the coding agent

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| 2026-08 | Light mode fix — Skills player | SUCCESS | portfolio-lab experiment |
| 2026-08 | Light mode fix — EY Fabric player | SUCCESS | portfolio-lab experiment |
| 2026-08 | Blockchain player text contrast | SUCCESS | portfolio-lab experiment |
| 2026-08 | Project navigation order | SUCCESS | portfolio-lab experiment |
| 2026-08 | Home page layout fixes (TAP button, section width) | SUCCESS | portfolio-lab experiment |

## Notes

- CLAUDE.md is the primary context carrier — keep it current. It functions as Federico's standing instructions to every session.
- Skills (slash commands) are the Ponytail interface on top of the agent — they encapsulate entire workflows behind a single command. Treat them as capability multipliers, not shortcuts.
- The agent runs in an ephemeral container in Claude Code web sessions — nothing persists unless committed to git. Always push before ending a session.
- For portfolio work: push to the feature branch, never directly to main (per session rules). For ai-capability-os: push directly to main.
