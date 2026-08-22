# Coordination — Canal entre LLMs y Agentes

Este directorio es el canal de comunicación entre cualquier LLM o agente que trabaje en el sistema de Federico.

---

## Reglas de uso

1. **Antes de empezar:** leer HANDOFF.md — puede haber trabajo en curso de otro agente/LLM
2. **Al terminar un bloque de trabajo:** agregar 3–6 líneas en AGENT-LOG.md
3. **Si dejás trabajo para otro:** actualizar HANDOFF.md con exactamente qué falta y qué debe hacer el próximo
4. **Solo hechos y próximos pasos** — nada de explicaciones largas ni justificaciones
5. **Federico / Supervisor cierra los handoffs importantes** — si un handoff requiere decisión de producto, marcarla explícitamente

---

## Archivos

| Archivo | Qué contiene |
|---------|-------------|
| `HANDOFF.md` | Estado actual del trabajo en curso — el próximo agente empieza aquí |
| `AGENT-LOG.md` | Historial de qué hizo cada agente/LLM — cronológico, breve |

---

## Formato de entrada en AGENT-LOG

```markdown
## YYYY-MM-DD — [Agente o LLM]
- Hizo: …
- Resultado: …
- Pendiente / siguiente: …
```

## Formato de HANDOFF

```markdown
## Handoff — YYYY-MM-DD

**Prioridad actual:** …
**En curso:** …
**Próximo agente debe:** …
**Blockers:** …
```
