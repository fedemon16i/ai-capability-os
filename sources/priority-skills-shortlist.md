# Priority Skills Shortlist — installs reales vs nuestro stack

**Fecha:** 2026-08-22  
**Fuente de adopción:** skills.sh / Skillselion (installs, no solo stars)  
**Intención Federico:** Producto → Storytelling → UI/UX → Presentaciones/ads → cloud/API después

---

## Top global por installs (referencia 2026)

| Rank | Skill | Publisher | ~Installs | Alineación con nosotros |
|------|-------|-----------|-----------|-------------------------|
| 1 | find-skills | vercel-labs | ~3.1M | Meta: descubrir skills — útil, no es dominio producto |
| 2 | **grill-me** | mattpocock | ~900k+ | **ADOPT** — producto antes de codear |
| 3 | **frontend-design** | anthropics | ~800k | **ADOPT** — UI anti-slop canónico |
| 4 | grill-with-docs | mattpocock | ~800k | STUDY — solapa grill-me; usar si hay docs de producto |
| 5 | improve-codebase-architecture | mattpocock | ~770k | LEARN — ingeniería, no prioritario ahora |
| 6 | tdd | mattpocock | ~740k | LEARN — calidad; después de UI craft |
| 7 | agent-browser | vercel-labs | ~710k | LEARN — verificación / Playwright path |
| 8 | setup-matt-pocock-skills | mattpocock | ~680k | Meta bundle |
| 9 | vercel-react-best-practices | vercel-labs | ~650k | ADOPT parcial — Next/React stack |
| 10 | **handoff** | mattpocock | ~650k | **ADOPT** — alinea con coordination/ |
| 11 | triage | mattpocock | ~640k | STUDY |
| 12 | **prototype** | mattpocock | ~630k | **ADOPT** — producto |
| — | web-design-guidelines | vercel-labs | ~565k | ADOPT parcial — gate a11y/UX (no diseño creativo) |
| — | remotion-best-practices | remotion-dev | ~490k | ADOPT cuando video programático |
| — | domain-modeling | mattpocock | ~470k | STUDY producto avanzado |

### Design-specific (ranking design)

| Skill | ~Installs | Rol |
|-------|-----------|-----|
| frontend-design | ~800k | Baseline obligatorio |
| vercel-react-best-practices | ~650k | Perf React/Next |
| web-design-guidelines | ~565k | Audit UX/a11y |
| design-taste-frontend / taste-skill | ~380k | Anti-slop opinionado |
| ui-ux-pro-max | ~320k | Decisiones UI/UX amplias |
| impeccable | (alto en reputación) | Brand mode vs product mode |

---

## Comparación: ecosistema vs lo que YA tenemos

| Necesidad | Ya en ai-capability-os / portfolio | Skill externo top | Acción |
|-----------|-----------------------------------|-------------------|--------|
| UI no genérica | UI Integrity Guardian, DESIGN.md portfolio, design-automation | **frontend-design** | Integrar como skill de referencia obligatorio antes de UI nueva |
| Craft / polish | ui-integrity, design-system-discipline (skills repo) | impeccable / taste | **Fusionar** en un Ponytail “UI craft” (no 3 capabilities) |
| Product discovery | user-story-to-spec, product-intelligence | **grill-me**, **prototype** | Cross-ref + adoptar flujo grill antes de spec |
| Handoff agentes | coordination/, agent-orchestration | **handoff** | Alinear nombres/reglas; no inventar paralelo |
| Analytics product | sources/pendo/, PostHog ADOPT, session-replay | — (Pendo/Mixpanel skills) | Seguir sources/pendo + mixpanel pendiente |
| Presentaciones | tech-growth-2026 (Gamma/Marp) | pptx, slidev, remotion | STUDY → ADOPT al primer deck real |
| Storytelling scroll | — | gsap-scrolltrigger-storytelling (ui-skills) | STUDY alto para portfolio/landing |
| Ads / growth creativo | page-cro listado | Ad Creative Engine (mcpmarket) | STUDY growth |
| Visual QA | design-automation (Playwright) | agent-browser | Playwright install sigue pendiente |

---

## ADOPT ahora (máx 8 — calidad > cantidad)

| # | Skill | Por qué | Cómo entra al sistema |
|---|-------|---------|------------------------|
| 1 | **frontend-design** (anthropics) | #1 design por installs; anti-slop oficial | Referencia en design-automation + DESIGN.md; skill de agente |
| 2 | **grill-me** | #2 global; mata builds en dirección equivocada | Antes de user-story-to-spec / prototipos |
| 3 | **prototype** | Producto rápido con disciplina | Con v0-ui-prototyping / design flow |
| 4 | **handoff** | Ya pensamos coordination; este es el estándar de mercado | Mapear a coordination/HANDOFF |
| 5 | **web-design-guidelines** (Vercel) | Gate a11y/UX post-generación | Con UI Integrity Guardian |
| 6 | **UI craft fusion** (impeccable OR taste, no ambos) | Product mode vs brand mode / dials de taste | Un solo doc capability o skill pack |
| 7 | **vercel-react-best-practices** | Stack Next real | Cuando se toque portfolio/app React |
| 8 | **remotion-best-practices** | Video/changelog cuando haga falta | Con tech-growth video section |

### Explicitamente NO ADOPT en masa

- find-skills (meta; usamos nuestros sources)
- setup-matt-pocock-skills (bundle; preferir skills sueltos)
- 200+ skills de ui-skills.com → solo los de shortlist
- Azure/Lark enterprise skills → fuera de foco
- Cualquier skill “casi igual” a frontend-design sin diferencia clara

---

## Próximo paso de integración

1. Documentar en capabilities o `sources/adopted-skills/` el flujo: **grill-me → prototype/spec → frontend-design → web-design-guidelines → UI Integrity**.
2. Instalar en el agente de trabajo solo esa cadena (Claude Code / Cursor).
3. Playwright + agent-browser cuando Federico desbloquee entorno.
4. Presentaciones: primer uso real con Gamma o pptx skill, no catálogo infinito.

*Última actualización: 2026-08-22*
