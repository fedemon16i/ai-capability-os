# Pattern: AutoResearch (karpathy) — STUDY

**Fuente:** karpathy/autoresearch  
**Status:** STUDY — el patrón aplica, el tooling ML no (requiere GPU)  
**Fecha:** 2026-08-22

---

## Qué es

AutoResearch es un loop de investigación autónoma con métricas de verdad:

```
idea → editar → medir contra benchmark real → keep / discard
```

La clave: un `program.md` que define la hipótesis y el benchmark. El agente itera libremente, pero cada iteración se evalúa contra una métrica objetiva — no contra "me parece bien".

**Lo que lo hace diferente:** no es un loop de generación libre. Es un loop con un **árbitro externo** (métrica) que decide qué iteraciones sobreviven.

---

## Por qué importa para Federico (PM / producto / UI)

El patrón ML de karpathy tiene un equivalente directo en product/UI:

| ML (karpathy) | Product / UI (Federico) |
|---------------|------------------------|
| `program.md` = hipótesis + benchmark | User story + métrica de éxito clara |
| Editar modelo | Cambiar feature / UI / copy |
| Medir accuracy | Medir conversión / task completion / tiempo en página |
| Keep / discard | Lanzar / revertir |

**El error sin este patrón:** iterar sin árbitro → cada iteración "mejora" subjetivamente → no hay evidencia real de progreso.

---

## Aplicación concreta (sin GPU)

### Para product experiments
```
1. Definir: hipótesis + métrica que decide (task completion rate, clicks, tiempo)
2. Crear: branch de experimento con el cambio
3. Medir: PostHog / Pendo contra el baseline
4. Decidir: keep (merge) o discard (revert) — sin opinión subjetiva
```

### Para UI iterations
```
1. Definir: criterio de mejora visible (Lighthouse score, a11y violations, visual regression pass/fail)
2. Iterar: Claude Code propone el cambio
3. Árbitro: `npm test` — Playwright decide si hay regresiones
4. Keep: si pasa los tests + criterio. Discard: si falla.
```

**El Playwright de este portfolio ES el árbitro.** Los tests son el `program.md` del loop visual.

---

## Cuándo aplicar este patrón

- Antes de iterar en UI sin una métrica clara → definir el árbitro primero
- Cualquier "hacelo más lindo" sin criterio objetivable → convertirlo a "el árbitro es X"
- Experimentos A/B: definir la métrica que gana antes de correr el experimento

## Cuándo NO aplicar

- En tareas con output claro (agregar un campo, arreglar un bug) — el árbitro es "funciona o no"
- No correr el loop ML completo sin GPU — requiere hardware que no tenemos

---

## Referencia

- [karpathy/autoresearch](https://github.com/karpathy/autoresearch)
- Concepto central: `program.md` como benchmark fijo + loop edit→measure→keep/discard
