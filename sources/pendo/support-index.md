# Pendo Support — Índice de artículos clave

**Base:** https://support.pendo.io/hc/en-us  
**Uso:** referencia técnica de implementación; buscar acá antes de googlear

---

## Categorías principales

| Categoría | URL |
|-----------|-----|
| Analytics | support.pendo.io/hc/en-us/categories/… |
| Guides | support.pendo.io/hc/en-us/categories/360001404191-Guides |
| Agent Analytics | support.pendo.io/hc/en-us/articles/41103266988699 |
| Install / SDK | support.pendo.io/hc/en-us/articles/360046272771 |
| Glossary | support.pendo.io/hc/en-us/articles/360034911511-Glossary |

---

## Artículos de alta relevancia para Federico

### Setup e instrumentación
- **Developer's guide — install script:** https://support.pendo.io/hc/en-us/articles/360046272771
  Metadata de visitor y account; configurar el snippet; SPA (React)
- **Configure visitor and account metadata:** https://support.pendo.io/hc/en-us/articles/360031832072
  Cómo enviar metadata desde el install script o SDK

### Agent Analytics (nuevo 2026)
- **Add and configure AI agents:** https://support.pendo.io/hc/en-us/articles/41103266988699
  `Product > Agent Analytics > + Add an agent` — setup completo
  
### Guides
- **Guides overview:** https://support.pendo.io/hc/en-us/articles/27240321140763
  Tipos de guías, use cases, Visual Design Studio
- **What's new in Guides:** https://support.pendo.io/hc/en-us/articles/15375185104283
  Tab Effectiveness → analizar performance de guías (Guides Pro)
- **Deliver guides to visitors opted out of tracking:** https://support.pendo.io/hc/en-us/articles/51431704312603
  Configurar web SDK + cookie settings para usuarios sin tracking

---

## Nota de implementación

El snippet de Pendo requiere `visitorId`. Sin él, no se puede servir guías segmentadas ni trackear interacciones individuales. En SPAs (React, Next.js): inicializar DESPUÉS de que el usuario haga login, y re-llamar en cada cambio de ruta.
