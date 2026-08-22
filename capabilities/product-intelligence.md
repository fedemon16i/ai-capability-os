# Capability: Product Intelligence

**Domain:** product-intelligence  
**Status:** ADOPT  
**Delegation level:** 4 / 5  
**Score:** 62 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Federico needs to synthesize qualitative research (interviews, support tickets, NPS verbatims), understand product analytics, write PRDs and stakeholder updates, or run competitive intelligence — tasks that currently take 4-6 hours manually and produce lower-quality outputs than AI-assisted alternatives.

## Underlying concept

Product intelligence is the capability to turn raw product signals (user research, analytics, competitive data, team feedback) into structured, actionable insights — faster and at higher quality than manual synthesis.

The AI layer doesn't replace Federico's product judgment. It removes the mechanical work between raw data and insight: transcription, tagging, pattern-finding, draft generation, formatting. Federico still decides what question to ask, which patterns matter, and what to do with the findings.

**The three-layer model:**
1. **Gather** — Perplexity or raw data collection (competitive, market, or research data)
2. **Synthesize** — Claude transforms raw data into structured findings using the 5-part synthesis pattern
3. **Produce** — Claude or Notion AI converts findings into a stakeholder artifact (brief, PRD section, update)

The Ponytail moment: paste 8 user interview transcripts + a synthesis prompt → structured brief with confidence-rated patterns, contradictions, and open questions in 20 minutes. What used to take a full day.

## When to use

- Synthesizing user interview batches (5-10 transcripts per session)
- Writing PRD sections, stakeholder updates, roadmap narratives from bullet-point inputs
- Competitive landscape research before a strategy session
- Weekly competitive monitoring (Visualping alerts + Perplexity follow-up)
- Analyzing NPS verbatims or support ticket themes at scale
- Generating discussion guides for upcoming research sessions

## When NOT to use

**Tasks that must remain Federico's judgment:**
- Prioritization tradeoffs — AI can apply frameworks but not weigh real constraints
- Stakeholder relationship decisions — when/how to escalate, how to frame bad news
- Interpreting weak signals in research — the pause before an answer, the outlier who felt off
- Deciding what question to ask — which metric matters, which assumption to test first
- Hiring and team assessment
- Ethics, compliance, and privacy calls
- Final sign-off on anything customer-facing

## Federico's role

Define the research question. Curate which data to include. Review AI-generated patterns for accuracy. Make the judgment calls on implications. Decide what action to take.

## AI's role

Transcription, tagging, pattern identification (with confidence levels), contradiction mapping, draft generation, document formatting, competitive fact-gathering.

## The 5-Part Synthesis Prompt (implement today, no new tools)

```
You are a senior product researcher helping me synthesize qualitative data.

[Paste 200-word product context: what the product does, current priorities, open hypotheses]

[Paste 5-8 raw transcripts/notes, separated by ---]

Synthesize using five lenses:
1. Recurring patterns — with confidence level (high/medium/low based on independent source count)
2. Contradictions — where sources disagree and what might explain the gap
3. What this confirms vs. challenges about current assumptions
4. What remains unanswered — questions this data raises but doesn't resolve
5. Where evidence is thin — flag any pattern resting on fewer than 2 independent sources

If uncertain, say so explicitly. Do not invent confidence.
```

Follow up: "Draft a 3-paragraph stakeholder brief. Audience: product leadership who didn't see the research. Lead with roadmap implications, not methodology."

## Current best implementation

**Research synthesis:** Claude (with a maintained Project context)  
**Competitive research:** Perplexity Deep Research → Claude for structuring  
**Product analytics:** PostHog (self-serve, no data team required)  
**Competitive monitoring:** Visualping (free tier, 15-minute setup)

## Alternatives considered

| Tool | Why not selected |
|------|-----------------|
| Dovetail | Best-in-class for research repositories. Add when research volume exceeds 2-3 studies/quarter. LEARN. |
| Amplitude | Enterprise-grade, requires mature data infrastructure. Better once PostHog usage is stable. STUDY. |
| Pendo | For in-app onboarding and enterprise-scale NPS. High overhead for current context. STUDY. |
| ChatPRD | Purpose-built PRD tool. Claude with a well-maintained Project is more flexible. REFERENCE. |
| Notion AI | Good for document-layer tasks inside Notion. Not for deep synthesis. LEARN. |
| Klue / Crayon | Enterprise competitive intelligence. Perplexity covers the same territory at fraction of the cost. REFERENCE. |

## Delegation level

**4/5** — Research gathering and synthesis fully delegated. Document drafting fully delegated. Federico retains product judgment, prioritization, and stakeholder relationship calls.

## Ponytail score

**8/10** — The synthesis workflow turns hours of manual work into a 20-minute Claude session. The complexity of pattern-finding, contradiction-mapping, and confidence-rating disappears behind a structured prompt.

## Weekly workflow pattern

**Monday (30 min):** Pull qualitative inputs → run 5-part synthesis → structured brief  
**Tuesday (15 min):** Convert to stakeholder brief → file in Dovetail (when available)  
**Every Monday (10 min):** Review Visualping alerts → Perplexity follow-up on significant changes  
**Monthly (1 hour):** Full competitive brief via Perplexity → structured summary → Notion

## Related capabilities

- [Agent Orchestration](agent-orchestration.md) — for running research sweeps across multiple sources simultaneously
- [Memory MCP](memory-mcp.md) — stores product context, personas, and strategy across sessions
- [AI Coding Agent](ai-coding-agent.md) — for prototyping concepts that emerge from research

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| 2026-08 | AI Capability OS Research Cycle #1 | SUCCESS — 5-domain parallel research, synthesis into capability files | this repo |

## Notes

- **Claude Project**: create a Claude Project pre-loaded with product context, personas, current strategy, and open hypotheses. Reuse across sessions. This is the primary lever — the difference between a generic response and a contextually precise one.
- **Perplexity + Claude combo**: Perplexity gathers and cites facts (5-10 queries/day on free tier). Claude structures, frames, and produces the document. Better output than either alone.
- **PostHog first**: if any product Federico works on can be instrumented, PostHog is the entry point to analytics — free tier, self-serve setup under 2 hours, AI assistant built in.
- **Dovetail timing**: low value at low research volume. Worth setting up when research cadence exceeds 2 studies/quarter — the value compounds as the tagged library grows.
- Research synthesis quality degrades past 10 transcripts per prompt, even with large context windows. Keep batches to 5-8.
