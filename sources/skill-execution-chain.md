# Skill Execution Chain — uso operativo

Cadena única para agentes. **No son 5 capabilities nuevas**: es el orden de trabajo.

Basado en installs reales (skills.sh 2026) + capabilities ya en el repo.
Claude Code ya fusionó craft (impeccable/taste/hallmark) → **frontend-design**.

---

## Cadena canónica

```
1. grill-me          →  afilar problema / plan (antes de codear)
2. prototype OR        →  exploración rápida  OR  spec formal
   user-story-to-spec
3. frontend-design     →  dirección visual anti-slop (Anthropic)
4. DESIGN.md           →  tokens / sistema real del proyecto (portfolio u otro)
5. Implementación      →  React/Next + vercel-react-best-practices si aplica
6. web-design-guidelines + UI Integrity Guardian  →  gate a11y / densidad / roturas
7. Playwright / agent-browser  →  verificación visual (cuando esté instalado)
8. handoff             →  cerrar sesión en coordination/ (AGENT-LOG + HANDOFF)
```

---

## Mapeo a archivos del repo

| Paso | Skill externo | Nuestro archivo |
|------|---------------|-----------------|
| 1 | mattpocock **grill-me** | (skill agente) + product thinking |
| 2a | mattpocock **prototype** | `capabilities/v0-ui-prototyping.md` |
| 2b | — | `capabilities/user-story-to-spec.md` |
| 3 | anthropics **frontend-design** | `capabilities/design-automation.md` (sección skill) |
| 4 | create-design-md (ui-skills) | `federico-portfolio/DESIGN.md` |
| 6 | vercel **web-design-guidelines** | `capabilities/ui-integrity-guardian.md` |
| 7 | agent-browser / Playwright | `capabilities/design-automation.md` |
| 8 | mattpocock **handoff** | `coordination/HANDOFF.md` + AGENT-LOG |

Analytics en paralelo (no bloquean la cadena UI):
- `sources/pendo/` · `capabilities/session-replay.md` · `capabilities/mixpanel-skills.md` · product-intelligence

Presentaciones / ads (bajo demanda):
- Gamma/Marp → `sources/tech-growth-2026.md`
- remotion-best-practices · Ad Creative Engine → STUDY hasta primer uso real

---

## Reglas para el agente

1. **No saltear grill-me** si el pedido es vago (“haceme un dashboard lindo”).
2. **No inventar tokens** si existe DESIGN.md del proyecto.
3. **No instalar** taste + impeccable + frontend-design juntos — uno solo (frontend-design).
4. Al terminar trabajo multi-agente: actualizar coordination, no solo el código.
5. Knowledge Center: no duplicar esta cadena como teoría; acá vive la operación.

---

## Install sugerido (Claude Code / Cursor — lo hace Federico o Claude en máquina)

```bash
# Referencia HANDOFF — no ejecutar desde este chat sin entorno
npx skills add anthropics/claude-code --skill frontend-design
# + grill-me, prototype, handoff (mattpocock/skills)
# Playwright en portfolio cuando toque QA visual
```

*Última actualización: 2026-08-22 — Grok (cadena operativa post-paralelo Claude)*
