# Priority Skills Shortlist — curado con installs reales

**Fecha:** 2026-08-22  
**Fuentes:** skills.sh / Skillselion (installs reales), contenido SKILL.md verificado por Claude Code  
**Intención Federico:** Producto → Storytelling → UI/UX → Presentaciones/ads → cloud/API después

---

## Top por installs (referencia skills.sh 2026)

| Rank | Skill | Publisher | ~Installs | Alineación con Federico |
|------|-------|-----------|-----------|-------------------------|
| 1 | find-skills | vercel-labs | ~3.1M | Meta: descubrir skills — útil, no es dominio producto |
| 2 | **grill-me** | mattpocock | ~900k | **ADOPT** — sharpening de plan/idea antes de codear |
| 3 | **frontend-design** | anthropics | ~800k | **ADOPT** — UI anti-slop canónico |
| 4 | grill-with-docs | mattpocock | ~800k | STUDY — solapa grill-me; usar si hay docs de producto |
| 5 | improve-codebase-architecture | mattpocock | ~770k | LEARN — ingeniería, no prioritario ahora |
| 6 | tdd | mattpocock | ~740k | LEARN — calidad; después de UI craft |
| 7 | agent-browser | vercel-labs | ~710k | LEARN — verificación / Playwright path |
| 10 | **handoff** | mattpocock | ~650k | **ADOPT** — alinea con coordination/ |
| 12 | **prototype** | mattpocock | ~630k | **ADOPT** — prototipo HTML self-contained |
| — | web-design-guidelines | vercel-labs | ~565k | ADOPT — gate a11y/UX post-generación |
| — | design-taste-frontend / taste | — | ~380k | STUDY — fusionar con frontend-design |
| — | ui-ux-pro-max | — | ~320k | STUDY — decisiones UI/UX amplias |

---

## Los 8 ADOPT canónicos

| # | Skill | URL/Repo | Dominio | Fusiona con | Installs |
|---|-------|----------|---------|-------------|----------|
| 1 | **frontend-design** | [anthropics/claude-code](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md) | UI/UX anti-slop | Reemplaza: impeccable, taste, hallmark | ~800k |
| 2 | **grill-me** | [mattpocock/skills](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md) | Producto — sharpening | Pre-step para user-story-to-spec | ~900k |
| 3 | **prototype** | [mattpocock/skills](https://github.com/mattpocock/skills/tree/main/skills/productivity) | Producto — prototipo | v0-ui-prototyping (diferente: HTML estático vs v0) | ~630k |
| 4 | **handoff** | [mattpocock/skills](https://github.com/mattpocock/skills/tree/main/skills/productivity) | Agentes — coordinación | coordination/HANDOFF.md (mapear reglas) | ~650k |
| 5 | **web-design-guidelines** | vercel-labs | UI — QA/a11y | Con UI Integrity Guardian | ~565k |
| 6 | **Mixpanel deep-research** | [mixpanel/ai-plugins](https://github.com/mixpanel/ai-plugins) | Analytics — investigación | capabilities/mixpanel-skills.md ✓ | oficial |
| 7 | **Mixpanel analyze-report** | [mixpanel/ai-plugins](https://github.com/mixpanel/ai-plugins) | Analytics — lean reading | capabilities/mixpanel-skills.md ✓ | oficial |
| 8 | **gsap-scrolltrigger** | [greensock/gsap-skills](https://github.com/greensock/gsap-skills) | UI — scroll storytelling | design-automation.md | oficial GSAP |

---

## Fusiones aplicadas

| Skills fusionados | Resultado | Razón |
|-------------------|-----------|-------|
| frontend-design + impeccable + taste + hallmark | → **frontend-design** (canonical) | 800k installs, Anthropic oficial, SKILL.md extraído. Los otros no tienen ventaja diferencial verificada. |
| mattpocock/handoff + coordination/HANDOFF.md | → **coordination/ existente** (más completo) | Mapear nombres — no crear paralelo |
| shape (ui-skills) + prototype (mattpocock) | → **prototype** (verificado, ~630k installs) | shape bloqueado, sin contenido verificado |

---

## Flujo integrado de uso

```
grill-me → (idea sharpened)
    ↓
user-story-to-spec → (spec con Gherkin + coverage analysis)
    ↓
frontend-design → (UI no genérica, 2-pass design system)
    ↓
DESIGN.md portfolio → (tokens + guardrails)
    ↓
web-design-guidelines / UI Integrity Guardian → (QA post-generación)
    ↓
Playwright (visual regression) → (no regresiones)
```

---

## STUDY / Segunda oleada

| Skill | Razón de espera |
|-------|----------------|
| ad-creative (borghei) | Sin solapamiento — cuando haya growth real |
| remotion | Video programático — cuando aplique |
| vercel-react-best-practices | Stack React/Next — cuando el portfolio escale |
| gsap-storytelling (ui-skills) | ui-skills bloqueado — investigar fuera de sesión |
| slidev / pptx | Ya en tech-growth-2026.md, Federico tiene skill instalado |

---

## Bloqueados por proxy (anotados, sin acción de Federico)

| Fuente | Estado |
|--------|--------|
| ui-skills.com | Bloqueado — 221 skills, sin acceso en sesión |
| aura.build/skills | Bloqueado |
| mcpmarket.com/tools/skills | Bloqueado — resuelto parcialmente via WebSearch |

*Última actualización: 2026-08-22*
