# Architecture

How the AI Capability OS is structured and why.

---

## Design decisions

### Why capabilities, not tools

Tools are implementations. Capabilities are what you can do.

When Claude is replaced by a better model, the capability (e.g., "code understanding") persists. When Figma changes its API, the capability (e.g., "design-to-code") persists.

Organizing by capability makes the system resilient to tool churn.

### Why Markdown + Git

- Readable by all AI systems without special tooling
- Portable across machines and environments
- Versioned by default
- Diffable — you can see what changed and why
- Works offline
- No proprietary format lock-in

### Why templates

Consistency enables AI to navigate the system predictably.  
Templates also reduce friction — a blank page is the enemy of capture.

### Why separate `/research` from `/capabilities`

Research is raw. Capabilities are curated.  
Research contains 100 candidates. Capabilities contain 3 adopted ones.  
Keeping them separate prevents the system from becoming a junkyard.

---

## Directory map

```
ai-capability-os/
│
├── README.md                    System overview
├── PRINCIPLES.md                Operating constraints
├── FEDERICO.md                  Context about Federico
├── ARCHITECTURE.md              This file
├── CAPABILITY-MODEL.md          Definition of a capability
├── RESEARCH-PROTOCOL.md         How to run research cycles
├── EVALUATION-FRAMEWORK.md      How to score candidates
│
├── capabilities/                The curated library
│   ├── _index.md               Master registry of all capabilities
│   ├── product-intelligence/
│   ├── design-execution/
│   ├── ai-engineering/
│   ├── automation/
│   ├── research/
│   └── software-understanding/
│
├── packs/                       Assembled Capability Packs
│   └── _template.md
│
├── tools/                       Individual tool evaluations
│   └── _template.md
│
├── agents/                      Agent configs and prompts
│   └── _template.md
│
├── mcps/                        MCP server catalog
│   └── _catalog.md
│
├── skills/                      Reusable AI skills and prompts
│   └── _template.md
│
├── workflows/                   Automation
│   ├── n8n/
│   ├── github-actions/
│   └── scripts/
│
├── research/                    Research cycles (raw)
│   └── _template.md
│
├── learning/                    After-action knowledge records
│   └── _template.md
│
├── experiments/                 Real-world tests
│   ├── _template.md
│   └── portfolio-lab/
│
├── decisions/                   Architecture Decision Records
│   └── _template.md
│
├── sources/                     Discovery source configs
│   └── _catalog.md
│
└── templates/                   All blank templates in one place
```

---

## The capability lifecycle

```
DISCOVER → EVALUATE → CLASSIFY → ADOPT → PACK → REUSE
```

### Discover
A research cycle surfaces candidates. Stored in `/research/`.

### Evaluate
Scored against the evaluation framework. Classification assigned.

### Classify
ADOPT / LEARN / STUDY / REFERENCE / IGNORE.  
Only ADOPT items proceed further.

### Adopt
A capability entry is created in `/capabilities/`.  
A tool entry is created in `/tools/` if there's a specific implementation.

### Pack
Related capabilities are assembled into a Capability Pack in `/packs/`.  
A pack includes: capability + tool + agent + workflow + validation method.

### Reuse
The pack is applied to real problems. Results captured in `/learning/`.

---

## The learning loop

```
Real problem
→ agent solves it using a capability
→ capture: what worked, what the capability was, what Federico needs to know
→ update capability entry if needed
→ update pack if needed
→ update learning record
```

Each iteration makes the system smarter.

---

## Capability domains

| Domain | Covers |
|--------|--------|
| `product-intelligence` | Analytics, instrumentation, insight, CRO, experimentation |
| `design-execution` | Design systems, tokens, motion, accessibility, Figma, design-to-code |
| `ai-engineering` | Agents, MCP, RAG, memory, evaluation, orchestration |
| `automation` | n8n, APIs, webhooks, scheduled agents, pipelines |
| `research` | Web research, repo discovery, competitive intelligence, source evaluation |
| `software-understanding` | Frontend, backend, DOM, codebase reading, browser automation |

---

## Supervised Agent Architecture

> **Principio rector:** Buena estructura de información > cantidad de agentes.  
> Un modelo bien dirigido por una estructura clara se convierte en muchos agentes según el contexto que lee.

### Roles

| Rol | Responsabilidad | Permisos |
|-----|-----------------|---------|
| **Supervisor** | Define el brief, asigna tareas, revisa calidad, acepta o rechaza output, actualiza STATUS.md | Único con permiso de escritura final al repo (commits) |
| **Research Worker** | Extrae información de una fuente específica | Solo devuelve output estructurado — no escribe al repo |
| **Curator Worker** | Compara candidatos, elimina ruido, asigna scores según el Evaluation Framework | Solo devuelve output estructurado |
| **Writer Worker** | Escribe el documento final según el template correspondiente | Solo devuelve output estructurado |
| **Quality Guardian** | Revisa que el output cumpla reglas de estructura, principios del sistema, y criterios de aceptación | Puede vetar — si veta, el output vuelve al Worker |

### Regla de oro

**Ningún Worker escribe directamente al repositorio.** Solo el Supervisor hace commits finales después de revisar y aprobar el output de todos los Workers. Un Worker que propone editar un archivo devuelve el contenido propuesto — el Supervisor decide si aplicarlo.

### Formato de output estructurado (obligatorio para Workers)

Todo Worker devuelve output en este formato. Si no lo cumple → rechazo automático por el Supervisor.

```markdown
## Worker Output

**Rol:** [Research / Curator / Writer / Quality Guardian]
**Tarea:** [descripción de la tarea asignada]
**Status:** COMPLETE | PARTIAL | BLOCKED

### Output

[contenido estructurado según la tarea]

### Confidence

[HIGH / MEDIUM / LOW — con razón]

### Gaps / Notas

[qué quedó sin cubrir, qué fue inferido, qué necesita decisión del Supervisor]

### Veto (solo Quality Guardian)

[VETO: razón] o [APPROVE]
```

### Gestión de errores y resiliencia

| Error | Comportamiento del Supervisor |
|-------|------------------------------|
| Rate limit de modelo / API | Esperar el retry-after indicado, reintentar una vez. Si falla dos veces → marcar tarea como BLOCKED en STATUS.md y continuar con otras tareas |
| Fuente que no responde | El Worker marca `Status: PARTIAL`, documenta qué faltó. El Supervisor decide: reintentar con otra fuente o marcar gap |
| Output de Worker mal formado | Rechazo automático. El Supervisor re-envía con el formato de output correcto explícito |
| Fallo parcial en ciclo de research (1 de 5 agentes falla) | Los agentes exitosos se procesan. El dominio fallido se re-agenda para el próximo ciclo o se reintenta inmediatamente si hay contexto disponible |
| Quality Guardian veta el output | El Writer recibe el veto + razón específica y reescribe. Máximo 2 iteraciones — si el tercer intento falla, el Supervisor escribe esa sección manualmente |
| Outputs contradictorios entre Workers | El Supervisor resuelve la contradicción explícitamente. Nunca mezclar silenciosamente — la contradicción se documenta en STATUS.md |

### Cuándo usar agentes vs. cuándo no

**Usar fan-out (paralelo):** cuando las subtareas son independientes y el resultado de una no depende de otra (investigar 5 dominios en paralelo, auditar 6 páginas en paralelo).

**Usar pipeline (secuencial):** cuando cada etapa depende del output de la anterior (discover → curate → write → review).

**No usar agentes:** para tareas de una sola línea, edits quirúrgicos, o cuando Federico puede hacer la tarea más rápido que escribir el brief.

---

## Multi-LLM strategy

This system is model-agnostic by design.

All capabilities are expressed as:
- a description of what the capability does
- what problem it solves
- how to invoke it (prompt, agent, workflow, tool)
- what the output looks like
- how to validate it

Any capable model can use this system as context.  
Claude Code establishes the canonical architecture.  
Other systems adapt to it.

---

## STATUS.md — punto de entrada obligatorio

`STATUS.md` en la raíz es el primer archivo que cualquier agente, modelo, o sesión nueva debe leer.

Contiene: fase actual, últimos cambios, prioridades, trabajo en curso, blockers.

**Regla:** el Supervisor actualiza STATUS.md al inicio y al final de cada ciclo de trabajo. Nunca dejar STATUS.md con información de más de 48 horas sin actualizar.

---

## What this system is NOT

- Not a Wikipedia of AI tools
- Not a course curriculum
- Not a tool collection
- Not a knowledge dump

It is a **decision support system** for knowing what to reach for when a real problem needs solving.
