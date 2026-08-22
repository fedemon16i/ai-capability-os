# Pendo — Use cases & workflows

Casos de uso documentados por Pendo para MCP + agentes (Claude, ChatGPT, Cursor).

---

## 5 formas de usar Pendo MCP (blog oficial)

Fuente: https://www.pendo.io/pendo-blog/how-to-use-mcp/

1. **Preguntar sin salir del flujo** — En Claude/ChatGPT: adopción, métricas, sin abrir el dashboard.
2. **Product data en el editor** — En Cursor: usage, errores por feature, impacto de un release mientras se codea.
3. **Análisis multi-sistema** — Pendo + Jira + Slack + Drive en un solo prompt (priorización, QBR, board).
4. **Decisiones de roadmap con evidencia** — Uso real + feedback + tickets.
5. **CS / churn / onboarding** — Cuentas en riesgo, features no adoptadas, health antes de una call.

---

## Use cases por rol (derivados de prompts + skills)

| Rol | Use cases |
|-----|-----------|
| **C-level / Leadership** | Board updates con data real; MAU/tendencias; narrativa de adopción |
| **Product** | Feature adoption curves; time-to-value; priorizar por drop-offs; roadmap evidence |
| **Engineering** | Páginas con mayor caída de uso + bugs Jira; impacto de release |
| **CS / Revenue** | Inactive accounts; single-user dependency; churn risk; prep de llamada (account-health) |
| **Design / UX** | Feedback de diseño anclado a comportamiento real; session replay |
| **Marketing** | Features más usadas por beta; launch briefs basados en behavior |

---

## Workflows end-to-end (patrón)

1. **Health check pre-call** → skill `account-health` o prompt de churn/engagement → talking points.
2. **Priorización semanal** → drops de uso (Pendo) + feedback + Jira → lista ordenada.
3. **Post-release** → adoption curve feature nueva + errores + session replays de fricción.
4. **Onboarding audit** → time to multi-feature adoption + funnels + guides conversion.
5. **QBR** → template Drive + métricas Pendo de la cuenta → deck rellenado.

---

## Agent Analytics (producto Pendo)

Pendo también mide **agentes AI dentro del producto** (Agent Analytics): conversaciones, insights, skills de setup para Claude Code/Cursor al instrumentar.

Relevante cuando Federico diseñe o audite experiencias agentic (ver Knowledge: Agentic Design / Measuring Agentic Experiences).

---

## Nota de acceso

| Acción | Requisito |
|--------|-----------|
| Leer este catálogo / copiar prompts | Ninguno |
| Correr skill o prompt contra data del cliente | Pendo MCP + auth + permisos de la subscription |
