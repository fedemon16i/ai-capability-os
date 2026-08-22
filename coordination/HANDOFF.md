# Handoff — 2026-08-22

**Prioridad actual:** Skills curados e integrados. Flujo de uso documentado. Próximo: instalar skills en Claude Code + Playwright en portfolio.

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
