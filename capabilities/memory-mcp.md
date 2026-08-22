# Capability: Memory MCP

**Domain:** ai-engineering  
**Status:** ADOPT  
**Delegation level:** 5 / 5  
**Score:** 66 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Claude sessions start cold — no memory of Federico's preferences, ongoing projects, client context, past decisions, or design system rules — the first 20% of every session is spent re-establishing context. Memory MCP eliminates this.

## Underlying concept

Every Claude conversation starts with a blank context window. CLAUDE.md partially solves this for repo-specific sessions, but it doesn't carry project history, evolving preferences, or cross-session decisions forward.

Memory MCP is a local knowledge graph that Claude reads and writes during a session. It stores entities (people, projects, tools, decisions) and their relationships, persisting them between sessions. Claude queries it at the start of a session and updates it when new relevant information emerges.

The Ponytail moment: Federico never manually maintains a "context file." Claude updates its own memory as it works, and recalls it the next time Federico opens a session.

## When to use

- Any session that benefits from remembering previous decisions or context
- Ongoing projects where decisions accumulate (design system choices, client preferences, infrastructure decisions)
- Cross-session work where Federico switches contexts and returns
- When CLAUDE.md isn't enough because context is dynamic rather than static

## When NOT to use

- One-off tasks with no follow-up — memory overhead isn't worth it
- Tasks where fresh eyes are better than remembered context (e.g., a fresh accessibility audit that shouldn't be biased by past results)
- Sensitive data that shouldn't persist anywhere (credentials, client PII)

## Federico's role

Install once. Optionally review the memory store periodically. Correct wrong assumptions when Claude recalls something inaccurate.

## AI's role

Query the knowledge graph at session start, update it with new entities and relationships as they emerge, and use stored context to skip re-establishment overhead.

## Current best implementation

**Tool:** Memory MCP (Anthropic official)  
**Why chosen:** Official Anthropic implementation, no API key required, local knowledge graph (data stays on the machine), open source. Highest trust level for a persistence layer.  
**Install:** `npx @modelcontextprotocol/server-memory`  
**Docs:** https://github.com/modelcontextprotocol/servers/tree/main/src/memory  
**License:** MIT

## Alternatives considered

| Tool | Why not selected |
|------|-----------------|
| Mem0 MCP | Cloud-synced alternative. Growing fast (660+ GitHub stars). Better for team-shared memory. Higher trust risk than local. STUDY. |
| Managed Agents Persistent Memory | Anthropic's platform-managed memory (public beta, April 2026). Highest Ponytail score when mature. API-accessible and team-sharable. LEARN — will likely become the dominant approach within 12 months. |
| Obsidian + LightRAG | High setup cost, indirect Claude integration. Only worthwhile at 50K+ notes. STUDY. |
| CLAUDE.md | Static context only — works for repo rules but not for evolving project history. Use both in combination. |

## Delegation level

**5/5** — Fully autonomous. Claude queries and writes memory without Federico directing it.

## Ponytail score

**8/10** — Eliminates the most consistent friction in AI workflows (context re-establishment). One install, no ongoing maintenance.

## Related capabilities

- [AI Coding Agent](ai-coding-agent.md) — primary beneficiary of persistent memory
- [Agent Orchestration](agent-orchestration.md) — shared memory across orchestrated agents
- [GitHub MCP](github-mcp.md) — repo context that memory can reference

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| | | | |

## Notes

- The memory store is a local JSON file (knowledge graph). Back it up — it's not version-controlled by default.
- Pair with a `MEMORY.md` in project roots: a structured file Claude is instructed to update at session end via a hook. Belt-and-suspenders approach.
- Privacy: all data stored locally. Nothing sent to Anthropic. Verify by reading the open source code before installing.
- Gap to watch: Memory MCP stores *what was said*, not *what was decided and why*. Supplement with decision-record.md files for durable architectural decisions.
