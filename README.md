# AI Capability OS

**Federico Monroy's personal AI Capability Operating System.**

This is not a documentation project. It is an operating system for solving product problems using AI leverage.

---

## What this is

A structured, evolving library of capabilities that allows Federico to:

- delegate technical execution reliably
- retain product judgment and quality control
- discover, evaluate, and adopt the best AI tools available
- capture what works so it can be reused
- build toward a Product Intelligence platform

The system is organized around **capabilities**, not tools.

A tool is replaceable. A capability is transferable.

---

## How to navigate

| Directory | What it contains |
|-----------|-----------------|
| `/capabilities` | Indexed library, organized by domain |
| `/packs` | Assembled Capability Packs (capability + tool + agent + workflow) |
| `/tools` | Individual tool evaluations |
| `/agents` | Agent configurations and prompts |
| `/mcps` | MCP server catalog |
| `/skills` | Reusable AI skills and prompts |
| `/workflows` | Automation (n8n, GitHub Actions, scripts) |
| `/research` | Research cycles — raw discoveries and evaluations |
| `/learning` | Knowledge capture records (after-action, by problem solved) |
| `/experiments` | Real-world tests, including the portfolio lab |
| `/decisions` | Architecture Decision Records |
| `/sources` | Discovery source configurations |
| `/templates` | Blank templates for every document type |

---

## Core model

```
REAL PROBLEM
→ AI/agent solves it
→ inspect the result
→ extract the capability
→ document the pattern
→ add to Capability OS
→ reuse
```

---

## Classification system

Every resource is classified as:

| Class | Meaning |
|-------|---------|
| **ADOPT** | We intend to use it |
| **LEARN** | Federico needs to understand the concept |
| **STUDY** | Technically interesting, not currently needed |
| **REFERENCE** | Useful to retain, no deep learning required |
| **IGNORE** | Low leverage, redundant, immature, or irrelevant |

---

## Research discipline

```
100 discovered → 30 relevant → 15 evaluated → 8 tested → 3 adopted
```

We value curation over quantity.

---

## Start here

- [`PRINCIPLES.md`](PRINCIPLES.md) — how this system operates
- [`FEDERICO.md`](FEDERICO.md) — who Federico is and what he's optimizing for
- [`ARCHITECTURE.md`](ARCHITECTURE.md) — how the system is structured and why
- [`CAPABILITY-MODEL.md`](CAPABILITY-MODEL.md) — what a capability is
- [`RESEARCH-PROTOCOL.md`](RESEARCH-PROTOCOL.md) — how to run a research cycle
- [`EVALUATION-FRAMEWORK.md`](EVALUATION-FRAMEWORK.md) — how to score candidates
- [`capabilities/_index.md`](capabilities/_index.md) — master capability registry

---

## Current status

> **Phase 1:** System architecture established.  
> **Phase 2:** First research cycle — pending.  
> **Phase 3:** First capability packs — pending.

Last updated: 2026-08-21
