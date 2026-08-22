# CONTEXT-BRIEF — AI Capability OS

> **Punto de entrada global del sistema.**  
> Cualquier LLM o agente nuevo lee este archivo primero, siempre.

---

## Qué es esto

Un sistema operativo de capacidades para Federico Monroy — Product Manager y orquestador de agentes AI. Organiza qué puede hacer Federico con AI (capabilities), cómo se investigan y adoptan herramientas, y cómo se coordina el trabajo entre múltiples LLMs y agentes.

**Principio rector:** Buena estructura de información > cantidad de agentes. Un modelo bien dirigido por un STATUS + index actualizado necesita menos contexto que un dump del repo entero.

---

## Los tres repos del sistema

| Repo | Rol | STATUS |
|------|-----|--------|
| **`ai-capability-os`** (este) | Capabilities de ejecución, orquestación, Research Protocol, contexto global, coordination | [STATUS.md](STATUS.md) |
| **`federico-skills`** | Knowledge Center — conocimiento de dominio curado (Research Methods, Agentic Design teoría, Analytics, etc.) | STATUS.md en ese repo |
| **Portfolio** (`federico-portfolio`) | Producto público, case studies, design system lab | STATUS.md en ese repo |

**Regla de separación:**  
¿Es sobre cómo ejecutar algo? → `ai-capability-os`  
¿Es conocimiento de dominio que aplica independientemente de la herramienta? → `federico-skills`

---

## Fase actual

**Research Cycle #1:** completo — 5 dominios, 35+ capabilities registradas  
**Framework:** arquitectura supervisada activa (Supervisor / Workers / Quality Guardian)  
**En curso:** sistema de contexto compartido + coordination

---

## Reglas de oro

1. **Leer en orden:** CONTEXT-BRIEF → STATUS.md → coordination/HANDOFF.md → tarea
2. **Supervisor es el único que hace commits finales** — los Workers devuelven output estructurado
3. **No inventar métricas ni clasificaciones** — usar solo el Evaluation Framework documentado
4. **Preferir contexto curado sobre dump** — STATUS + _index + archivo específico, no el repo entero
5. **coordination/ es el canal entre LLMs/agentes** — lo que se necesita handoffear va ahí, no en el chat

---

## Debt actual (no tocar en este ciclo)

| Item | Estado | Prioridad |
|------|--------|-----------|
| Memory MCP | No instalado — espera setup de Federico en Claude Desktop | Alta |
| GitHub MCP | No instalado | Alta |
| Hetzner VM | No provisionada — espera decisión de Federico | Media |
| Playwright (portfolio) | No instalado | Media |
| Claude Desktop (iPad) | No confirmado setup | Media |
| n8n | Pendiente Cycle #2 | Baja |

---

## Para un LLM nuevo: cómo ponerse al día

```
1. Lee este archivo (CONTEXT-BRIEF.md) — ya lo estás haciendo
2. Lee STATUS.md — fase actual, últimos cambios, prioridades
3. Lee coordination/HANDOFF.md — qué hay en curso, qué se necesita hacer
4. Si vas a trabajar en capabilities: lee capabilities/_index.md
5. Lee solo los archivos específicos del task — no el repo entero
```

**No empecés a escribir sin leer los 3 primeros.**  
**No hagas commits — el Supervisor (Claude principal de Federico) los hace.**

---

*Última actualización: 2026-08-22*
