# Architecture

How the AI Capability OS is structured and why.

---

## Design decisions

### Why capabilities, not tools

Tools are implementations. Capabilities are what you can do.

When Claude is replaced by a better model, the capability (e.g., "code understanding") persists. When Figma changes its API, the capability (e.g., "design-to-code") persists.

Organizing by capability makes the system resilient to tool churn.

### Why Markdown + Git

- Readable by all AI systems without special tooling
- Portable across machines and environments
- Versioned by default
- Diffable — you can see what changed and why
- Works offline
- No proprietary format lock-in

### Why templates

Consistency enables AI to navigate the system predictably.  
Templates also reduce friction — a blank page is the enemy of capture.

### Why separate `/research` from `/capabilities`

Research is raw. Capabilities are curated.  
Research contains 100 candidates. Capabilities contain 3 adopted ones.  
Keeping them separate prevents the system from becoming a junkyard.

---

## Directory map

```
ai-capability-os/
│
├── README.md                    System overview
├── PRINCIPLES.md                Operating constraints
├── FEDERICO.md                  Context about Federico
├── ARCHITECTURE.md              This file
├── CAPABILITY-MODEL.md          Definition of a capability
├── RESEARCH-PROTOCOL.md         How to run research cycles
├── EVALUATION-FRAMEWORK.md      How to score candidates
│
├── capabilities/                The curated library
│   ├── _index.md               Master registry of all capabilities
│   ├── product-intelligence/
│   ├── design-execution/
│   ├── ai-engineering/
│   ├── automation/
│   ├── research/
│   └── software-understanding/
│
├── packs/                       Assembled Capability Packs
│   └── _template.md
│
├── tools/                       Individual tool evaluations
│   └── _template.md
│
├── agents/                      Agent configs and prompts
│   └── _template.md
│
├── mcps/                        MCP server catalog
│   └── _catalog.md
│
├── skills/                      Reusable AI skills and prompts
│   └── _template.md
│
├── workflows/                   Automation
│   ├── n8n/
│   ├── github-actions/
│   └── scripts/
│
├── research/                    Research cycles (raw)
│   └── _template.md
│
├── learning/                    After-action knowledge records
│   └── _template.md
│
├── experiments/                 Real-world tests
│   ├── _template.md
│   └── portfolio-lab/
│
├── decisions/                   Architecture Decision Records
│   └── _template.md
│
├── sources/                     Discovery source configs
│   └── _catalog.md
│
└── templates/                   All blank templates in one place
```

---

## The capability lifecycle

```
DISCOVER → EVALUATE → CLASSIFY → ADOPT → PACK → REUSE
```

### Discover
A research cycle surfaces candidates. Stored in `/research/`.

### Evaluate
Scored against the evaluation framework. Classification assigned.

### Classify
ADOPT / LEARN / STUDY / REFERENCE / IGNORE.  
Only ADOPT items proceed further.

### Adopt
A capability entry is created in `/capabilities/`.  
A tool entry is created in `/tools/` if there's a specific implementation.

### Pack
Related capabilities are assembled into a Capability Pack in `/packs/`.  
A pack includes: capability + tool + agent + workflow + validation method.

### Reuse
The pack is applied to real problems. Results captured in `/learning/`.

---

## The learning loop

```
Real problem
→ agent solves it using a capability
→ capture: what worked, what the capability was, what Federico needs to know
→ update capability entry if needed
→ update pack if needed
→ update learning record
```

Each iteration makes the system smarter.

---

## Capability domains

| Domain | Covers |
|--------|--------|
| `product-intelligence` | Analytics, instrumentation, insight, CRO, experimentation |
| `design-execution` | Design systems, tokens, motion, accessibility, Figma, design-to-code |
| `ai-engineering` | Agents, MCP, RAG, memory, evaluation, orchestration |
| `automation` | n8n, APIs, webhooks, scheduled agents, pipelines |
| `research` | Web research, repo discovery, competitive intelligence, source evaluation |
| `software-understanding` | Frontend, backend, DOM, codebase reading, browser automation |

---

## Multi-LLM strategy

This system is model-agnostic by design.

All capabilities are expressed as:
- a description of what the capability does
- what problem it solves
- how to invoke it (prompt, agent, workflow, tool)
- what the output looks like
- how to validate it

Any capable model can use this system as context.  
Claude Code establishes the canonical architecture.  
Other systems adapt to it.

---

## What this system is NOT

- Not a Wikipedia of AI tools
- Not a course curriculum
- Not a tool collection
- Not a knowledge dump

It is a **decision support system** for knowing what to reach for when a real problem needs solving.
