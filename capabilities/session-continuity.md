# Session Continuity Framework

**Status:** Active · **Priority:** High  
**Problem:** Long Claude Code sessions (Playwright, multi-file UI) exhaust context; the model “forgets” installs, baselines, and decisions. Chat history is not a system of record.

---

## Principle

**Structure beats memory.**  
Anything needed after a token wall must already live in the repo.

```
Chat = scratchpad (ephemeral)
Git  = memory (HANDOFF, CHECKPOINT, LOG, CLAUDE.md)
```

---

## File roles

| File | Cadence | Content |
|------|---------|--------|
| `CONTEXT-BRIEF.md` | Rare | Global entry — all LLMs |
| `STATUS.md` | Per phase | Priorities, blockers |
| `coordination/HANDOFF.md` | Every handoff | What next agent must do |
| `coordination/AGENT-LOG.md` | Every agent session close | What was done |
| **`CONTEXT-CHECKPOINT.md`** (per product repo) | Every 15–20 min useful work + each milestone | Live state: goal, done, pending, exact commands, pass/fail |
| `CLAUDE.md` / `CLAUDE-SHORT.md` | Rare | Eternal rules (not live status) |
| `PORTFOLIO-NEW-INSTRUCTIONS.md` | Standing | Scope Chat A vs B |

---

## Checkpoint template (copy into repo root)

```markdown
# CONTEXT-CHECKPOINT

**Updated:** YYYY-MM-DD HH:mm  
**Scope:** Chat A | Chat B | Playwright | Other

## Goal this session
-

## Done
-

## Pending
-

## Commands / evidence
- `npm run serve` → …
- `npm test` → pass/fail + note

## Next agent must
1.
2.

## Do not
-
```

---

## Operating rules

1. **Start:** Recovery prompt → read BRIEF → STATUS → HANDOFF → CHECKPOINT → only then task files.  
2. **During:** Update CHECKPOINT on every milestone (especially before/after Playwright or big refactors).  
3. **End:** AGENT-LOG entry + HANDOFF “next must…”.  
4. **One scope per session** — OS shell ≠ players ≠ pure QA.  
5. **Never** “continue from memory of previous chat.”  
6. Prefer **curated files** over dumping the whole monorepo into context.

---

## Recovery prompt location

Artifacts / Federico: `PROMPT-CLAUDE-RECOVERY-CONTEXT.md`  
Paste when context dies after Playwright or any long run.

---

## Why Playwright triggers amnesia

- Large traces, many files, long tool outputs fill the window  
- Mid-session token stop leaves no automatic write to CHECKPOINT  

**Mitigation:** write CHECKPOINT *before* `npm test`, append result *after*, even if the run fails.

*Last updated: 2026-08-24*
