# MCP Server Catalog

MCP (Model Context Protocol) servers that give AI agents real capabilities beyond text generation.

**Last updated: 2026-08-22 — Research Cycle #1**

---

## What MCP is

MCP is a standard protocol that lets AI models (Claude, etc.) connect to external tools and data sources.  
Instead of just generating text, Claude can: read files, search the web, query databases, call APIs, control browsers.

**The key insight:** an MCP server is a Ponytail-style capability — it encapsulates complex integrations behind a simple AI-accessible interface.

75,000+ public servers in the ecosystem (Glama registry, August 2026).

---

## ADOPTED

| Server | What it enables | Source | Status |
|--------|----------------|--------|--------|
| Figma MCP | Read/write Figma files, design-to-code, code-to-design | figma.com | Active in sessions |

---

## ADOPT — install on Federico's machine

| Server | What it enables | Install | Priority |
|--------|----------------|---------|----------|
| **Memory MCP** | Persistent knowledge graph across sessions — entities, relationships, project history. No API key. Data stays local. | `npx @modelcontextprotocol/server-memory` | #1 |
| **GitHub MCP** | Issues, PRs, CI status, code search from within Claude. Requires GitHub PAT (`repo` scope). | `npx @modelcontextprotocol/server-github` | #2 |

---

## LEARN — evaluate when the use case appears

| Server | What it enables | Notes |
|--------|----------------|-------|
| **Playwright MCP** | Browser automation — portfolio QA, visual regression, responsive testing | #1 globally by usage in 2026. High value for portfolio QA. |
| **Notion MCP** | Read/write Notion pages from Claude — PM docs ↔ AI execution | Needs Notion API key |
| **Linear MCP** | Issue tracking, sprint management via natural language | Only relevant if team uses Linear |
| **Brave Search MCP** | Real-time web search without leaving Claude | Useful if Notion MCP isn't needed |
| **Vercel MCP** | Deploy previews, env vars, rollback via natural language | Relevant if hosting moves to Vercel |
| **Supabase MCP** | Full database + auth management via chat | Relevant for prototypes with real backends |

---

## STUDY — watch, don't adopt yet

| Server | What it enables | Why watch |
|--------|----------------|-----------|
| **Sequential Thinking MCP** | Improves Claude's reasoning on complex decisions (#1 on Smithery, 5,550+ uses) | High usage signal — test on a real complex decision |
| **Mem0 MCP** | Cloud-synced memory alternative to Memory MCP (660+ stars, growing fast) | Better for team-shared context. Monitor for stability. |

---

## NOT USEFUL for this setup (crossed off shortlist)

| Server | Why skip |
|--------|----------|
| Filesystem MCP | Redundant — Claude Code has Read/Write/Edit tools built in |
| Brave Search MCP | Redundant — Claude Code already has WebSearch tool |

---

## How to install (Claude Desktop)

Open Claude Desktop → Settings → Developer → Edit Config → add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your_pat_here"
      }
    }
  }
}
```

Restart Claude Desktop. The servers appear in the tools panel.

---

## Discovery directories

- **Glama:** glama.ai/mcp/servers — 75,000+ servers, comprehensive directory
- **Smithery:** smithery.ai — curated marketplace with usage rankings
- **Awesome MCP:** github.com search "awesome-mcp"
- **Anthropic official:** github.com/modelcontextprotocol/servers

---

## Evaluation criteria for MCP servers

In addition to the standard Evaluation Framework, MCP servers should also be scored on:

| Extra dimension | What to check |
|----------------|---------------|
| **Auth model** | What credentials does it need? Is that safe? |
| **Data exposure** | Does it send data to third parties? |
| **Scope** | Is the permission scope minimal and necessary? |
| **Claude compatibility** | Does it work with Claude Desktop + Claude Code? |
| **Stability** | Does it crash? Does it handle errors gracefully? |
| **Redundancy** | Does Claude Code already do this natively? |
