# Skill Marketplaces (Agent Skills / SKILL.md) — 2026

Índices para descubrir skills reales. **No instalar cientos**: filtrar, evaluar, fusionar.

**Prioridad de dominio para Federico:** Producto → Storytelling → UI/UX → Presentaciones/ads → (después) cloud/storage/API.

---

## Directorios prioritarios

| Fuente | URL | Qué es | Notas |
|--------|-----|--------|-------|
| **UI Skills** | https://www.ui-skills.com/skills | ~221 skills de design engineering | **Alta prioridad UI/UX/motion/storytelling scroll** |
| **Aura Skills** | https://www.aura.build/skills | Skills de diseño web (frontend-design, taste, artifacts) | Anti-slop; Meng To / Anthropic sources |
| **MCP Market Skills** | https://mcpmarket.com/tools/skills | Skills + MCP hub (Claude/ChatGPT/Codex) | Incluye Ad Creative Engine, workflows |
| **MCP Market** | https://mcpmarket.com | Servidores MCP | Cloud, APIs, tools — segunda oleada |
| **SkillsMP** | https://skillsmp.com | Biblioteca masiva SKILL.md | Curar fuerte |
| **Claude Market** | https://www.claudemarket.ai/ | Skills + MCP + CLI search | Install commands |
| **skills.sh (Vercel)** | skills.sh | Ranking por installs reales | Mejor señal de adopción |
| **AtCyrus** | https://www.atcyrus.com/skills | Curado (design, marketing, docs) | Menos ruido |
| **dukelyuu/skills-marketplace** | GitHub | “npm for agent skills” | Multi-IDE |
| **anthropics/skills** | GitHub | Oficiales | frontend-design, skill-creator |
| **Pendo** | `sources/pendo/` | Prompts + skills analytics | Ya catalogado |

---

## Shortlist ADOPT-candidatos (sin duplicar)

### Producto + storytelling
| Skill | Fuente | Por qué |
|-------|--------|--------|
| grill-me / prototype | mattpocock | Afinar producto antes de codear |
| handoff | mattpocock | Handoff agentes (alineado a coordination/) |
| shape | ui-skills | Briefs UX por entrevista estructurada |
| gsap-scrolltrigger-storytelling | ui-skills | Storytelling por scroll |
| better-writing / clarify | ui-skills | Microcopy producto |
| Ad Creative Engine | mcpmarket | Ángulos de ads + test plan (growth) |

### UI / UX (elegir 1 “anti-slop” + 1 motion + 1 layout)
| Skill | Fuente | Nota de fusión |
|-------|--------|----------------|
| **frontend-design** | anthropics / Aura | Canónico anti-generic |
| **impeccable** / taste-skill / hallmark | ui-skills / Aura / AtCyrus | **Fusionar en un solo Ponytail “UI craft”** |
| better-layout / better-typography / polish | ui-skills | Sub-skills del craft |
| landing-page-design / compact-landing / page-cro | ui-skills / AtCyrus | Landing + CRO |
| animation-vocabulary / accessible-animation / page-transition | ui-skills | Motion + a11y |
| create-design-md | ui-skills | Ya tenemos DESIGN.md en portfolio — reforzar |

### Presentaciones / banners / ads
| Skill / tool | Fuente | Uso |
|--------------|--------|-----|
| slidev / slide-wright / frontend-slides | ui-skills | Decks web/dev |
| pptx / ppt-generation | SkillsMP / doc skills | PPT formal |
| Gamma / Tome / Marp | tech-growth-2026.md | Builders de producto |
| remotion | AtCyrus | Video en código |
| Ad Creative Engine | mcpmarket | Publicidades multi-ángulo |

### Cloud / storage / API (segunda oleada)
| Tipo | Dónde buscar |
|------|----------------|
| MCP servers | mcpmarket.com (no skills de UI) |
| PostHog / Pendo MCP | ya documentado |
| Vercel / Cloudflare Workers | flags, edge (tech-growth-2026) |

---

## Regla de adopción

1. **Producto + UI + storytelling primero**; cloud/API después.
2. Preferir installs (skills.sh) o mantenedor serio (Anthropic, ui-skills, mattpocock).
3. Dos skills iguales → **uno** en nuestro sistema.
4. No clonar marketplaces enteros.
5. Inferiores / genéricos / sin evidencia → descartar.

*Última actualización: 2026-08-22*
