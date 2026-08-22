# Capability: GitHub MCP

**Domain:** ai-engineering  
**Status:** ADOPT  
**Delegation level:** 4 / 5  
**Score:** 62 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Federico needs to interact with GitHub beyond git operations — querying issues, reviewing PRs, checking CI status, creating releases — currently requiring context switching out of Claude and into the browser.

## Underlying concept

GitHub MCP connects Claude directly to the GitHub API. Instead of switching to github.com to read an issue, check a PR, or search repository history, Federico describes what he needs in natural language and Claude executes the GitHub operation.

Combined with Claude Code's git operations (commit, push, branch), GitHub MCP closes the loop: Claude Code writes and pushes code, GitHub MCP manages everything that happens after the push — reviews, issues, CI feedback, releases.

The Ponytail moment: "Create an issue for the accessibility audit findings" → Claude creates a structured issue with the right labels and assigns it. No browser required.

## When to use

- Querying or creating GitHub issues from within a Claude session
- Reviewing pull request status or CI checks without leaving Claude
- Searching repository history or code across repos
- Creating releases or managing branches via natural language
- Cross-repository work (checking related repos without browser switching)
- When collaborating with a team that tracks work in GitHub Issues/PRs

## When NOT to use

- Simple git operations (push, commit, pull) — Claude Code handles these natively without MCP
- When the task is visual (reviewing a PR diff visually is better in the browser)
- For sensitive repo operations (force push, repo deletion) — browser confirmation is safer

## Federico's role

Describe the GitHub operation in plain language. Review any created artifacts (issues, PRs) before merging or publishing.

## AI's role

Execute GitHub API calls, format outputs (issue bodies, PR descriptions), search and retrieve repository data, create and update GitHub objects.

## Current best implementation

**Tool:** GitHub MCP (GitHub official)  
**Why chosen:** Official GitHub implementation. Actively maintained. Full GitHub API coverage. Required: GitHub PAT (Personal Access Token) with `repo` scope.  
**Install:** `npx @modelcontextprotocol/server-github`  
**Docs:** https://github.com/modelcontextprotocol/servers/tree/main/src/github  
**License:** MIT

## Alternatives considered

| Tool | Why not selected |
|------|-----------------|
| gh CLI (GitHub CLI) | Already usable from Claude Code's bash tool. Lower Ponytail score — requires knowing CLI commands. GitHub MCP is higher abstraction. |
| Linear MCP | Better if the team tracks work in Linear, not GitHub Issues. LEARN if Linear is adopted. |

## Delegation level

**4/5** — Most GitHub operations fully delegated. Federico reviews created artifacts before publishing (issues, PR descriptions).

## Ponytail score

**7/10** — Significant friction reduction for team workflows. Lower in solo contexts where gh CLI already works.

## Related capabilities

- [AI Coding Agent](ai-coding-agent.md) — the primary tool that generates code pushed to GitHub
- [Memory MCP](memory-mcp.md) — GitHub repo context stored in memory across sessions
- [Agent Orchestration](agent-orchestration.md) — orchestrated agents can create and track issues

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| | | | |

## Notes

- Requires a GitHub PAT with `repo` scope. Store securely — not in any tracked file.
- For Claude Code web sessions: GitHub access is managed by the session's proxy (add_repo tool), which is separate from GitHub MCP. Both can coexist.
- Most immediately valuable: querying issues and CI status without context switching. Less immediately valuable: issue/PR creation (the browser is fine for these).
- Priority: install Memory MCP first, GitHub MCP second.
