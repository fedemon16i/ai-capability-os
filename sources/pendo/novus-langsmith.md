# STUDY: Pendo Novus + LangSmith — Comportamiento de usuario → code fixes

**Status:** STUDY → candidato a ADOPT (patrón, no el producto)  
**Fuente:** https://www.langchain.com/blog/how-pendo-used-langsmith-to-trace-novus-from-user-behavior-to-code-fixes  
**Autor:** Zain Lakhani, Chief AI Officer, Pendo — Julio 2026  
**Relevancia para Federico:** Alta — experiencia directa con Pendo (DollarCity, Chek) + work en agentic systems

---

## Qué es Novus

**Novus** es un product agent de Pendo que detecta problemas de usabilidad en apps en producción, diagnostica la causa raíz, y genera el code fix automáticamente.

- **90%+ success rate** en evals revisados por PMs
- Shipped a producción en días, no meses
- Stack: **Claude Agent SDK** + LangSmith (observabilidad)

---

## Pipeline técnico

```
Usuario instala snippet Novus
        ↓
Clicks + session replays monitoreados en vivo
        ↓
Novus agrega datos de comportamiento
        ↓
AI interpreta → superficie issue accionable
  ej: "3% drop en funnel checkout→order confirmation / 1000 visitas/día"
        ↓
Session replay → root cause (ej: rage clicks)
        ↓
Correlación con archivos de código específicos
        ↓
Genera PR con fix sugerido
```

**Ciclo completo:** behavioral signal → diagnosis → code fix, sin intervención manual de producto o engineering.

---

## Hallazgo clave (de LangSmith traces)

> "El agente elegía product analytics OR código — raramente ambos."

LangSmith detectó esto en producción temprano. La solución: ajuste de prompts para hacer explícito que el valor de Novus viene de **combinar** las dos fuentes. Usar solo una regresa al estado pre-Novus.

**Lección generalizable:** en sistemas multi-contexto, el agente puede tomar shortcuts hacia la fuente más fácil. Los traces de observabilidad lo detectan antes que los usuarios.

---

## Cómo usan LangSmith

| Capacidad | Uso en Novus |
|-----------|--------------|
| Trace tree completo | inputs, outputs, tool calls, subagents, tokens, costo por run |
| Tags por run | `username`, `conversation_id`, `org` → costo por organización |
| Thread view | conversaciones multi-turn → ¿el agente llevó al usuario a una resolución? |
| Feedback scores | señal de cómo aterrizan los outputs en la práctica |
| Design-partner phase | leyeron traces cada mañana → definieron use cases reales sin suposiciones |

---

## Resultados

- **25% menos tiempo** identificando y evaluando nuevos use cases vs productos anteriores
- **60% de problemas de AI detectados por traces** antes de ser detectados por clientes

---

## Conexiones con el sistema de Federico

| Concepto Novus | Paralelo en ai-capability-os / federico-skills |
|----------------|--------------------------------------------------|
| behavioral data → AI → code fix | `capabilities/agentic-design.md` — human + agent loops |
| LangSmith traces en producción | `capabilities/token-efficiency.md` — observabilidad de costo |
| Combinar analytics + código | `knowledge/analytics/pendo-patterns.md` — Pendo como capa de datos |
| Evals PM-reviewed antes de ship | `capabilities/user-story-to-spec.md` — Gherkin + closing self-critique |

---

## Por qué esto importa para Federico

Federico tiene la combinación exacta que hace Novus interesante como referencia:
1. **Experiencia profunda en Pendo** (DollarCity, Chek) → entiende la data que Novus consume
2. **Trabajo en portfolio en agentic systems** → puede narrar este caso con credibilidad
3. **UX + AI** → Novus es el caso real de "AI-native product experience" más documentado de Pendo

**Potencial uso:** como referencia en entrevistas cuando pregunten por AI en producto, o como patrón de arquitectura para instrumentar un agente con observabilidad.
