# Pendo — Skills

## Skills del plugin oficial (GitHub)

Repo: https://github.com/pendo-io/cursor-pendo-plugin  
Pensado para **Cursor** (+ flujo con Claude Code / MCP).

| Skill | Descripción |
|-------|-------------|
| **account-health** | Preparar llamada a cliente: engagement, sentiment, feedback |
| **feature-adoption** | Tasas de adopción, power users vs laggards, tendencias |
| **feedback-analysis** | Temas, insights, riesgos desde feedback |
| **session-replay** | Encontrar y surfacear session replays (debug, UX, comportamiento) |

### Cómo se invocan (plugin)

```
/account-health <account-name>
/feature-adoption <feature-name>
/feedback-analysis
/session-replay
```

Requiere autenticar Pendo MCP en el cliente.

### Tools MCP asociadas (plugin)

activityQuery · productEngagementScore · searchEntities · accountQuery · accountMetadataSchema · visitorQuery · sessionReplayList · generate_feedback_topics · get_feedback_insights · get_feedback_items · guideMetrics · segmentList · list_all_applications

---

## MCP Lab: “Skills” + project instructions

La Lab (https://www.pendo.io/mcp-lab/) anuncia:

- **Project instructions** — contexto de proyecto para el agente
- **Skills** — instrucciones reutilizables (además de prompts sueltos)
- **End-to-end workflows** — ver use-cases.md

Soportados explícitamente en UI: **Claude · ChatGPT · Cursor**.

Detalle fino de cada “Skill” del Lab es dinámico en la web; el plugin de Cursor es la fuente **estable y versionada en GitHub** prioritaria para nuestro catálogo.

---

## Relación con nuestros capabilities

| Skill Pendo | Capability / área en ai-capability-os |
|-------------|--------------------------------------|
| session-replay | `capabilities/session-replay.md` |
| feature-adoption / account-health | `capabilities/product-intelligence.md` |
| feedback-analysis | Product intelligence + research methods (Knowledge) |

No duplicar: referenciar este archivo desde capabilities cuando se implemente ejecución.
