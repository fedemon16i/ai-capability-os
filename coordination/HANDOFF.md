# Handoff — 2026-08-22

**Prioridad actual:** cerrar detalles menores del sistema de contexto + debt de setup (VM / MCP) cuando Federico decida

---

## Estado

- ai-capability-os operativo (capabilities + arquitectura supervisada + CONTEXT-BRIEF + coordination)
- federico-skills (Knowledge Center) con base sólida; STATUS ya apunta a CONTEXT-BRIEF
- Canal de comunicación entre LLMs activo vía `coordination/`

---

## En curso / reciente

- Grok revisó el sistema de contexto, escribió en AGENT-LOG, actualizó STATUS de federico-skills
- Claude Code ya completó Token Efficiency, Dispatch, Agentic Design, Pendo, cloud-compute

---

## Próximo agente debe

1. **Claude Code (si lee esto):**  
   - Actualizar el footer de STATUS.md para que diga: leer CONTEXT-BRIEF → STATUS → HANDOFF (no solo STATUS → ARCHITECTURE → _index)  
   - Opcional: agregar STATUS.md corto al portfolio apuntando al CONTEXT-BRIEF  
   - No hace falta rehacer capabilities que ya existen

2. **Cualquier LLM nuevo:**  
   Leer CONTEXT-BRIEF.md → STATUS.md → coordination/HANDOFF.md → luego el repo del trabajo

3. **Cuando Federico resuelva setup (VM / Claude Desktop):**  
   Instalar Memory MCP y GitHub MCP según `capabilities/memory-mcp.md`

---

## Blockers / Debt (no tocar hasta que Federico decida)

| Item | Prioridad |
|------|-----------|
| Memory MCP / GitHub MCP install | Alta (espera setup) |
| Hetzner VM | Media |
| STATUS.md en portfolio | Baja |
| Cross-links finos Knowledge ↔ Capabilities | Baja (debt) |
| APIs externas, n8n, Lovable test real | Después |
