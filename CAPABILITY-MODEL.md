# Capability Model

What a capability is, how it's defined, and how to document one.

---

## Definition

A **capability** is something Federico can reliably do (or direct AI to do) to solve a class of product problems.

A capability is NOT:
- a specific tool
- a specific model
- a specific API
- a prompt

A capability IS:
- transferable across tool versions
- applicable to multiple problems
- describable independently of implementation
- improvable over time

---

## The capability anatomy

Every capability entry answers:

### Problem class
What category of problems does this solve?  
(Not "what does the tool do" — what real friction does this remove?)

### Underlying concept
What is the essential idea?  
(One paragraph. No jargon if avoidable.)

### When to use
Specific triggering conditions. Be precise.

### When NOT to use
Equally important. Prevents misapplication.

### Federico's role
What does Federico provide? (intent, judgment, approval, constraints)

### AI's role
What does AI provide? (analysis, implementation, iteration, validation)

### Current best implementation
The strongest current tool/agent for this capability.

### Alternatives
What else exists. Why we chose what we chose.

### Delegation level
Scale 1-5.  
1 = Federico must be deeply involved.  
5 = Fully delegatable with minimal supervision.

### Classification
ADOPT / LEARN / STUDY / REFERENCE / IGNORE

### Related capabilities
Other capabilities this connects to.

### Related packs
Capability Packs that use this.

---

## Capability entry format

File: `/capabilities/{domain}/{capability-name}.md`

```markdown
# Capability: {Name}

**Domain:** {domain}  
**Status:** ADOPT | LEARN | STUDY | REFERENCE | IGNORE  
**Delegation level:** {1-5}  
**Last updated:** {date}

---

## Problem class

{What category of problems this solves}

## Underlying concept

{Essential idea in 1-3 paragraphs}

## When to use

- {condition}
- {condition}

## When NOT to use

- {condition}
- {condition}

## Federico's role

{What Federico provides}

## AI's role

{What AI provides}

## Current best implementation

**Tool:** {name}  
**Why:** {one line reason}  
**Docs:** {URL}  
**License:** {license}

## Alternatives considered

| Tool | Reason not selected |
|------|---------------------|
| {tool} | {reason} |

## Delegation level

{score}/5 — {explanation}

## Related capabilities

- [{name}]({path})

## Related packs

- [{name}]({path})

## Learning record

- [{date} — {problem}]({path to learning record})
```

---

## The Ponytail pattern

Some capabilities are **Ponytail-like**: they encapsulate significant technical complexity behind a usable workflow.

These are the highest-value capabilities to discover and adopt.

Characteristics of a Ponytail-like capability:

- High technical complexity underneath
- Simple interface on top
- Reusable across multiple problem instances
- Doesn't require deep implementation knowledge to use correctly
- Has a clear input/output contract

When evaluating tools, always ask: **does this encapsulate complexity I don't want Federico to own?**

High Ponytail score = high adoption priority.

---

## Domain index

Capabilities live under one of these domains:

| Domain | Path |
|--------|------|
| Product Intelligence | `/capabilities/product-intelligence/` |
| Design Execution | `/capabilities/design-execution/` |
| AI Engineering | `/capabilities/ai-engineering/` |
| Automation | `/capabilities/automation/` |
| Research | `/capabilities/research/` |
| Software Understanding | `/capabilities/software-understanding/` |

See [`capabilities/_index.md`](capabilities/_index.md) for the full registry.
