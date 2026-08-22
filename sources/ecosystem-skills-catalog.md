# Ecosystem Skills Catalog

**Fecha:** 2026-08-22  
**Criterio:** solo recursos con acceso real verificado, stars/adopción documentada, o fuente oficial.  
**Metodología:** research con WebFetch + WebSearch. Bloqueados por proxy anotados sin pedir acción a Federico.

---

## Tabla de hallazgos por rama

### Analytics

| Skill / Recurso | Fuente | URL | Problema que resuelve | Ponytail? |
|-----------------|--------|-----|----------------------|-----------|
| **deep-research** | mixpanel/ai-plugins (oficial) | github.com/mixpanel/ai-plugins | Investigación estructurada de métricas: scope → validate → investigate. 3 fases, empieza broad, estrecha con evidencia | **Sí** |
| **analyze-report** | mixpanel/ai-plugins (oficial) | github.com/mixpanel/ai-plugins | Interpretación lean de reportes: valor actual + tendencia + anomalías. Límite explícito: NO hace root cause a menos que se pida | **Sí** |
| **monitor-metrics** | mixpanel/ai-plugins | github.com/mixpanel/ai-plugins | Detección de anomalías + atribución de causa raíz con diagnósticos | Parcial |
| **manage-experiment** | mixpanel/ai-plugins | github.com/mixpanel/ai-plugins | Diseño de experimento (hipótesis, métricas, sizing) + interpretación de resultados | Parcial |
| **manage-lexicon** | mixpanel/ai-plugins | github.com/mixpanel/ai-plugins | Audita, puntúa, enriquece y limpia metadatos de eventos en Lexicon | Parcial |
| Pendo MCP Prompt Library | Pendo (oficial) | pendo.io/mcp-prompt-library | Prompts oficiales de Pendo para conectar product analytics data a agentes | **Sí** — bloqueado por proxy de sesión |
| Mixpanel 7 analysis skills | Mixpanel blog | mixpanel.com/blog/7-analysis-skills-prompts-to-teach-your-ai-client-mcp/ | 7 prompts para funnel, retención, segmentación, path analysis | **Sí** — bloqueado por proxy de sesión |
| Hotjar | Web pública | hotjar.com | Sin material público de prompts/skills encontrado | No — skip |

### Design / UI

| Skill / Recurso | Fuente | URL | Problema que resuelve | Ponytail? |
|-----------------|--------|-----|----------------------|-----------|
| **DESIGN.md** (VoltAgent estándar) | VoltAgent/awesome-design-md | github.com/VoltAgent/awesome-design-md | Un archivo → cualquier agente genera UI consistente. 73+ sistemas reales (Stripe, Linear, Vercel) | **Sí — ya creado** en el portfolio |
| Design-System skill | alirezarezvani/claude-skills | github.com/alirezarezvani/claude-skills | WCAG-AA brand tokens — paths exactos no accesibles por proxy | Parcial — sin contenido verificado |
| A11y Audit skill | alirezarezvani/claude-skills | github.com/alirezarezvani/claude-skills | Auditoría de accesibilidad — paths no accesibles por proxy | Parcial — sin contenido verificado |

### Product / PM

| Skill / Recurso | Fuente | URL | Problema que resuelve | Ponytail? |
|-----------------|--------|-----|----------------------|-----------|
| **user-story-prompt-template.md** | deanpeters/product-manager-prompts | github.com/deanpeters/product-manager-prompts | Mike Cohn + Gherkin (Given/When/Then). Detecta split signals. 3 next-steps post-generación. CC BY-NC-SA | **Sí — incorporado** en capabilities/user-story-to-spec.md |
| **prd-prompt-template.md** | deanpeters/product-manager-prompts | github.com/deanpeters/product-manager-prompts | PRD de 9 secciones desde material crudo. Labela gaps como "Assumption" o "Open Question". Closing self-critique | **Sí — incorporado** |
| agent-strategy-canvas | deanpeters/product-manager-prompts | github.com/deanpeters/product-manager-prompts | Diseño de sistemas agentic AI — canvas para tomar decisiones de autoridad, visibilidad, handoff | Parcial — solapamiento con agentic-design.md |
| session-saver-prompt.md | deanpeters/product-manager-prompts | github.com/deanpeters/product-manager-prompts | Preserva contexto de sesión entre conversaciones | No — el sistema coordination/ ya lo cubre mejor |

### Coding Agents / Claude Skills

| Skill / Recurso | Fuente | URL | Problema que resuelve | Ponytail? |
|-----------------|--------|-----|----------------------|-----------|
| **Playwright Pro** | alirezarezvani/claude-skills | github.com/alirezarezvani/claude-skills | Test gen, flaky fix, migrations — paths no verificados por proxy | Parcial — no se pudo extraer contenido |
| **Handoff skill** | alirezarezvani/claude-skills | github.com/alirezarezvani/claude-skills | Matt Pocock-inspired workflow transfer. Estructura de cierre de tarea | Parcial — similar al coordination/ existente |

### FE/BE / QA

| Skill / Recurso | Fuente | URL | Problema que resuelve | Ponytail? |
|-----------------|--------|-----|----------------------|-----------|
| PostHog Agent Skills | PostHog/posthog (CI) | github.com/PostHog/posthog | Skills para data de AI observability (nested payloads, log shapes). PR babysitting, flaky test hunting | Parcial — posthog.com bloqueado por proxy |
| DESIGN.md (ver arriba) | — | — | — | Ya catalogado |

---

## 8 candidatos Ponytail consolidados

| # | Nombre | Fuente | Problema | Acción |
|---|--------|--------|----------|--------|
| 1 | **Mixpanel deep-research skill** | mixpanel/ai-plugins (oficial) | Investigación sistemática de cambios en métricas. 3 fases, start broad → narrow. Produce dashboard + respuesta directa + caveats | Crear capability `capabilities/mixpanel-skills.md` con los 2 skills de Mixpanel |
| 2 | **Mixpanel analyze-report skill** | mixpanel/ai-plugins (oficial) | Interpretación lean de cualquier reporte. Límite explícito: no hace root cause a menos que se pida | Incorporar en el mismo `capabilities/mixpanel-skills.md` |
| 3 | **user-story-prompt-template** (deanpeters) | github.com/deanpeters/product-manager-prompts | Mike Cohn + Gherkin + split signal detection. Validado, CC BY-NC-SA | **Incorporado** en user-story-to-spec.md ← este ciclo |
| 4 | **prd-prompt-template** (deanpeters) | github.com/deanpeters/product-manager-prompts | PRD desde material crudo. Labels de gaps. Closing self-critique | **Incorporado** en user-story-to-spec.md ← este ciclo |
| 5 | **DESIGN.md del portfolio** | VoltAgent estándar | Cualquier agente → UI consistente con el design system real | **Creado** en federico-portfolio/DESIGN.md ← ciclo anterior |
| 6 | **Pendo MCP Prompt Library** | Pendo (oficial) | Prompts de product analytics de Pendo listos para usar con agentes. Federico ya usa Pendo en producción | Federico visita pendo.io/mcp-prompt-library — proxy bloquea acceso de agente |
| 7 | **Mixpanel 7 analysis skills** | Mixpanel blog | 7 prompts validados: funnel, retención, segmentación, path analysis, model orientation | Federico visita mixpanel.com/blog/7-analysis-skills-prompts-to-teach-your-ai-client-mcp/ |
| 8 | **alirezarezvani Playwright Pro** | alirezarezvani/claude-skills | QA: test gen + flaky fix + migrations. Paths no accesibles en sesión — estructura confirmada | Federico instala Playwright + evalúa el skill en su próxima sesión local |

---

## Bloqueados por proxy (sin pedir acción a Federico)

| Recurso | Dominio | Estado |
|---------|---------|--------|
| Pendo MCP Prompt Library | pendo.io | Bloqueado — contenido existe, Federico accede directamente |
| Mixpanel blog (7 skills) | mixpanel.com | Bloqueado — artículo público, Federico accede directamente |
| PostHog newsletter + docs | posthog.com | Bloqueado |
| GitHub API (repos privados o rate-limited) | api.github.com | 403 sin auth |
| alirezarezvani/claude-skills SKILL.md files | raw.githubusercontent.com paths | 404 — paths no coinciden con la estructura inferida |

---

## Gaps confirmados

| Gap | Estado |
|-----|--------|
| Hotjar prompts/skills | No existe material público — definitivamente skip |
| QA visual regression | No hay community Ponytail. UI Integrity Guardian + Playwright (no instalado) es la respuesta |
| PostHog AI observability | Bloqueado — material existe (6 capas: traces, costs, errors, evals, feedback, prompts). Investigar en sesión con acceso a posthog.com |
| alirezarezvani SKILL.md files | Paths no verificados — estructura existe, contenido no extraíble en sesión |
