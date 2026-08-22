# Handoff — 2026-08-22

**Prioridad actual:** incorporar recomendaciones de Grok (Knowledge Center `federico-skills`) + resolver debt de conexiones

---

## Estado

El sistema ai-capability-os está operativo y completo para esta fase:
- 35+ capabilities documentadas, 15+ ADOPT
- Arquitectura supervisada activa
- Sistema de coordination activo (este archivo)
- CONTEXT-BRIEF.md como punto de entrada global

---

## En curso

- Grok está trabajando en `federico-skills` (Knowledge Center) y va a pasar recomendaciones de alineación
- Federico va a decidir setup de VM (Hetzner vs Oracle Cloud) y Claude Desktop en iPad

---

## Próximo agente debe

1. **Si sos Grok o venís de federico-skills:** leer CONTEXT-BRIEF.md + STATUS.md + capabilities/_index.md. Luego pasarle a Claude Code las diferencias o gaps entre lo que tenés en Knowledge Center y lo que está documentado acá — especialmente en Agentic Design, Token Efficiency, y Research Methods.

2. **Si sos Claude Code y Federico trae recomendaciones de Grok:** incorporar lo que sea relevante sin duplicar. El Knowledge Center (federico-skills) tiene el "qué es" y el "por qué". Este repo tiene el "cómo ejecutarlo con herramientas". Si Grok documentó algo conceptual que falta acá como capability → crear el archivo. Si ya existe → agregar cross-reference.

3. **Si Federico resuelve el setup de Claude Desktop:** instalar Memory MCP primero (`npx @modelcontextprotocol/server-memory`), luego GitHub MCP. Instrucciones completas en `capabilities/memory-mcp.md` y `mcps/_catalog.md`.

---

## Blockers / Debt pendiente

| Item | Qué necesita Federico | Prioridad |
|------|----------------------|-----------|
| Memory MCP | Confirmar si tiene Claude Desktop activo en su máquina | Alta |
| Hetzner VM | Decidir si provisionar o seguir solo con Codespaces | Media |
| Playwright portfolio | `npm init playwright@latest` en el repo del portfolio | Media |
| federico-skills STATUS.md | Verificar que existe y apunta a este CONTEXT-BRIEF | Media |

---

## Lo que NO se toca en el próximo ciclo (hasta que Federico lo decida)

- APIs externas (Supabase, PostHog, Amplitude)
- n8n setup
- Lovable/v0 test real
- Claude Desktop / MCP config (espera confirmación del setup de Federico)
