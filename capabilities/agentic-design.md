# Capability: Agentic Design

**Domain:** product-intelligence / design-execution  
**Status:** ADOPT  
**Delegation level:** 2 / 5  
**Score:** 58 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Federico needs to design products or experiences where humans and LLM agents collaborate in the same workflow — deciding what the human controls vs. what the agent executes, how the agent's work is made visible, how handoffs are designed, and how the experience handles uncertainty and agent failure.

This is not about designing AI features as a novelty. It's about designing the interaction layer between human judgment and agent execution in products that have both.

## Underlying concept

Agentic design is the discipline of designing human-agent collaborative systems. It's distinct from standard UX because:

1. **The agent acts, not just responds.** Traditional UI design: user triggers action, UI shows result. Agentic design: agent takes multi-step actions autonomously, user supervises and intervenes.

2. **Trust is earned, not assumed.** Users need to calibrate how much to trust the agent. The design must make trust earned and visible — not defaulted to.

3. **Failure is a first-class experience.** In standard UI, error states are edge cases. In agentic systems, partial completion, unexpected agent choices, and recovery paths are core to the experience.

4. **Human judgment is a product decision.** Deciding where the human must stay in the loop, where the agent can run autonomously, and how the handoff works — these are design decisions with UX consequences, not implementation details.

Federico is already practicing agentic design in his own AI workflow (supervising Claude Code, reviewing agent output, making judgment calls on agent choices). The capability is to apply this discipline to products he designs for others.

## The four design questions

Every agentic product experience must answer:

### 1. Division of authority
What does the human decide, and what does the agent decide?

| Decision type | Human | Agent |
|---------------|-------|-------|
| Product goals | ✓ Always | |
| Task decomposition | ✓ or shared | |
| Task execution | | ✓ Always |
| Output quality | ✓ Reviews | |
| Error recovery | ✓ Approves | ✓ Attempts |
| Final commitment | ✓ Always | |

### 2. Visibility of agent work
How does the human see what the agent is doing?

- **Narration:** agent announces each step before and after ("I'm going to modify shared.css — here's what I'll change")
- **Diff view:** show exactly what changed, not just "done"
- **Confidence signals:** agent flags uncertain decisions rather than resolving them silently
- **Audit trail:** history of agent decisions is readable and searchable

### 3. Handoff design
When does control move from agent to human, and how?

- **Trigger conditions:** what makes the agent stop and ask? (ambiguity, risk threshold, out-of-scope, cost limit)
- **Handoff format:** what does the agent hand to the human? (proposed action + alternatives + reasoning, not just "what should I do?")
- **Resume after human input:** how does the agent pick up after the human decides?
- **Graceful degradation:** if the agent can't complete the task, what does the partial output look like?

### 4. Uncertainty communication
How does the experience represent what the agent doesn't know?

- Never present agent output as certain unless it is
- Confidence levels on generated content
- Clear distinction between "I did this" vs "I inferred this" vs "I assumed this"
- Explicit flagging of decisions made without user input

## Measurement (emerging — 2026)

The metrics for agentic experiences are still maturing. Current best practices:

| Metric | Definition | Why it matters |
|--------|-----------|----------------|
| **Task completion rate by agent** | % of tasks completed without human intervention | Measures automation effectiveness |
| **Cost of human supervision** | Time/effort per agent task that requires human input | The ratio that determines ROI |
| **Trust calibration** | Do users trust the agent appropriately? (not too much, not too little) | Under-trust = friction; over-trust = errors |
| **Handoff quality** | When the agent stops to ask, is the human question clear and answerable? | Poor handoffs create bottlenecks |
| **Recovery rate** | % of agent errors the human successfully corrects | Tests whether the human-in-the-loop works |
| **Prompt-to-outcome accuracy** | Does the agent's output match what the user intended? | Core quality metric |

**Note on measurement maturity:** these metrics have no standardized benchmarks yet. Define project-specific baselines.

## When to use

- Designing any product feature where an AI agent takes actions on behalf of the user
- Specifying agent behavior boundaries in a PRD (what can the agent do autonomously?)
- Designing the "agent status" UI component (what does the user see while the agent works?)
- Defining handoff protocols between agent and human in a workflow
- Evaluating whether an existing feature's agent behavior is well-designed
- UX research on how users perceive and calibrate trust in agents

## When NOT to use

- For purely generative AI features that show output but don't take actions (those are standard UX with an AI output component)
- For backend agent orchestration design (that's engineering architecture, not product design)
- As a framework for building agent systems — this is for designing the human-facing experience of those systems

## Federico's role

Own the design decisions: where the human stays in the loop, what the handoff looks like, how uncertainty is communicated. These are product strategy calls, not implementation details. Review agent-facing UX with the same rigor as human-facing UX.

## AI's role

Generate UI mockups and interaction flows for agent states. Draft handoff protocol specifications. Analyze whether a proposed agentic workflow has ambiguous division of authority or missing uncertainty signals. Generate measurement frameworks for a specific agentic feature.

## Delegation level

**2/5** — Agentic design is fundamentally a product judgment capability. Federico owns the decisions. AI assists with documentation, mockup generation, and analysis — but the design choices are Federico's.

## Ponytail score

**4/10** — The conceptual framework is encapsulated here, but application requires Federico's product judgment for every decision. This is a thinking tool, not an automation tool.

## Related capabilities

- [Agent Orchestration](agent-orchestration.md) — the technical architecture for what agentic design specifies
- [Session Replay](session-replay.md) — captures how real users interact with agentic experiences
- [User Story → Product Spec](user-story-to-spec.md) — agentic features need specs that define agent authority boundaries
- [UI Integrity Guardian](ui-integrity-guardian.md) — verifies that agentic UI components meet design system standards
- [Product Intelligence](product-intelligence.md) — research methods for understanding how users experience agents

## Related packs

- *(none yet — candidate for a "Agentic Product Design" pack)*

## Knowledge Center cross-reference

The conceptual knowledge (research methods for studying human-agent interaction, academic frameworks, case studies) lives in `federico-skills` (Knowledge Center).  
This file documents the **execution capability** — how to apply that knowledge in Federico's product work.

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| 2026-08 | Designing the supervision model for ai-capability-os research cycles | In progress | this repo |

## Notes

- **Agentic design is still a nascent discipline.** There are no established playbooks. The frameworks here are synthesized from current practice (2025-2026), not from a mature body of research.
- **The biggest design mistake:** designing the happy path where the agent always succeeds, and treating failure as an afterthought. Design the failure states first.
- **Trust calibration is the hardest problem.** Users consistently either over-trust AI agents (not checking output) or under-trust them (re-doing everything the agent did). The design must actively support appropriate trust.
- **Federico's unfair advantage:** he supervises AI agents in his own workflow daily. This lived experience gives him intuition about what supervision feels like that most designers don't have. Use it.
