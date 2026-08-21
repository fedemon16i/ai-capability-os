# Source Catalog

Discovery sources used for research cycles.

**Before starting a research cycle, check if the relevant sources are already listed here.**

---

## Primary sources

### GitHub
- Search: `github.com/search?type=repositories&q={topic}`
- Topics: use GitHub topic search for `ai-agents`, `mcp`, `design-systems`, etc.
- Stars filter: prefer >200 for maturity signal
- Last commit: filter to <12 months
- Reliability: ★★★★★

### Jina Reader
- URL pattern: `r.jina.ai/{any-url}`
- Returns clean Markdown from any page
- Rate limit: generous on free tier
- Use for: extracting specific doc pages without full crawl
- Reliability: ★★★★☆

### Firecrawl
- URL: firecrawl.dev
- Use for: crawling entire documentation sections
- Returns: structured Markdown from multiple pages
- Rate limit: check current plan
- Reliability: ★★★★☆

---

## Documentation ecosystems

| Tool | Docs URL | What to find there |
|------|----------|--------------------|
| Anthropic / Claude | docs.anthropic.com | Prompting guides, tool use, MCP, skills |
| OpenAI | platform.openai.com/docs | GPT capabilities, Codex, structured outputs |
| Cursor | docs.cursor.com | AI coding agent features, rules, context |
| Figma | help.figma.com | Plugin API, variables, design system features |
| Pendo | support.pendo.io | Instrumentation, analytics, guide setup |
| Adobe | developer.adobe.com | Creative Cloud APIs |
| n8n | docs.n8n.io | Workflow automation patterns |

---

## Community resources

| Source | URL | What to find there | Reliability |
|--------|-----|-------------------|-------------|
| Awesome Claude | github.com/anthropics/awesome-claude | MCP servers, Claude skills | ★★★★★ |
| MCP directory | glama.ai/mcp/servers | MCP server catalog | ★★★★☆ |
| smithery.ai | smithery.ai | MCP server marketplace | ★★★★☆ |

---

## Notes

- Always check `robots.txt` before crawling
- Check ToS for commercial restrictions
- If a source requires auth, note it and do not scrape
- Add new sources here as they're discovered
