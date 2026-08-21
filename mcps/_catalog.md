# MCP Server Catalog

MCP (Model Context Protocol) servers that give AI agents real capabilities beyond text generation.

**Update as servers are evaluated and adopted.**

---

## What MCP is

MCP is a standard protocol that lets AI models (Claude, etc.) connect to external tools and data sources.  
Instead of just generating text, Claude can: read files, search the web, query databases, call APIs, control browsers.

**The key insight:** an MCP server is a Ponytail-style capability — it encapsulates complex integrations behind a simple AI-accessible interface.

---

## Catalog

### ADOPTED

| Server | What it enables | Source | Status |
|--------|----------------|--------|--------|
| Figma MCP | Read/write Figma files, design-to-code, code-to-design | figma.com | Active in this session |

### EVALUATED — not yet adopted

| Server | What it enables | Score | Classification |
|--------|----------------|-------|----------------|
| *(add after research cycle)* | | | |

### SHORTLISTED — not yet evaluated

| Server | What it enables | Source |
|--------|----------------|--------|
| Playwright MCP | Browser automation | github.com/microsoft/playwright-mcp |
| GitHub MCP | Read/write GitHub repos | github.com/github/github-mcp-server |
| Filesystem MCP | File operations | Built into Claude Desktop |
| Memory MCP | Persistent knowledge graph | github.com/anthropics/mcp-memory |
| Brave Search MCP | Web search | github.com/anthropics/mcp-servers |

---

## Discovery directories

- **Glama:** glama.ai/mcp/servers — comprehensive directory
- **Smithery:** smithery.ai — curated marketplace
- **Awesome MCP:** github.com search "awesome-mcp"
- **Anthropic examples:** github.com/anthropics/mcp-servers

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
