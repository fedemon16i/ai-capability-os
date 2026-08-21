# Research Protocol

How to run a research cycle in the AI Capability OS.

---

## When to run a research cycle

- Before adopting a new capability domain
- When an existing tool feels insufficient
- Quarterly review of each domain
- When a new category emerges (new class of AI tools, new MCP patterns, etc.)

---

## The 11-step cycle

### Step 1 — Define the question

What capability are we researching?  
What problem is it meant to solve?  
What does "good" look like?

Write this down before searching. It prevents scope creep.

### Step 2 — Discover broadly

Search across:
- GitHub (stars, recent activity, topics)
- Official documentation ecosystems
- Known community resources
- Curated directories
- Technical blogs
- Existing capabilities in this OS (check before searching externally)

Do not evaluate yet. Just collect candidates.

Tools available for this step:
- `r.jina.ai/{url}` — clean markdown from any page
- `firecrawl` — crawl full doc sections
- GitHub search API
- Web search

### Step 3 — Deduplicate

Remove:
- Forks that are identical to the original
- Tools that solve exactly the same problem with no differentiation
- Dead projects (last commit > 18 months, no releases)

### Step 4 — Evaluate each candidate

Score against the [Evaluation Framework](EVALUATION-FRAMEWORK.md).

Focus on:
- Does it solve the right problem?
- Is it mature enough to trust?
- Does it integrate with Federico's stack?
- What does the delegation level look like?

### Step 5 — Compare alternatives

For the top 3-5 candidates:
- Side-by-side comparison on key criteria
- Identify the essential tradeoff

### Step 6 — Identify the underlying capability

Even if no tool is adopted, name the capability.  
A capability can exist before its best tool is found.

### Step 7 — Identify what is worth learning

What concept must Federico understand to use this well?  
(Not implement — use.)

### Step 8 — Identify what can be delegated

What execution work can AI fully own?

### Step 9 — Select a default

Pick one tool to adopt as the current default.  
Explain why in one paragraph.

### Step 10 — Test when practical

If the portfolio lab or another real problem is a good test bed:
- run a small test
- document the result in `/experiments/`

### Step 11 — Document and update

- Create or update the capability entry in `/capabilities/`
- Create or update the tool entry in `/tools/`
- Archive the research in `/research/{year-month}/`
- Update `capabilities/_index.md`

---

## Research cycle document format

File: `/research/{year-month}/{capability-area}.md`

```markdown
# Research: {Capability Area}

**Date:** {date}  
**Trigger:** {why we researched this}  
**Researcher:** {Federico / Claude / agent name}

---

## Question

{What we were trying to answer}

## Candidates discovered

| Tool | URL | Stars | Last updated | Notes |
|------|-----|-------|--------------|-------|
| | | | | |

## Eliminated

| Tool | Reason |
|------|--------|
| | |

## Top candidates evaluated

### {Tool 1}
Score: {total}/50  
Strengths: ...  
Weaknesses: ...

### {Tool 2}
Score: {total}/50  
Strengths: ...  
Weaknesses: ...

## Comparison

{Side-by-side on key dimensions}

## Underlying capability

{Name and description of the capability}

## Selected default

**{Tool}** — {one paragraph justification}

## What Federico needs to understand

{Short explanation of the concept}

## What Federico does NOT need to learn

{Delegated complexity}

## Next steps

- [ ] Create capability entry
- [ ] Create tool entry
- [ ] Run test in portfolio lab
- [ ] Update capability index
```

---

## Source catalog

Sources used for discovery are tracked in [`sources/_catalog.md`](sources/_catalog.md).

This prevents repeating the same searches and builds institutional memory about which sources are reliable.
