# Capability: Session Replay

**Domain:** design-execution / product-intelligence  
**Status:** ADOPT  
**Delegation level:** 4 / 5  
**Score:** 58 / 80  
**Last updated:** 2026-08-22

---

## Problem class

When Federico needs to understand how a real user interacted with a prototype — what they clicked, where they hesitated, what path they took — without commercial session replay tools (Pendo, FullStory) and without needing a backend or cloud infrastructure.

Also: when the portfolio lab or a research prototype needs behavioural data from test participants, and setting up analytics infrastructure is disproportionate to the task.

## Underlying concept

Session replay is the ability to record a user's interaction with a web prototype (clicks, cursor movement, scrolls, key interactions) and replay it exactly as it happened — or analyze the recorded data for patterns.

For Federico's context, the architecture is intentionally lightweight: all recording happens client-side in the browser (no backend), sessions are stored in `localStorage` or exported as a JSON file, and replay is a self-contained HTML page. No account, no API key, no cloud dependency.

This is the "own it" version of what Pendo and FullStory sell as a service. It gives Federico behavioural data from prototypes without giving away user data to a third party.

**The Ponytail moment:** embed a `<script>` tag in any HTML prototype → session is recorded automatically → replay it in a separate page to watch the exact user journey.

## Architecture

### Recording layer (client-side)

```javascript
// Attach to any prototype
const session = {
  id: crypto.randomUUID(),
  startedAt: new Date().toISOString(),
  url: location.href,
  events: []
};

const record = (type, data) => {
  session.events.push({
    type,
    ts: Date.now(),
    ...data
  });
};

document.addEventListener('click', e => record('click', {
  x: e.clientX, y: e.clientY,
  target: e.target.tagName,
  text: e.target.textContent?.slice(0, 50)
}));

document.addEventListener('mousemove', e => record('mousemove', {
  x: e.clientX, y: e.clientY
}), { passive: true });

document.addEventListener('scroll', () => record('scroll', {
  x: window.scrollX, y: window.scrollY
}), { passive: true });

// Save on unload
window.addEventListener('beforeunload', () => {
  const sessions = JSON.parse(localStorage.getItem('sessions') || '[]');
  sessions.push(session);
  localStorage.setItem('sessions', JSON.stringify(sessions));
});
```

### Storage options

| Option | When to use | Persistence | Privacy |
|--------|------------|-------------|---------|
| `localStorage` | Solo testing, same-device replay | Browser-only | Local only |
| JSON export (`Blob` download) | Multi-device, sharing with colleagues | File-based | Manual transfer |
| Supabase REST API | Multi-participant research, centralized | Cloud | User-controlled |

### Replay layer (self-contained HTML)

A separate `replay.html` page reads the session from `localStorage` or a JSON file and plays back events using:
- A `<canvas>` or absolute-positioned cursor overlay for mouse movement
- CSS highlight injection for click events
- A timeline scrubber for navigation
- Playback speed controls (0.5×, 1×, 2×)

### API integration (future)

When multi-participant research requires centralized session storage, sessions can be POSTed to a Supabase table:

```javascript
// POST session on unload (requires Supabase anon key)
fetch('https://your-project.supabase.co/rest/v1/sessions', {
  method: 'POST',
  headers: {
    'apikey': SUPABASE_ANON_KEY,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(session)
});
```

## Error handling

| Error | Behavior |
|-------|----------|
| `localStorage` full | Rotate: delete the oldest session and retry |
| `beforeunload` blocked | Periodic save every 30s as a fallback |
| Supabase unavailable | Fall back to localStorage silently |
| Corrupt session data | Skip on replay, log warning to console |
| Session interrupted mid-recording | Mark as `incomplete: true`, still save partial data |

## When to use

- User testing sessions on portfolio prototypes (portfolio lab)
- Research prototypes where participant behaviour data is needed
- Validating interaction hypotheses ("do users find the CTA?")
- Debugging UX issues in prototypes before implementing in production
- A/B testing interaction patterns on static HTML pages

## When NOT to use

- Production sites with real users (use a commercial tool with proper consent flows)
- When consent and compliance are requirements (GDPR etc.) — this implementation has no consent UI
- When you need heatmaps aggregated across many sessions (this is single-session replay, not analytics)
- When backend data (form submissions, API calls) is what you need to track — this tracks UI interaction only

## Federico's role

Embed the recording script in the prototype. Run the user session. Review the replay to identify friction points and validate interaction assumptions.

## AI's role

Generate the recording script, replay page, and storage integration. Parse exported session JSON to identify patterns, hesitations (long gaps between events), and dead clicks. Suggest UX changes based on the replay data.

## Current best implementation

**Approach:** Self-contained vanilla JS + localStorage (no dependencies)  
**Status:** Pattern documented — generate with Claude Code on demand, no permanent install needed  
**Supabase integration:** Optional — requires Supabase project + anon key  

## Delegation level

**4/5** — Claude generates the recording + replay code from scratch on demand. Federico embeds it, runs the session, and reviews the replay. No manual JS writing required.

## Ponytail score

**7/10** — Encapsulates the complexity of DOM event capture, session serialization, and replay into a prompt. Federico describes what he wants to track; Claude generates the instrumented prototype.

## Related capabilities

- [Design Automation & Visual QA](design-automation.md) — complementary: Playwright tests automated behavior, session replay captures human behavior
- [Product Intelligence](product-intelligence.md) — the output of replay analysis feeds into research synthesis
- [UI Integrity Guardian](ui-integrity-guardian.md) — the replay may surface UI issues that the guardian should catch preventively

## Related packs

- *(none yet)*

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| | | | |

## Notes

- **Consent:** any deployment with real external users needs a consent banner before recording starts. Add `document.body.innerHTML += '<div id="consent-banner">...</div>'` and gate `startRecording()` behind acceptance.
- **PII risk:** the `target.textContent` capture can accidentally record text from form fields. Filter input events: `if (e.target.tagName === 'INPUT') return;`
- **mousemove throttle:** raw mousemove fires 60+ times/second. Throttle to every 50ms to avoid bloating the session: `if (Date.now() - lastMove < 50) return;`
- **Portfolio lab use case:** embed recording in any prototype built in the portfolio lab, export the session JSON after the test, paste it into Claude for pattern analysis.
