# Capability: Mixpanel Analytics Skills

**Domain:** product-intelligence  
**Status:** ADOPT  
**Delegation level:** 4 / 5  
**Score:** 62 / 80  
**Source:** [mixpanel/ai-plugins](https://github.com/mixpanel/ai-plugins) — oficial Mixpanel  
**Last updated:** 2026-08-22

---

## Problem class

Mixpanel tiene datos, pero sacar insights requiere saber qué preguntar y cómo interpretar los resultados. El analítico crea reportes pero no sabe qué anómalos son normales. El PM ve el número pero no sabe si investigar o ignorar.

Estos dos skills encapsulan el proceso completo de lectura e investigación de métricas — de forma estructurada, sin inventar causas que no tienen evidencia.

---

## Los dos skills de alta señal

### 1. analyze-report — lectura lean de reportes

**Ponytail:** cualquier reporte → valor actual + tendencia + anomalías. En una respuesta, sin digresiones.

**Límite explícito:** NO hace root cause a menos que se pida explícitamente. Este límite es intencional — la mayoría del tiempo un reporte no necesita investigación, solo lectura limpia.

**Cuándo usarlo:**
- Abrir un funnel, reporte de retención, o dashboard en Mixpanel
- Necesitar una lectura rápida antes de una reunión
- Validar si hay algo que investigar más profundo (decide si activar deep-research)

**Prompt:**
```
Analiza este reporte de Mixpanel:

[pegar screenshot o datos del reporte]

Dame:
1. Valor actual de la métrica principal
2. Tendencia (subiendo / bajando / estable — en qué período)
3. Anomalías visibles (picos, caídas, outliers)
4. Una frase sobre si esto requiere investigación más profunda

NO hagas root cause analysis a menos que te lo pida explícitamente.
```

---

### 2. deep-research — investigación estructurada de cambios de métrica

**Ponytail:** pregunta sobre un cambio de métrica → investigación 3 fases → respuesta directa + dashboard sugerido + caveats.

**Las 3 fases (en orden):**

**Fase 1 — Scope:** ¿Qué exactamente cambió? ¿En qué período? ¿Cuál es la magnitud? ¿Afecta a todos los usuarios o a un segmento?

**Fase 2 — Validate:** Descartar explicaciones simples antes de investigar. ¿Hubo un problema técnico? ¿Cambió el tracking? ¿Cambió el producto en esa fecha? ¿Hay estacionalidad?

**Fase 3 — Investigate:** Con el scope claro y las explicaciones simples descartadas, profundizar. Segmentaciones, correlaciones, hypotheses priorizadas.

**Regla:** empieza broad, estrecha con evidencia. No saltar a conclusiones antes de validar.

**Cuándo usarlo:**
- Una métrica cayó o subió significativamente
- Un stakeholder pregunta "¿por qué bajó X?"
- Quiero entender qué está causando un cambio antes de tomar una decisión

**Prompt:**
```
Investiga este cambio de métrica usando el protocolo de deep-research:

Métrica: [nombre]
Cambio observado: [X% en el período Y]
Contexto del producto: [qué se lanzó, qué cambió en esa fecha si algo]

Fase 1 — Scope:
- Confirma el período exacto del cambio
- ¿Afecta a todos los usuarios o a un segmento específico?
- ¿Cuál es la magnitud absoluta, no solo porcentual?

Fase 2 — Validate:
- Descarta: problemas técnicos, cambios de tracking, estacionalidad, cambios recientes de producto
- ¿Hay alguna explicación simple que descarte la necesidad de investigar más?

Fase 3 — Investigate:
- Si llegamos acá, propone 2–3 hypotheses priorizadas
- Para cada una: qué dato confirmaría o descartaría la hypothesis
- Sugiere qué dashboard armar para monitorear

Produce: respuesta directa (1 párrafo), hypotheses priorizadas, dashboard sugerido, caveats.
```

---

## Otros skills disponibles en mixpanel/ai-plugins

| Skill | Problema | Cuándo invocar |
|-------|----------|----------------|
| **manage-experiment** | Diseño de experimento: hypothesis, métricas, sizing, interpretación de resultados | Antes de lanzar un A/B test |
| **manage-feature-flags** | Feature gates, rollout strategies, exposure debugging | Al implementar banderas de features |
| **manage-lexicon** | Audita, puntúa, enriquece metadatos de eventos | Cuando el tracking está desordenado |
| **monitor-metrics** | Detección de anomalías + atribución de causa raíz | Setup de alertas automáticas |
| **create-dashboard** | Builds validados + layout narrativo | Crear dashboard para equipo/stakeholders |
| **tracking-implementation** | Guía de implementación de analytics | Al agregar nuevo tracking al producto |

---

## Prerrequisito

Para ejecutar contra datos reales: **Mixpanel MCP** conectado (ver mcps/_catalog.md).  
Sin MCP: los prompts funcionan con datos pegados manualmente (copy/paste de reportes o exports CSV).

---

## Ponytail score

**8/10** — analyze-report: una lectura sin digresiones. deep-research: una pregunta → investigación estructurada 3 fases, ya sabe cómo empezar broad y estrechar.

## Related capabilities

- [Product Intelligence](product-intelligence.md) — síntesis de inteligencia de producto
- [Session Replay](session-replay.md) — para entender el comportamiento a nivel de sesión
- [User Story → Product Spec](user-story-to-spec.md) — los insights de Mixpanel alimentan los requisitos

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| | | | |
