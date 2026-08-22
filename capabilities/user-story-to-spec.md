# Capability: User Story → Product Spec

**Domain:** product-intelligence  
**Status:** ADOPT  
**Delegation level:** 4 / 5  
**Score:** 60 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Federico receives a user story — often long, messy, mixed with assumptions, written in a rush — and needs to turn it into a clean product spec that:
- Developers can build from without ambiguity
- Stakeholders can review and approve without a technical background
- QA can write test cases from
- Federico can use to validate the feature actually solves the original problem

## Underlying concept

A user story describes what a user wants. A product spec describes what to build, for whom, under what constraints, measurable how, with what edge cases covered.

The gap between them is where most product failures live: features built technically correct but that miss the point, or built correctly but not documented well enough for anyone to verify.

This capability uses Claude to bridge that gap — taking any form of user story input (even a Slack message or rough notes) and generating a structured, dual-audience spec: technical enough for engineers, readable enough for stakeholders.

**The output is not a template with blanks filled in.** It's a document that explains the feature as a product decision — why it exists, who it's for, what "done" looks like, what's out of scope, and where the story left gaps that need a decision.

**The Ponytail moment:** paste a messy user story → Claude returns a structured spec with requirements, scenarios, user role analysis, coverage gaps, and a stakeholder-facing visual summary — in one prompt.

## Output structure

The generated spec has two layers:

### Layer 1 — Technical spec (for engineers and QA)

| Section | Contents |
|---------|----------|
| Problem statement | What user problem this solves, evidence for it |
| User roles | Who is affected (primary, secondary, edge cases) |
| Requirements | Functional requirements, numbered, unambiguous |
| Scenarios | Happy path + key edge cases, in BDD format if needed |
| Out of scope | Explicitly excluded to prevent scope creep |
| Open questions | Gaps in the story that need a decision before building |
| Success metrics | How to measure whether this worked |
| Definition of done | Binary checklist for QA sign-off |

### Layer 2 — Stakeholder brief (for leadership, PO, clients)

- One-paragraph plain-language summary of the feature
- Who benefits and how (user impact, not feature description)
- What changes in the product when this ships
- What was decided to be out of scope and why
- Key risks or assumptions being made
- What approval or input is needed from them (if any)

### Optional: annotated visual

When the user story references a specific UI or flow, Claude can generate an HTML prototype with annotations explaining how each element responds to a requirement — visible to non-technical stakeholders without reading the spec.

## Acceptance criteria format (Gherkin)

Cada escenario en la spec sigue este patrón — validado en [deanpeters/product-manager-prompts](https://github.com/deanpeters/product-manager-prompts):

```
Scenario: [nombre del caso]
  Given [precondición / estado del sistema]
  When  [acción que dispara el comportamiento]
  Then  [resultado observable y verificable]
```

**Split signal:** si un escenario necesita múltiples `When` o múltiples `Then`, es señal de que la historia debe dividirse. Claude marca esto automáticamente en la Coverage Analysis.

**Regla de actor:** el usuario del escenario debe coincidir con el persona de la user story. Si no coinciden, la AC es incorrecta.

---

## The synthesis prompt

```
You are a senior product manager helping me turn a user story into a product spec.

Context:
[Paste product context: what the product does, who the users are, current state]

User story input:
[Paste the raw user story — any format, any length, even messy]

Generate a two-layer output:

LAYER 1 — Technical spec:
1. Problem statement (what user problem this solves, with evidence from the story)
2. User roles (primary user, secondary users, edge-case users)
3. Functional requirements (numbered, unambiguous, testable)
4. Key scenarios (happy path + top 3 edge cases)
5. Explicitly out of scope
6. Open questions (gaps that need a decision before building)
7. Success metrics (how we know this worked)
8. Definition of done (QA checklist)

LAYER 2 — Stakeholder brief (plain language, no jargon):
- What this feature does and why it matters
- Who benefits
- What stays the same (important for change management)
- What we decided NOT to build and why
- What you need from the stakeholder (approval, input, decision)

After generating, add a Coverage Analysis:
- What does the story clearly specify?
- What did you have to infer or assume?
- What is ambiguous or contradictory?
- What is missing that could cause rework?
- Label each gap as **Assumption** or **Open Question** — never invent facts to fill gaps.

Then add a Closing Self-Critique:
- Strongest section: [which section is best supported by the story]
- Weakest section: [which section had the most inference]
- Top 3 assumptions to validate before building

Finally, offer these four next steps (let me choose):
1. Generate scope cuts (up/down — smaller or larger version of this story)
2. Check for split signals and suggest how to split
3. Generate a test case checklist from the acceptance criteria
4. Write the stakeholder brief as a standalone email

Do NOT generate the annotated visual unless explicitly asked.
```

## When to use

- Any time a user story needs to become a buildable spec
- Before handing a feature to engineering (even for solo/small team contexts)
- When a stakeholder provides a feature request in natural language
- When turning a Jira ticket, Slack message, or email into a formal document
- When Federico needs to validate whether a story is actually complete enough to build

## When NOT to use

- For technical architecture decisions — this is a product capability, not a system design tool
- When the story is already a complete spec (adding layer on top of a good spec wastes time)
- For exploratory research questions — this is a transformation tool, not a discovery tool
- As a substitute for talking to users — the spec describes what to build, not whether to build it

## Federico's role

Provide the raw user story and the product context. Review the generated spec section by section — especially the Coverage Analysis (open questions and ambiguities are high-value). Make the judgment calls on open questions. Decide what goes to the stakeholder layer and what stays internal.

## AI's role

Parse the story for explicit requirements, inferred requirements, and gaps. Structure them unambiguously. Write both layers with different voice and detail level. Flag assumptions and contradictions. Generate the annotated visual on request.

## Delegation level

**4/5** — Full spec draft delegated. Federico reviews for product accuracy (Claude doesn't know the business context, team velocity, or political constraints) and makes calls on open questions.

## Ponytail score

**8/10** — Takes any-format input and produces a structured, dual-audience document. The mechanical work of structuring, formatting, identifying gaps, and writing for two audiences simultaneously is fully delegated.

## Related capabilities

- [Product Intelligence](product-intelligence.md) — the research synthesis that feeds into user stories
- [UI Integrity Guardian](ui-integrity-guardian.md) — runs after the spec is implemented to verify UI quality
- [Session Replay](session-replay.md) — validates the implemented feature against real user behavior
- [v0 UI Prototyping](v0-ui-prototyping.md) — generates the annotated visual when needed

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| | | | |

## Sources incorporados

- [deanpeters/product-manager-prompts](https://github.com/deanpeters/product-manager-prompts) — user-story-prompt-template.md (Mike Cohn + Gherkin + split signals, CC BY-NC-SA 4.0) y prd-prompt-template.md (9-section PRD, closing self-critique). Validados en Claude/ChatGPT/Gemini.
- [Ponytail score 8/10] encapsula: estructuración, Gherkin, split detection, dual-audience writing, gap labeling.

## Notes

- **The Coverage Analysis es el output de mayor valor.** Engineers build from requirements. Federico's value is in catching the gaps before building starts. The Coverage Analysis is where Claude earns its keep — it surfaces what Federico would have missed in a rushed review.
- **Confidence signal:** ask Claude to rate its confidence in each requirement (high/medium/low based on how explicitly the story supports it). Low-confidence requirements need a conversation before building.
- **Iterative use:** generate the full spec, then use follow-up prompts to drill into specific sections: "Rewrite the edge cases for the role of [user type X]" or "What would the QA test cases look like for requirement 3?"
- **Annotated visual:** when the story references a specific UI, the annotated HTML page is a powerful stakeholder communication tool — it shows exactly how each element connects to a requirement, without requiring the stakeholder to read the spec.
