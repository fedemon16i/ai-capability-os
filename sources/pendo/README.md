# Pendo — fuentes del ecosistema (MCP Lab / Skills / Use cases)

**Rol:** material oficial y público de Pendo para agentes (Claude, ChatGPT, Cursor).
**No reinventar:** preferir estos recursos sobre prompts inventados.

## Contenido de esta carpeta

| Archivo | Qué contiene |
|---------|----------------|
| [prompts.md](prompts.md) | Prompt Library (~48) + 12 del blog |
| [skills.md](skills.md) | Skills del plugin oficial Cursor + tipos del Lab |
| [use-cases.md](use-cases.md) | Use cases / workflows end-to-end + Agent Analytics |
| [novus-langsmith.md](novus-langsmith.md) | STUDY: Novus — behavioral data → LLM → code fix. LangSmith para observabilidad de agentes |
| [agent-analytics-kpis.md](agent-analytics-kpis.md) | 10 KPIs para medir agentes AI + Agent Analytics producto + benchmarks + ebooks indexados |
| [support-index.md](support-index.md) | Artículos técnicos de support.pendo.io (install, Agent Analytics setup, guides) |

## Separación de repos — regla de oro

> **Este repo = cómo ejecutar con Pendo. `federico-skills` = qué sabe Federico sobre Pendo.**

| Dónde | Qué va |
|-------|--------|
| **Aquí** (`ai-capability-os/sources/pendo/`) | MCP workflows, prompts, patrones de agentes, KPIs de ejecución, implementación técnica |
| **Knowledge** (`federico-skills/knowledge/analytics/`) | Cuándo usar Pendo, patrones de diseño/producto, HEARTS, business case, entrevistas |
| **Capabilities** | Cómo ejecutar (Session Replay, Product Intelligence, Agent Analytics) |

## Ebooks de Pendo — dónde va cada uno

| Ebook | Destino |
|-------|---------|
| 10 essential KPIs para AI agents | `agent-analytics-kpis.md` (acá) |
| How to build user onboarding that boosts retention | `federico-skills/knowledge/ui-patterns/onboarding-and-activation.md` |
| The hidden cost of bad software | `federico-skills/knowledge/analytics/pendo-roi-business-case.md` |
| The CIO's guide to optimizing software spend | `federico-skills/knowledge/analytics/pendo-roi-business-case.md` |
| 10 KPIs for the digital workplace 2025 | `federico-skills/knowledge/analytics/pendo-roi-business-case.md` |
| The 10 KPIs every product leader needs to know | `federico-skills/knowledge/analytics/pendo-patterns.md` |

## MCP vs solo prompts

- **Leer / copiar** prompts y skills documentados → no requiere MCP.
- **Ejecutar** contra datos reales de una cuenta Pendo → sí requiere Pendo MCP + auth.

## Links oficiales

- MCP Lab: https://www.pendo.io/mcp-lab/
- Prompt Library: https://www.pendo.io/mcp-prompt-library/
- Blog 12 prompts: https://www.pendo.io/pendo-blog/mcp-prompts/
- Plugin Cursor: https://github.com/pendo-io/cursor-pendo-plugin
- Connect MCP: docs en support.pendo.io (Claude / ChatGPT / Cursor)

*Última actualización: 2026-08-22*
