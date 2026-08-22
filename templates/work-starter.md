# Work Starter — arranque de cualquier trabajo

**Uso:** pegá el prompt al inicio del chat. Marcá **uno o más códigos de escenario** (ej. `UI-3 + AN-1 + DS-2`).  
Completá solo los `[ ]`. El agente lee capabilities + knowledge; vos hablás en criollo.

---

## Menú de escenarios (elegí códigos)

### Entrada de material (qué te dieron)
| Código | Escenario |
|--------|-----------|
| **IN-1** | Solo idea / pedido verbal (sin story, sin ticket) |
| **IN-2** | User story (formal o informal) |
| **IN-3** | Ticket / Jira / Linear (con o sin acceptance criteria) |
| **IN-4** | Capturas / video de lo **actual** |
| **IN-5** | Capturas de lo que **tenían** (legacy) + pedido de cambio |
| **IN-6** | Figma / prototipo existente |
| **IN-7** | Nada de UI: solo users / roles / problemas |
| **IN-8** | Mezcla (story + capturas + “y además mobile”) |

### UI / UX / experiencia
| Código | Escenario |
|--------|-----------|
| **UI-1** | Feature **nuevo** desde cero |
| **UI-2** | Auditar / mejorar lo que ya está en producción |
| **UI-3** | **Modernizar UI** (look viejo → actual, sin cambiar tanto el flujo) |
| **UI-4** | **Modernizar experiencia** (flujos viejos, no solo piel) |
| **UI-5** | Rediseñar flujo completo (onboarding, checkout, etc.) |
| **UI-6** | **Tablas / datos densos** que en desktop van bien → **mobile** (card stack, horizontal scroll controlado, master-detail, filtros, etc.) |
| **UI-7** | Responsive creativo (no solo “apilar columnas”) |
| **UI-8** | Dark mode / theming roto o inexistente |
| **UI-9** | Design system: consistencia, tokens, drift |
| **UI-10** | Migrar de un design system / librería a otro |
| **UI-11** | Accesibilidad / teclado / contraste |
| **UI-12** | Empty states, errores, loading, edge cases |

### Producto / discovery
| Código | Escenario |
|--------|-----------|
| **PR-1** | Clarificar pedido vago (grill-me) |
| **PR-2** | User story → requirements / scenarios / roles (spec) |
| **PR-3** | Priorizar qué construir esta semana |
| **PR-4** | Research / entrevistas / usability (sin codear UI) |
| **PR-5** | Validación rápida 1 día o 2–3 días |

### Analytics / medición
| Código | Escenario |
|--------|-----------|
| **AN-1** | ¿Están en **Pendo / Mixpanel / PostHog / Hotjar / otra**? ¿Qué datos ya existen? |
| **AN-2** | Producto **dice** que tiene funnels/journeys — hay que **pedir** y leer (no inventar métricas) |
| **AN-3** | **No hay** analytics → proponer taxonomía mínima de eventos + tool |
| **AN-4** | Diseñar medición del feature **nuevo** (qué eventos, dónde) |
| **AN-5** | Session replay / heatmaps / “por qué abandonan” |
| **AN-6** | Dashboard o reporte para stakeholders (no solo tracking) |

### Entrega / calidad
| Código | Escenario |
|--------|-----------|
| **QA-1** | Verificar con Playwright / visual / a11y |
| **QA-2** | UI Integrity (tokens, paddings, no romper DS) |
| **QA-3** | Handoff a dev / cierre de sesión de agente |
| **QA-4** | Documentar para producto (spec legible, no solo Figma) |

Podés combinar: `IN-2 + UI-6 + AN-1` = “tengo story, tabla compleja a mobile, y hay que ver qué analytics tienen”.

---

## Mapa rápido: escenario → qué usar del sistema

| Si marcaste… | Capabilities / skills | Knowledge |
|--------------|----------------------|-----------|
| IN-1, PR-1 | grill-me | — |
| IN-2, IN-3, PR-2 | user-story-to-spec | — |
| UI-1, UI-5 | frontend-design, prototype, DESIGN.md | — |
| UI-3, UI-4 | frontend-design, UI Integrity, design-system-discipline | design-system-discipline |
| UI-6, UI-7 | frontend-design + plan responsive (cards, drawers, priority+) | mobile-first-resilience |
| UI-8, UI-9, UI-10 | UI Integrity, design-automation; (gap: Design System Ops formal) | design-system-discipline |
| UI-11 | design-automation (axe), Accessibility | Accessibility-Standards |
| AN-1, AN-2 | mixpanel-skills, product-intelligence, Pendo ADOPT | analytics/* (pendo, mixpanel-hotjar, event-taxonomy, HEARTS) |
| AN-3, AN-4 | product-intelligence + event-taxonomy | analytics/event-taxonomy |
| AN-5 | session-replay | pendo-patterns, behavioral-analytics |
| PR-4, PR-5 | product-intelligence | research-methods/*, product-testing/* |
| QA-1, QA-2, QA-3 | Playwright, UI Integrity, handoff | — |

**Analytics — regla de oro para el agente:**  
1) Preguntar / asumir solo con evidencia: ¿hay tool? ¿acceso?  
2) Si hay tool → **pedir** funnels, journeys, retention (AN-2), no inventar números.  
3) Si no hay → AN-3 (mínimo viable de eventos), no un data warehouse.  
4) Feature nuevo → AN-4 en el mismo plan que la UI.

---

## Prompt listo para pegar

```text
Modo: Work Starter v2 (Federico).

1) CONTEXTO DEL SISTEMA
   Leé si podés: ai-capability-os → CONTEXT-BRIEF → STATUS → coordination/HANDOFF + AGENT-LOG
   federico-skills → knowledge/_index y carpetas que apliquen
   Si no tenés acceso, pedime HANDOFF + lo mínimo del proyecto.

2) ESCENARIOS (códigos que marco yo)
   [ ej. IN-4 + UI-6 + AN-1 + QA-1 ]

3) DATOS DE LA TAREA
   Empresa / producto: [ ]
   Pedido en criollo: [ ]
   Material: [ imágenes / story / ticket / Figma / nada ]
   Analytics que yo sepa: [ Pendo | Mixpanel | PostHog | Hotjar | ninguna | no sé ]
   Acceso a datos de producto: [ sí puedo pedir | no | no sé ]
   Restricciones: [ ]
   Listo = [ ]

4) COMPORTAMIENTO
   - Confirmá los códigos de escenario y qué implica cada uno.
   - Si hay AN-*: primero aclará medición (tool existente vs crear tracking) antes de inventar KPIs.
   - Si hay UI-6/UI-7: proponé 2–3 patrones responsive (no solo stack vertical).
   - Cadena UI por defecto: grill-me (si vago) → spec/prototype → frontend-design + DESIGN.md → UI Integrity → Playwright.
   - Plan máximo 5–7 pasos. NO codear hasta que diga “dale”.

5) RESPUESTA CORTA
   - Qué entendiste
   - Escenarios confirmados
   - Qué capability/knowledge vas a usar
   - Preguntas bloqueantes (máx 3)
   - Plan

Trabajo de hoy:
[texto libre]
```

---

## Ejemplos de combinación

**Tabla monstruo a mobile + no sé si hay Mixpanel**  
`IN-4 + UI-6 + UI-7 + AN-1` → primero qué miden hoy; después patrones de tabla responsive.

**Story sin pantallas, modernizar experiencia**  
`IN-2 + UI-4 + PR-2 + AN-4` → spec + flujos + eventos del feature.

**Capturas viejas, “que se vea 2026”**  
`IN-5 + UI-3 + UI-9 + QA-2`

**Solo me hablaron por Slack**  
`IN-1 + PR-1 + UI-1` → grill-me antes de diseñar.

**Hay Pendo; quieren saber por qué no convierten**  
`AN-1 + AN-2 + AN-5 + PR-4` → datos primero, UI después si hace falta.

---

## Regla de oro

Un starter, muchos **códigos**, no cien skills.  
Vos elegís el combo; el agente enruta a capabilities + knowledge.

*Última actualización: 2026-08-22*
