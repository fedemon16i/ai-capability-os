# Research Cycle Runner — Protocolo + Fuentes

**Propósito:** Correr periódicamente para detectar nuevos skills, tools, y cambios en el ecosistema. Comparar contra lo que ya tenemos y documentar lo que vale la pena adoptar.

**Cuándo correrlo:** Primer lunes de cada mes, o cuando Federico traiga un recurso nuevo.

**Costo estimado:** ~20k tokens por ciclo completo. ~5k si solo se busca una categoría.

---

## Engine recomendado

Usar el skill `/research` de mattpocock como motor:
> "Investiga preguntas contra fuentes primarias confiables"

Combinado con Firecrawl para scraping de fuentes bloqueadas.

**Trigger:** `"corré el research cycle"` en Claude Code → Claude lee este doc + corre /research por categoría.

---

## Sources a monitorear (por categoría)

### Skills y plugins
| Source | URL | Frecuencia | Herramienta |
|--------|-----|------------|-------------|
| emilkowalski/skills | github.com/emilkowalski/skills | Mensual | gh raw README |
| mattpocock/skills | github.com/mattpocock/skills | Mensual | gh raw README |
| anthropics/claude-code plugins | github.com/anthropics/claude-code/plugins | Mensual | gh raw README |
| tasteskill.dev | tasteskill.dev | Mensual | Firecrawl |
| skills.sh | skills.sh | Mensual | Firecrawl |

### Producto y AI
| Source | URL | Frecuencia | Herramienta |
|--------|-----|------------|-------------|
| Pendo blog | pendo.io/pendo-blog | Mensual | Firecrawl search |
| LangChain blog | langchain.com/blog | Mensual | Firecrawl search |
| Anthropic changelog | anthropic.com/changelog | Quincenal | WebFetch |
| Claude Code releases | github.com/anthropics/claude-code/releases | Quincenal | gh |

### Diseño y UI
| Source | URL | Frecuencia | Herramienta |
|--------|-----|------------|-------------|
| emilkowalski (blog/X) | emilkowalski.com | Mensual | Firecrawl |
| Panda CSS changelog | panda-css.com | Trimestral | WebFetch |
| Motion One | motion.dev | Trimestral | WebFetch |

### Newsletters / agregadores (leer manualmente)
| Newsletter | Qué cubre | Frecuencia |
|------------|-----------|------------|
| TLDR AI | Modelos, tools, papers | Diario |
| The Rundown AI | Productos AI, casos de uso | Diario |
| Bytes.dev | Frontend, design systems | Semanal |
| Product Hunt "AI" filter | Launches nuevos | Semanal |
| Ben Tossell / makerpad | No-code + AI workflows | Semanal |

---

## Protocolo paso a paso

### 1. Prep (2 min)
```
Leer ai-capability-os/sources/priority-skills-shortlist.md
Leer ai-capability-os/STATUS.md
→ Saber qué ya tenemos antes de buscar
```

### 2. Scan de sources (paralelo)
Por cada fuente de la tabla de arriba:
- Scrape con Firecrawl o gh raw
- Extraer: nombre, descripción, fecha, installs si disponible
- Flag todo lo que NO está en priority-skills-shortlist.md

### 3. Clasificar novedades
Por cada novedad encontrada:
```
¿Solapa con algo que tenemos? → SKIP (documentar por qué)
¿Directamente útil para Federico hoy? → ADOPT
¿Interesante pero no urgente? → STUDY
¿Stack diferente o fuera de scope? → SKIP
```

### 4. Escribir findings
- Actualizar `priority-skills-shortlist.md` con novedades
- Agregar entrada en `coordination/AGENT-LOG.md`:
  ```
  ## YYYY-MM-DD — Research Cycle #N
  - Fuentes escaneadas: X
  - Novedades encontradas: X
  - ADOPT: [lista]
  - STUDY: [lista]
  - Sin cambios: [lista]
  ```

### 5. Instalar ADOPTs (si hay)
```bash
npx skills add [author/repo] --skill [nombre]
```

---

## Comparación rápida contra lo que tenemos

### Instalado y activo
- `frontend-design` (Anthropic) ✅
- `grill-me` (mattpocock) ✅
- `prototype` (mattpocock) ✅
- `handoff` (mattpocock) ✅
- `animate` (emilkowalski) ✅ — instalado 2026-08-26
- `review-animations` (emilkowalski) ✅ — instalado 2026-08-26
- `improve-animations` (emilkowalski) ✅ — instalado 2026-08-26

### Candidatos ADOPT (siguiente ciclo)
- `research` (mattpocock) — motor de research contra fuentes primarias
- `writing-for-agents` (mattpocock) — escribe skills, AGENTS.md, CLAUDE.md
- `agent-sdk-dev` (Anthropic) — Claude Agent SDK development
- `hookify` (Anthropic) — hooks personalizados para CLAUDE.md enforcement
- `web-design-guidelines` (vercel-labs) — QA de UI post-generación

### STUDY
- `apple-design` (emilkowalski) — overlaps con frontend-design
- `animation-vocabulary` (emilkowalski) — útil para prompts más precisos
- `improve-codebase-architecture` (mattpocock) — ingeniería, post-UI
- `ralph-wiggum` (Anthropic) — loops autónomos, cuando haya más automatización
