# Handoff — 2026-08-22

**Prioridad actual:** Ponytail de ejecución confirmados por research real. Research completado. Próximo: Playwright en portfolio + Pendo MCP Prompt Library.

---

## Estado

- ai-capability-os operativo (capabilities + arquitectura supervisada + CONTEXT-BRIEF + coordination)
- federico-skills (Knowledge Center) en pausa de expansión — base ya útil
- Canal de comunicación entre LLMs activo vía `coordination/`
- **DESIGN.md creado en el portfolio** — cualquier agente lo lee y genera UI consistente con el design system real
- Research de ecosystem completado: 5 ramas, 5 candidatos Ponytail con evidencia real

---

## Hallazgos del research (para que el próximo agente no repita)

| Candidato | URL | Estado |
|-----------|-----|--------|
| DESIGN.md portfolio | `federico-portfolio/DESIGN.md` | **Creado** |
| Pendo MCP Prompt Library | pendo.io/mcp-prompt-library | Federico visita directamente (proxy bloquea en sesión) |
| product-manager-prompts | github.com/deanpeters/product-manager-prompts | STUDY — curar 3–4 prompts para user-story-to-spec.md |
| alirezarezvani/claude-skills (345) | github.com/alirezarezvani/claude-skills | STUDY — filtrar por design/product/QA/handoff |
| Handoff skill oficial | claudedirectory.org/skills/claude-skills-handoff | STUDY — consolidar con sistema coordination existente |

---

## Próximo agente debe

1. **Si es Claude Code:**
   - Instalar Playwright en el portfolio (`npm init playwright@latest`) — es la única tarea de QA desbloqueada
   - Agregar triggers obligatorios en `CLAUDE.md` del portfolio (antes de CSS → `/design-system-discipline`, antes de animación → verificar `--spring`)
   - Curar 3–4 prompts de product-manager-prompts y fusionar con `capabilities/user-story-to-spec.md`

2. **Si es Grok o cualquier LLM sobre Product:**
   - El user story → spec tiene material nuevo en `product-manager-prompts` (deanpeters, 119 assets validados)
   - El Ponytail de product ya está en `capabilities/user-story-to-spec.md` — expandir con las mejores 3 técnicas del repo, no reemplazar

3. **Cualquier LLM nuevo:**
   Leer CONTEXT-BRIEF.md → STATUS.md → coordination/HANDOFF.md → luego el repo del trabajo

---

## Blockers / Debt

| Item | Prioridad |
|------|-----------|
| Playwright install (portfolio) | Alta — desbloqueado ahora |
| Pendo MCP Prompt Library | Alta — Federico visita pendo.io/mcp-prompt-library |
| Memory MCP / GitHub MCP install | Alta (espera setup de Claude Desktop) |
| Curar alirezarezvani/claude-skills | Media |
| Springs.studio / DesignMD MCP | Media — bloqueado por proxy de sesión, investigar fuera |
| Hetzner VM | Media |
| APIs externas, n8n, Lovable test real | Después |
