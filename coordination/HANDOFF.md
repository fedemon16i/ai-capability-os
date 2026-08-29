# Handoff — 2026-08-29

## Trabajo hecho en esta sesión (2026-08-29)

**`federico-os`:**
- `beats.html` — sistema de comentarios estilo Figma implementado (commit `df493b6`) — ver `context/BEATS-LOG.md`
- `context/BEATS-LOG.md` creado — inventario de 47 beats, bug de timing documentado, dos opciones de fix
- `context/ANIMATE-UI.md` creado — stack de animación recomendado, vocabulario estándar de 8 tipos
- `README.md` actualizado con status de beats y DS Projects

**`ai-capability-os`:**
- `capabilities/product-ui-animation.md` creado — capability ADOPT (62/80), vocabulario de animación, herramientas evaluadas
- `sources/ui-animation-resources.md` creado — 9 repos del framework evaluados, 5 libs de animación, 5 técnicas listas para implementar
- `capabilities/_index.md` actualizado — 34 capabilities, 16 ADOPT

**Repos evaluados (research agent — 2026-08-29):**

| Repo | Verdict |
|------|---------|
| extract-design-system | REFERENCE — real CLI, útil para onboarding de clientes |
| stylelift | REFERENCE — concepto correcto, 0 stars, esperar madurez |
| uselayout/app | IGNORE — Next.js + Docker, overkill |
| screenshot-to-design-system | IGNORE — 4 commits, no confiable |
| html-figma / HTML-to-Design | IGNORE — prototipos muertos |
| mimic-ai | REFERENCE — MCP + Figma DS enforcer, no aplica aún |
| story-ui / storysync | IGNORE — Storybook/React dependency |

**Decisión pendiente de Federico:**
- `beats.html` timing fix: Option A (postMessage handshake, 2-3h) vs Option B (beats nativos sin iframes, 6-8h)
- DS Projects page: segunda página en `federico-os` — pendiente de definir scope

---

# Handoff — 2026-08-22

**Prioridad actual:** Skills instalados + Playwright configurado. Próximo: primer run de baselines + explorar skills en tarea real.

---

## Estado

- ai-capability-os operativo (capabilities + arquitectura supervisada + CONTEXT-BRIEF + coordination)
- federico-skills (Knowledge Center) en pausa de expansión — base ya útil
- Canal de comunicación entre LLMs activo vía `coordination/`
- **DESIGN.md creado en el portfolio** — cualquier agente lo lee y genera UI consistente con el design system real

**Sources completados:**
- `sources/pendo/` — prompts, skills, use cases Pendo
- `sources/skill-marketplaces.md` — índices + shortlist
- `sources/tech-growth-2026.md` — Gamma/Tome, density modes, growth, video
- `sources/ecosystem-skills-catalog.md` — Mixpanel/deanpeters research
- `sources/priority-skills-shortlist.md` — 8 ADOPT canónicos con installs reales (skills.sh)

**Capabilities actualizadas este ciclo:**
- `capabilities/mixpanel-skills.md` — creada (deep-research + analyze-report con prompts completos)
- `capabilities/design-automation.md` — expandida con frontend-design skill
- `capabilities/user-story-to-spec.md` — expandida con Gherkin + split signals + closing self-critique

---

## Hallazgos clave (installs 2026)

Top producto/UI alineados a Federico:
1. **grill-me** (~900k) — sharpening de plan antes de codear
2. **frontend-design** anthropics (~800k) — UI anti-slop canónico
3. **handoff** / **prototype** mattpocock (~630–650k)
4. **web-design-guidelines** (Vercel, ~565k) — gate a11y/UX
5. Fusionar impeccable/taste → frontend-design (mismo dominio, mejor señal)

---

## Flujo de uso integrado (para cualquier agente)

```
grill-me → user-story-to-spec → frontend-design → DESIGN.md → web-design-guidelines → Playwright
```

---

## Próximo agente debe

1. **Si es Claude Code:**
   - Instalar: `npx skills add anthropics/claude-code --skill frontend-design`
   - Instalar: grill-me, prototype, handoff de mattpocock
   - Instalar Playwright en el portfolio (`npm init playwright@latest`)
   - Agregar triggers obligatorios en `CLAUDE.md` del portfolio (antes de CSS → `/design-system-discipline`, antes de UI nueva → `/frontend-design`)

2. **Si es Grok o cualquier LLM:**
   - Documentar el flujo grill-me → spec → frontend-design como una cadena de uso (no 5 capabilities separadas)
   - Elegir **un** craft skill (frontend-design ya elegido) — no sumar taste/impeccable si no hay diferencia clara

3. **Cualquier LLM nuevo:**
   Leer CONTEXT-BRIEF.md → STATUS.md → coordination/HANDOFF.md → luego el repo del trabajo

---

## Blockers / Debt

| Item | Prioridad |
|------|-----------|
| Playwright install (portfolio) | Alta — desbloqueado ahora |
| Instalar skills (frontend-design, grill-me, prototype, handoff) | Alta |
| Memory MCP / GitHub MCP install | Alta (espera setup Claude Desktop) |
| gsap-scrolltrigger (ui-skills bloqueado) | Media — investigar fuera de sesión |
| ad-creative (growth) | Media |
| Hetzner VM | Media |
| APIs externas, n8n, Lovable test real | Después |
