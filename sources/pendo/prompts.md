# Pendo — Prompts

Fuente: MCP Lab / Prompt Library (~48) + blog oficial.
Texto usable **sin MCP**. Ejecución live **con MCP**.

---

## Del blog (12 MCP prompts) — texto completo

Fuente: https://www.pendo.io/pendo-blog/mcp-prompts/

1. **Board slides** — “Read the [period] board deck's product slides, then propose updates based on product usage from the last quarter.”
2. **MAU / daily usage** — “How many people are using our product today? Has this increased or decreased from last week?”
3. **NPS / sentiment** — “Give me customers leaving poor NPS responses in the #nps channel.”
4. **Eng prioritization** — “Find pages with the greatest usage drops over the last 30 days and attach customer feedback with ARR data. Finally, add relevant Jira tickets.”
5. **Roadmap evidence** — “Show me usage data from Pendo for [feature] over the last quarter. Who's using it most, how often, and what's the retention impact?”
6. **Bugs vs adoption** — “Are there features with high bug counts in Jira but surprisingly strong adoption metrics in Pendo?”
7. **Usage spikes** — “Let's use the Pendo usage investigator to investigate an increase in usage in [nav item / feature].”
8. **Daily summary** — “What happened yesterday?”
9. **Design + behavior** — “Review this Figma design file and give me feedback as [persona], based on their actual behavior in the product.”
10. **QBR / BSR** — “Use the BSR template in Google Drive and fill in all the details for this customer.”
11. **Churn risk** — “Show me customers at risk of churn.” / “Which new customers aren't adopting key features?”
12. **Marketing / launch** — “Show me which [feature set] our beta users engage with most. Then, create a launch brief that summarizes the top use cases and user behaviors.”

---

## De la Prompt Library (muestra verificada públicamente)

Fuente: https://www.pendo.io/mcp-prompt-library/ y https://www.pendo.io/mcp-lab/  
Library anuncia **48** prompts. Carga dinámica; lista parcial extraída:

| Título | Prompt (texto) | Tags típicos |
|--------|----------------|--------------|
| Inactive accounts (14 days) | List all accounts that haven't logged in during the past 14 days. | Account Health, Churn Risk, CS, Revenue |
| Traits of highly engaged accounts | What are the common metadata attributes of our most engaged accounts? | Account Health, Product Adoption, Marketing, Revenue, PM |
| Adoption curves for recent features | Show me the adoption curve for features launched in the last 6 months. | Product Adoption, Feature Usage, PM, Marketing |
| Single-user dependency risk | Identify accounts with single-user dependencies (1 power user, rest inactive). | Churn Risk, Account Health, CS, Revenue |
| Accounts with major user decline | Which accounts have decreased their number of active users by 20%+ this month? | Churn Risk, Account Health, CS, Revenue |
| Feature usage by long-tenured customers | (Library) | Product Adoption |
| Time to multi-feature adoption | How many days does it take new users to adopt 3+ core features? | Onboarding, Product Adoption, PM, CS |
| Weekly active workflow usage | What's the weekly active usage trend for our core workflow events? | Feature Usage |
| Upgrade prompt conversion impact | What's the conversion impact of our upgrade prompt guide? | Conversion, Guides |
| Top enterprise feature adoption | Which enterprise accounts have the highest feature adoption rates in the last 30 days? | Product Adoption, Account Health |
| Feature adoption mobile vs web | How does feature adoption compare across our mobile and web applications? | Product Adoption, Engagement |

> Completar el resto de los 48 cuando un agente pueda scrapear la Lab completa sin bloqueo de proxy.

---

## Uso recomendado

- Copiar al chat / skill del agente como **plantilla**.
- Sustituir placeholders (`[feature]`, `[persona]`, periodo).
- Con MCP conectado: las mismas frases consultan data real.
- Sin MCP: útiles como checklist de preguntas de product analytics.
