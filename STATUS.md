# Current Status — AI Capability OS

**Última actualización:** 2026-08-22  
**Fase actual:** Framework Update completo → Alineación con Knowledge Center en curso  
**Research Cycle activo:** ninguno (Cycle #1 cerrado; Cycle #2 pendiente de definir)

---

## Estado general

- Sistema operativo y pusheado a GitHub (`fedemon16i/ai-capability-os`)
- Research Cycle #1 completado: 5 dominios cubiertos, 33 capabilities registradas, 12 archivos de capability escritos
- Framework Update completado: STATUS.md, arquitectura supervisada, RESEARCH-PROTOCOL.md, 3 nuevas capabilities
- Alineación con `federico-skills` (Knowledge Center) documentada en ARCHITECTURE.md

---

## Últimos cambios importantes (más recientes primero)

- 2026-08-22: Token Efficiency capability — 7 técnicas de alto impacto (caching, model routing, bound loops, MCP pruning, output schema, context curado)
- 2026-08-22: Dispatch Mode documentado en cloud-compute.md — template de brief para runs desatendidos
- 2026-08-22: Agentic Design capability — 4 design questions, measurement framework, progressive autonomy

- 2026-08-22: Framework Update — STATUS.md, Supervisor/Workers/QG architecture, error handling, Session Replay, UI Integrity Guardian, User Story → Spec
- 2026-08-22: Agentic Design capability creada — diseño de productos con humanos + agentes
- 2026-08-22: Separación de repos documentada en ARCHITECTURE.md (capabilities de ejecución acá, knowledge de dominio en `federico-skills`)
- 2026-08-22: Pendo reclasificado de STUDY → ADOPT (contexto: Federico tiene experiencia profunda en DollarCity + Chek)
- 2026-08-22: Research Cycle #1 — 29 capabilities iniciales

---

## Prioridades actuales

1. **Instalar Memory MCP en la máquina de Federico** — primer ADOPT sin acción real todavía. Espera definición de setup (iPad + VM vs Codespaces)
2. **Investigación de VMs** — en curso (agente corriendo: opciones gratis y baratas para iPadOS + agentes long-running)
3. **Knowledge Center en `federico-skills`** — trabajo paralelo con Grok; este repo y ese son complementarios
4. **Cycle #2 candidatos:** n8n deep dive, Playwright setup en portfolio, Lovable test en prototipo real

---

## Trabajo en curso

- VM research (agente en background): Oracle Cloud, Hetzner, Codespaces, opciones iPad-accesibles
- Alineación entre `ai-capability-os` y `federico-skills` — la separación está documentada; la implementación del Knowledge Center sigue en `federico-skills`

---

## Repos del sistema

| Repo | Contenido | URL |
|------|-----------|-----|
| `ai-capability-os` (este) | Capabilities de ejecución, herramientas, orquestación, Research Protocol | github.com/fedemon16i/ai-capability-os |
| `federico-skills` | Knowledge Center — conocimiento de dominio curado (Research Methods, Analytics, Agentic Design teoría, etc.) | github.com/fedemon16i/federico-skills |

---

## Blockers / Notas

- Memory MCP y GitHub MCP no instalados — Federico trabaja desde iPad, necesita definir el setup de acceso antes de instalar
- MCP en Claude Desktop: Federico no lo tiene activo todavía — pendiente de resolver el setup de acceso
- VM research en curso — el resultado informará si conviene un servidor dedicado para agentes o seguir con Codespaces

---

> **Para cualquier agente que lea esto:** leé STATUS.md → ARCHITECTURE.md → capabilities/_index.md en ese orden. No escribas al repo sin leer estos tres primero. El Supervisor es el único que hace commits finales.
