# Research Protocol

How to run a research cycle in the AI Capability OS.

---

## When to run a research cycle

- Before adopting a new capability domain
- When an existing tool feels insufficient
- Quarterly review of each domain
- When a new category emerges (new class of AI tools, new MCP patterns, etc.)

---

## Arquitectura supervisada del ciclo

Cada ciclo de research opera con esta estructura de roles:

| Rol en el ciclo | Responsabilidad |
|-----------------|-----------------|
| **Supervisor (Federico + Claude principal)** | Define el brief, asigna dominios a Workers, revisa outputs, acepta o rechaza, hace commits finales, actualiza STATUS.md |
| **Research Worker (agente por dominio)** | Investiga un dominio específico, devuelve output estructurado |
| **Curator Worker** | Compara candidatos de múltiples Workers, elimina ruido, asigna scores |
| **Writer Worker** | Genera los archivos de capability según los templates |
| **Quality Guardian** | Revisa que los outputs cumplan los principios del sistema antes del commit final |

**Regla de oro:** ningún Worker hace commits al repo. El Supervisor valida y escribe.

### Formato de output obligatorio para Research Workers

Todo Research Worker devuelve exactamente este formato. Output fuera de formato → rechazo automático:

```markdown
## Research Output

**Dominio:** [nombre]
**Fecha:** [fecha]
**Status:** COMPLETE | PARTIAL | BLOCKED

### Candidatos descubiertos

| Tool | URL | Score estimado (/80) | Clasificación |
|------|-----|---------------------|---------------|
| | | | |

### Eliminados

| Tool | Razón |
|------|-------|
| | |

### Top picks para Federico

[Top 2-3 con justificación específica a su contexto]

### Conceptos que Federico debe entender

[Solo los conceptos no obvios]

### Qué se puede delegar totalmente

[Lista concreta]

### Gaps / Notas para el Supervisor

[Qué no se pudo investigar, qué quedó ambiguo]
```

### Manejo de errores en el ciclo

| Error | Acción del Supervisor |
|-------|----------------------|
| Rate limit (Worker falla) | Reintentar una vez después del delay. Si falla dos veces → marcar dominio como BLOCKED, continuar con otros, re-agendar |
| Fuente no responde | Worker marca PARTIAL + gap documentado. Supervisor decide si reintentar o marcar el gap |
| Output mal formado | Rechazo automático. Re-enviar con formato explícito |
| Outputs contradictorios | Supervisor resuelve explícitamente — nunca mezclar silenciosamente |
| Fallo parcial de ciclo | Procesar los exitosos. Documentar los fallidos en STATUS.md con fecha de re-intento |

---

## The 11-step cycle

### Step 1 — Define the question

What capability are we researching?  
What problem is it meant to solve?  
What does "good" look like?

Write this down before searching. It prevents scope creep.

### Step 2 — Discover broadly

Search across:
- GitHub (stars, recent activity, topics)
- Official documentation ecosystems
- Known community resources
- Curated directories
- Technical blogs
- Existing capabilities in this OS (check before searching externally)

Do not evaluate yet. Just collect candidates.

Tools available for this step:
- `r.jina.ai/{url}` — clean markdown from any page
- `firecrawl` — crawl full doc sections
- GitHub search API
- Web search

### Step 3 — Deduplicate

Remove:
- Forks that are identical to the original
- Tools that solve exactly the same problem with no differentiation
- Dead projects (last commit > 18 months, no releases)

### Step 4 — Evaluate each candidate

Score against the [Evaluation Framework](EVALUATION-FRAMEWORK.md).

Focus on:
- Does it solve the right problem?
- Is it mature enough to trust?
- Does it integrate with Federico's stack?
- What does the delegation level look like?

### Step 5 — Compare alternatives

For the top 3-5 candidates:
- Side-by-side comparison on key criteria
- Identify the essential tradeoff

### Step 6 — Identify the underlying capability

Even if no tool is adopted, name the capability.  
A capability can exist before its best tool is found.

### Step 7 — Identify what is worth learning

What concept must Federico understand to use this well?  
(Not implement — use.)

### Step 8 — Identify what can be delegated

What execution work can AI fully own?

### Step 9 — Select a default

Pick one tool to adopt as the current default.  
Explain why in one paragraph.

### Step 10 — Test when practical

If the portfolio lab or another real problem is a good test bed:
- run a small test
- document the result in `/experiments/`

### Step 10 — Quality Guardian review

Before committing, the Quality Guardian checks:
- [ ] Each capability file follows the template structure
- [ ] All ADOPT entries have delegation level, score, and Ponytail score filled
- [ ] No capability file is missing "When NOT to use"
- [ ] No tool is adopted without a documented reason for not choosing alternatives
- [ ] Index stats are updated correctly
- [ ] No principles from PRINCIPLES.md are violated

If a violation is found → Worker rewrites the specific section. Max 2 iterations before Supervisor writes manually.

### Step 11 — Document, update STATUS.md, and commit

- Create or update the capability entry in `/capabilities/`
- Create or update the tool entry in `/tools/`
- Archive the research in `/research/{year-month}/`
- Update `capabilities/_index.md` (stats section)
- **Update `STATUS.md`** — mark cycle as complete, list major additions, update priorities
- Supervisor makes the single final commit with all changes

---

## Research cycle document format

File: `/research/{year-month}/{capability-area}.md`

```markdown
# Research: {Capability Area}

**Date:** {date}  
**Trigger:** {why we researched this}  
**Researcher:** {Federico / Claude / agent name}

---

## Question

{What we were trying to answer}

## Candidates discovered

| Tool | URL | Stars | Last updated | Notes |
|------|-----|-------|--------------|-------|
| | | | | |

## Eliminated

| Tool | Reason |
|------|--------|
| | |

## Top candidates evaluated

### {Tool 1}
Score: {total}/50  
Strengths: ...  
Weaknesses: ...

### {Tool 2}
Score: {total}/50  
Strengths: ...  
Weaknesses: ...

## Comparison

{Side-by-side on key dimensions}

## Underlying capability

{Name and description of the capability}

## Selected default

**{Tool}** — {one paragraph justification}

## What Federico needs to understand

{Short explanation of the concept}

## What Federico does NOT need to learn

{Delegated complexity}

## Next steps

- [ ] Create capability entry
- [ ] Create tool entry
- [ ] Run test in portfolio lab
- [ ] Update capability index
```

---

## Source catalog

Sources used for discovery are tracked in [`sources/_catalog.md`](sources/_catalog.md).

This prevents repeating the same searches and builds institutional memory about which sources are reliable.
