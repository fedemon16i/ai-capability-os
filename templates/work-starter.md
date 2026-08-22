# Work Starter — arranque de cualquier trabajo

**Uso:** copiá el bloque de abajo al inicio de un chat (Claude Code, Grok, Cursor, ChatGPT…).  
Completá solo las líneas entre `[ ]`. El resto el agente lo resuelve leyendo repos.

No es un proceso corporativo: es un **atajo inteligente** para no empezar de cero ni alucinar.

---

## Cómo pensarlo (para vos)

Tres situaciones típicas:

| Situación | Qué pegás / adjuntás |
|-----------|----------------------|
| **Ya existe algo** (app, web, pantallas) | Capturas / links / “esto es lo actual” |
| **Hubo algo y lo quieren cambiar** | Antes vs ahora, o “tenían esto” |
| **Desde cero / feature nuevo** | User story, brief, o solo la idea en una frase |

El agente siempre debe: **orientarse → elegir capability/knowledge → proponer plan corto → no codear a lo loco.**

---

## Prompt listo para pegar

```text
Modo: Work Starter (Federico).

Antes de proponer soluciones o codear, hacé esto en orden:

1) CONTEXTO DEL SISTEMA (leé, no inventes)
   - Si tenés acceso a GitHub / repos:
     ai-capability-os: CONTEXT-BRIEF.md → STATUS.md → coordination/HANDOFF.md → coordination/AGENT-LOG.md
     federico-skills: knowledge/_index.md (y lo que aplique al dominio)
   - Si NO tenés acceso: pedime el mínimo (HANDOFF + DESIGN.md del proyecto) y seguí.

2) TIPO DE TRABAJO (elegí uno y confirmá)
   A) Auditar / mejorar lo que YA existe (adjunto imágenes o URLs de lo actual)
   B) Migrar / rediseñar algo que TENÍAN (antes → después)
   C) Feature o producto NUEVO desde cero
   D) Solo research / discovery (sin UI todavía)

3) DATOS DE ESTA TAREA (yo completo)
   Empresa / producto: [ ]
   Qué me pidieron (1–3 frases): [ ]
   Material que adjunto: [ imágenes | Figma | user story | nada ]
   Restricciones: [ tiempo, no tocar X, stack, dark mode, etc. ]
   Definición de “listo”: [ ]

4) ELEGÍ HERRAMIENTAS (del sistema, no inventes 20 skills)
   Cadena por defecto si hay UI:
   grill-me (si el pedido es vago) → user-story-to-spec o prototype →
   frontend-design + DESIGN.md del proyecto → UI Integrity → Playwright (si hay repo con tests)

   Knowledge a consultar según dominio:
   - Research / entrevistas → federico-skills/knowledge/research-methods/
   - Analytics / Pendo / Mixpanel → knowledge/analytics/ + capabilities mixpanel/pendo
   - Design system / consistencia → design-system-discipline + ui-integrity-guardian
   - Agentes / tokens / remote → knowledge/emerging/ + token-efficiency / cloud-compute

5) RESPUESTA QUE ESPERO (corta)
   - 3–5 bullets: qué entendiste
   - Tipo A/B/C/D confirmado
   - Plan en máximo 5 pasos
   - Qué capability/knowledge vas a usar
   - Qué te falta de mi lado (si falta algo)
   - NO empieces a codear hasta que diga “dale” o el plan esté OK

Trabajo de hoy:
[escribí acá en tono normal, como le hablarías a un colega]
```

---

## Atajos aún más cortos

**Solo imágenes de lo actual**
```text
Work Starter tipo A. Estas capturas son el estado actual de [empresa/producto].
Revisá contexto del sistema (HANDOFF + capabilities de UI/DS).
Decime qué está roto o flojo y un plan de 5 pasos. No codees aún.
```

**Feature nuevo**
```text
Work Starter tipo C. Empresa: [ ]. Pedido: [ ].
Pasá por grill-me si hace falta, después plan corto con user-story-to-spec + frontend-design.
No codees hasta que confirme.
```

**“Tenían esto, quieren otra cosa”**
```text
Work Starter tipo B. Antes: [adjunto]. Quieren: [frase].
Compará gaps, proponé migración de UX/DS en pasos, usá knowledge + UI Integrity.
```

---

## Regla de oro

Un solo documento de arranque (este).  
No un skill distinto por empresa.  
El agente **lee** capabilities + knowledge; vos solo contás el caso en criollo.

*Última actualización: 2026-08-22*
