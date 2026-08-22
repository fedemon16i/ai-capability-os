# Capability: Agent Orchestration

**Domain:** ai-engineering  
**Status:** ADOPT  
**Delegation level:** 4 / 5  
**Score:** 64 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When a task is too large or complex for a single AI session — requiring parallel research across multiple domains, independent verification, or sequential stages where each stage informs the next — single-agent approaches are too slow, too shallow, or hit context limits.

## Underlying concept

Agent orchestration is the practice of coordinating multiple AI agents to accomplish a task that no single agent could handle as well alone. The orchestrator (Claude in supervisor mode, or Federico himself) breaks work into subtasks, assigns each to a specialized agent, and synthesizes the results.

Three core patterns:
- **Fan-out (parallel):** Multiple agents work simultaneously on independent subtasks. Wall-clock time = slowest single agent, not sum of all. Used for: research across multiple domains, parallel code reviews, multi-dimensional audits.
- **Pipeline (sequential):** Each agent's output feeds the next. Used for: discover → evaluate → synthesize → implement.
- **Adversarial:** Multiple agents independently evaluate the same finding and vote. Used for: verifying AI-generated conclusions before acting on them.

Federico is already running a supervisor pattern via CLAUDE.md + Skills. The natural next step is fan-out: when a research task covers 5 domains, launch 5 agents and synthesize in parallel rather than sequentially.

The Ponytail moment: "Research these 5 capability domains and give me the top picks" → 5 agents run simultaneously, results in 10 minutes instead of 50.

## When to use

- Research across multiple independent domains simultaneously
- Tasks too large for a single context window (large codebase audits, multi-file migrations)
- When independent verification adds value (AI-checked AI output)
- Recurring workflows that can be scripted (weekly research cycle, audit sweep)

## When NOT to use

- Simple, linear tasks — overhead of orchestration outweighs the benefit
- When results need to be sequential and each depends on the prior (use pipeline, not parallel)
- When Federico needs to make a decision mid-task — agents don't pause for product judgment

## Federico's role

Define the task decomposition. Write the orchestration prompt or script. Review synthesized outputs. Make judgment calls on findings. Redirect agents that go off-track.

## AI's role

Execute assigned subtasks. Return structured outputs. (In Claude Code Workflows) manage concurrency automatically.

## Current best implementation

**Tool:** Claude Code Agent tool (subagents) + Workflow scripts  
**Why chosen:** Native to Federico's existing Claude Code setup. No additional infrastructure. Supports both ad-hoc fan-out (Agent tool) and scripted orchestration (Workflow). The Agent tool alone is sufficient for most research and audit tasks.  
**Docs:** https://claude.ai/code  
**License:** Proprietary (Anthropic) — included in Claude Max / Pro plans

## Alternatives considered

| Tool | Why not selected |
|------|-----------------|
| n8n + AI agent nodes | Better for recurring, trigger-based workflows (scheduled, event-driven). Higher setup cost but highest Ponytail score for automation. LEARN — add when recurring workflows emerge. |
| CrewAI | Good for prototyping multi-agent systems. Too engineer-heavy for Federico's use case. STUDY for understanding the pattern. |
| LangGraph | The production standard for stateful agent workflows in 2026. High engineering overhead. Value for Federico: understand the state graph mental model for speccing systems, not building them. STUDY. |
| AutoGen | Microsoft's multi-agent framework. More research-oriented. REFERENCE. |

## Delegation level

**4/5** — Federico defines the task decomposition and reviews final output. Execution is fully delegated.

## Ponytail score

**8/10** — The Agent tool in Claude Code requires no infrastructure — fan-out is available immediately. The main investment is learning to decompose tasks correctly.

## Roles formales en la arquitectura supervisada

Esta arquitectura define quién hace qué en un ciclo de orquestación:

| Rol | Responsabilidad | Permisos |
|-----|-----------------|---------|
| **Supervisor** | Define brief, asigna, revisa, acepta/rechaza, commit final, actualiza STATUS.md | Único con write al repo |
| **Research Worker** | Investiga un dominio específico | Solo output estructurado |
| **Curator Worker** | Compara, elimina ruido, scores | Solo output estructurado |
| **Writer Worker** | Escribe el documento final según template | Solo output estructurado |
| **Quality Guardian** | Verifica que el output cumpla principios del sistema | Puede vetar |

**Regla de oro:** ningún Worker escribe directamente al repositorio.

### Manejo de errores en orquestación

| Error | Comportamiento |
|-------|---------------|
| Rate limit | Reintentar una vez con delay. Dos fallos → marcar BLOCKED en STATUS.md, continuar con otras tareas |
| Output mal formado | Rechazo automático, reenviar con formato explícito |
| Quality Guardian veta | Worker reescribe con razón específica. Max 2 iteraciones |
| Outputs contradictorios | Supervisor resuelve explícitamente — nunca mezclar silenciosamente |
| Fallo parcial (1 de N agentes) | Procesar los exitosos, documentar fallidos, re-agendar |

---

## Six concepts Federico must own

1. **Context window = working memory** — finite. Every agent starts fresh. Memory MCP and CLAUDE.md are how context persists.
2. **Orchestrator vs. worker** — the orchestrator plans and synthesizes; workers execute. Never conflate the roles in one agent.
3. **Fan-out vs. pipeline** — parallel when subtasks are independent; sequential when each depends on the prior.
4. **Memory tiers** — in-context (current session), session (CLAUDE.md/skills), persistent (Memory MCP). Know which tier a piece of context lives in.
5. **Skills as Ponytail abstraction** — Federico's current Skills are already the orchestration layer. Slash commands = encapsulated agent workflows.
6. **Tool use vs. agent delegation** — MCP = giving Claude a tool. Subagent = delegating a task to another Claude. Know which you're configuring.

## Related capabilities

- [AI Coding Agent](ai-coding-agent.md) — the worker agent in most orchestrations
- [Memory MCP](memory-mcp.md) — shared context across orchestrated agents
- [GitHub MCP](github-mcp.md) — agents can create issues and PRs as task outputs

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| 2026-08 | Research Cycle #1 — 5-domain parallel research | SUCCESS (3/5 agents completed; 2 hit rate limits) | this repo |

## Notes

- Rate limits apply per session — parallel agents share the same session's rate budget. Burst 5+ agents simultaneously risks hitting limits mid-task.
- The `Workflow` tool in Claude Code is more robust than ad-hoc Agent tool use — it handles retries, caching, and structured output schemas. Use for repeatable patterns.
- Standard patterns (safe to build on): CLAUDE.md + Skills, Claude Code subagents, n8n workflows.
- Experimental patterns (watch, don't bet on): Managed Agents memory (beta), cross-tool shared memory, self-modifying CLAUDE.md.
