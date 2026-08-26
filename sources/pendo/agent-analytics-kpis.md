# Pendo Agent Analytics — KPIs y producto

**Fuente:** pendo.io/product/agent-analytics/ + ebooks de recursos  
**Fecha:** Agosto 2026  
**Relevancia:** Alta — Pendo 2026 pivotó a medir agentes AI; Federico tiene experiencia profunda en Pendo

---

## Qué es Agent Analytics

Producto de Pendo (2026) que conecta datos de interacción con agentes AI al comportamiento tradicional de producto.

> "La única solución diseñada para conectar todos tus datos de software — interacciones AI + comportamiento UI tradicional — para probar que tus agentes mejoran time to value, retención y productividad."

**Setup:** `Product > Agent Analytics > + Add an agent`  
**Doc técnica:** https://support.pendo.io/hc/en-us/articles/41103266988699-Add-and-configure-AI-agents-in-Pendo

---

## Los 10 KPIs esenciales para agentes AI

Fuente: [e-book "10 essential KPIs to prove the value of AI agents"](https://www.pendo.io/essential-kpis-measuring-ai-agent-performance/)

### KPIs de performance del agente
1. **Unsupported requests** — Qué piden los usuarios que el agente no sabe responder → prioriza feature dev y gaps de training
2. **Issue detection rate** — Cuántos problemas detecta el agente (Pendo usa LLM internamente para identificar y sumar ocurrencias)
3. **Task completion rate** — ¿El agente realmente guía al usuario a completar la tarea?
4. **Prompts created** — Volumen y segmentos → adoption curves, power users vs dormant

### KPIs de adopción
5. **AI feature adoption rate** — % de usuarios con acceso que realmente usan el agente
6. **Agent vs traditional workflow** — ¿Los usuarios que usan el agente completan más rápido que los que no?
7. **Abandonment to traditional UI** — ¿Cuándo el usuario abandona el agente y vuelve al click manual?

### KPIs de negocio
8. **Time-to-value comparison** — Agent path vs non-agent path: ¿cuál es más rápido?
9. **Retention impact** — ¿Usuarios que usan el agente retienen más?
10. **Token cost per org** — Gasto real de LLM por cuenta (Pendo lo conecta con LangSmith-style tagging)

---

## Capacidades clave de Agent Analytics

| Capacidad | Qué muestra |
|-----------|-------------|
| Conversation tracking | Qué piden usuarios al agente, cómo responde |
| Top use cases discovery | Qué logran realmente (vs qué diseñaste) — revela si tus prompts al LLM capturaron el intent real |
| Downstream behavior connection | ¿Los que usan el agente convierten/retienen más o menos? |
| Thread view | Conversaciones multi-turn → ¿llegó a resolución? |
| Third-party agents | Sí, puede trackear agentes de terceros que usan tus empleados |

**Benchmarks de adopción (de Pendo data):**
- Companies using Pendo mejoran trial-to-paid conversion 25–40%
- Reducen support tickets en 15% promedio

---

## KPIs para el workplace digital (complementarios)

Fuente: [e-book "10 KPIs for the digital workplace 2025"](https://www.pendo.io/resources/10-kpis-for-the-digital-workplace-2025/)

1. **Workflow productivity** — Tiempo promedio en completar un workflow crítico (baseline para medir impacto de AI)
2. **Process adoption** — % completando workflows clave; superusers como referencia
3. **Support deflection** — Tickets evitados con Resource Center + guides
4. **TCO** — Costo total de ownership de apps; guías reducen tiempo de tarea

---

## KPIs para product leaders (clásicos + AI)

Fuente: [e-book "10 KPIs every product leader needs to know"](https://www.pendo.io/resources/the-10-kpis-every-product-leader-needs-to-know/)

- AI feature adoption rate (% base con acceso que usa el feature AI)
- Product performance (99.9% uptime, <2s para acciones críticas)
- Revenue uplift from personalization
- [Benchmarks interactivos de Pendo](https://www.pendo.io/product-benchmarks/) — 6,800 apps, 2,500 clientes, por región/tamaño/industria

---

## Recursos indexados en pendo.io/resources

| Título | Tipo |
|--------|------|
| 10 essential KPIs to prove the value of AI agents | e-Book (featured) |
| The hidden cost of bad software | e-Book |
| The CIO's guide to optimizing software spend | e-Book |
| How to build user onboarding that boosts retention | e-Book |
| 10 KPIs for the digital workplace 2025 | e-Book |
| The 10 KPIs every product leader needs to know | e-Book |

---

## Conexión con measuring-agentic-experiences.md

Este KPI framework de Pendo es el más concreto disponible para medir experiencias agentic en producción. Complementa lo que está en `knowledge/emerging/measuring-agentic-experiences.md` con:
- Métricas específicas y cómo calcularlas
- Benchmarks reales (25–40% conversion, 15% deflection)
- Una herramienta real (Pendo) vs teoría

**Para Federico en entrevistas:** puede hablar de Agent Analytics como el estado del arte de medición de agentes, con contexto de su experiencia previa en Pendo clásico.
