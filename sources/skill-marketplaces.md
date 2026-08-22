# Skill Marketplaces (Agent Skills / SKILL.md) — 2026

Índices para descubrir skills reales (Claude Code, Cursor, Codex, etc.). **No instalar cientos**: filtrar, evaluar, fusionar.

---

## Directorios prioritarios

| Fuente | URL | Qué es | Notas |
|--------|-----|--------|-------|
| **SkillsMP** | https://skillsmp.com / https://skillsmp.com/es/skills | Biblioteca masiva de Agent Skills (SKILL.md) para Claude/Codex | Filtros por categoría/ocupación; escala enorme → curar fuerte |
| **Claude Market** | https://www.claudemarket.ai/ | Skills + MCP + plugins; CLI `npx claudemarket search` | ~4k+ skills; install commands |
| **skills.sh (Vercel)** | skills.sh | Leaderboard por **installs reales** | Mejor señal de adopción que stars |
| **AtCyrus Skills** | https://www.atcyrus.com/skills | Marketplace curado (dev, design, marketing, docs) | Menos ruido; categorías claras |
| **dukelyuu/skills-marketplace** | https://github.com/dukelyuu/skills-marketplace | “npm for agent skills” open source | UI + sync GitHub; multi-IDE |
| **LobeHub Skills** | https://lobehub.com/skills | Agregador grande | CLI install por agente |
| **anthropics/skills** | GitHub Anthropic | Skills de referencia oficiales | frontend-design, skill-creator, etc. |

---

## Skills de alta señal (descubrimiento 2026)

| Skill | Origen típico | Para qué |
|-------|---------------|----------|
| **frontend-design** | anthropics/skills | UI con intención visual, no templates genéricos |
| **ui-ux-pro-max** | SkillsMP / AtCyrus | UI/UX web-móvil, a11y, tipografía, design systems |
| **skill-creator** | anthropics/skills | Crear/evaluar/optimizar skills |
| **vercel-react-best-practices** | vercel-labs | React/Next performance |
| **ppt-generation / pptx** | SkillsMP / docs skills | Presentaciones |
| **handoff** | mattpocock/skills | Handoff entre agentes/sesiones |
| **grill-me / prototype / tdd** | mattpocock/skills | Product thinking + delivery |
| **baseline-ui / shadcn** | AtCyrus | Validar UI Tailwind/shadcn |
| **hallmark / impeccable** | AtCyrus | Anti-slop design, polish UI |
| **page-cro / seo-audit / copywriting** | AtCyrus Marketing | Growth / conversion |
| **remotion** | AtCyrus | Video programático (React) |
| **analytics-tracking** | AtCyrus | Setup analytics |
| **browser-use / agent-browser** | varios | Navegación automatizada |

---

## Mapeo al research Tech & Growth 2026

| Área del prompt | Skills / fuentes a priorizar |
|-----------------|------------------------------|
| Presentation builders | ppt-generation, pptx, Gamma/Tome (tools, no solo skills) |
| UX/UI modes, motion, a11y | ui-ux-pro-max, frontend-design, baseline-ui, hallmark |
| Marketing / growth | page-cro, seo-audit, email-sequence, copywriting, analytics-tracking |
| Video | remotion; tools: Runway/Sora/HeyGen (fuera de SKILL.md) |
| Product features (cmdk, flags) | vercel-react-best-practices; PostHog Flags (capability existente) |

---

## Regla de adopción

1. Preferir skills con **installs** (skills.sh) o mantenedor serio (Anthropic, Vercel, mattpocock).
2. Si dos skills hacen lo mismo → **uno** fusionado en nuestro sistema.
3. Guardar candidatos en `sources/` o capability; no clonar marketplaces enteros.
4. Skills viejos del portfolio sin evidencia → sospechosos hasta revalidar.

*Última actualización: 2026-08-22*
