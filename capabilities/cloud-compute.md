# Capability: Cloud Compute for Agents

**Domain:** ai-engineering  
**Status:** ADOPT  
**Delegation level:** 3 / 5  
**Score:** 56 / 80  
**Last updated:** 2026-08-22

---

## Problem class

Cuando Federico necesita ejecutar agentes de forma persistente (Claude Code, scripts, tareas long-running) sin depender de la máquina local ni de sesiones que expiran. Especialmente relevante dado el setup iPad + Codespaces, donde las sesiones mueren y no hay máquina local confiable siempre disponible.

## Opción recomendada

### Hetzner CX32 — ~$8/mes (ADOPT)

| Spec | Valor |
|------|-------|
| CPU | 4 vCPU (Intel) |
| RAM | 8 GB |
| Storage | 80 GB NVMe SSD |
| Bandwidth | 20 TB/mes |
| OS | Ubuntu 22.04 LTS |

**Por qué Hetzner:**
- Mejor relación precio/performance del mercado en 2026
- 20 TB de bandwidth a $8/mes (DigitalOcean cobra $18 por 2 GB RAM)
- Siempre encendida — sin idle timeout, sin spin-down
- CPUs dedicadas, no compartidas
- Setup en 30 minutos

**Setup básico para agentes:**
```bash
# 1. Instalar Node.js + Claude Code
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
npm install -g @anthropic-ai/claude-code

# 2. Guardar el API key
echo 'export ANTHROPIC_API_KEY="tu_key_aqui"' >> ~/.bashrc
source ~/.bashrc

# 3. Usar tmux para sesiones persistentes
sudo apt install -y tmux
tmux new -s agents  # crear sesión
# ... correr Claude Code acá ...
# Ctrl+B, D para dejar la sesión corriendo
# Reconectar desde iPad: tmux attach -t agents
```

## Opciones gratuitas

### Oracle Cloud Free Tier (LEARN — si conseguís cuenta)

**Specs (post-agosto 2026, Oracle redujo el tier):**
- 2 OCPU + 12 GB RAM ARM (Ampere) — pool compartible en instancias
- 2 instancias AMD x86 micro adicionales
- 200 GB block storage, 10 TB bandwidth/mes

**Caveat crítico:** Oracle silenciosamente rechaza muchos registros nuevos (detección de fraude agresiva). Si ya tenés cuenta Oracle — usala. Si no, no cuentes con conseguirla.

**Nota de agosto 2026:** Oracle acaba de reducir el tier de 4 OCPU/24 GB a 2 OCPU/12 GB. Las instancias más grandes fueron terminadas automáticamente.

### Google Cloud e2-micro (REFERENCE — demasiado pequeño)

- 1 GB RAM, shared vCPU, 30 GB storage
- Truly always-free sin expiración
- 1 GB RAM no alcanza para Claude Code + dependencias bajo carga real
- Útil como coordinador lightweight o receptor de webhooks

### AWS t2.micro (REFERENCE — time-limited)

- 750 horas/mes por 12 meses, después se cobra
- 1 GB RAM — misma limitación que GCP
- No relevante para setup permanente

## Acceso desde iPad

**App recomendada: Blink Shell** ($19.99/año)
- Mosh nativo (resiste cambios de red, backgrounding, sleep del iPad)
- Mejor experiencia de teclado en iPad
- Integración con VS Code server

**Alternativa gratuita: Termius** (tier free disponible)
- Sincroniza hosts entre dispositivos
- Bueno para manejar múltiples servidores

**Workflow desde iPad:**
```
iPad → Blink Shell / Termius → SSH a Hetzner VM → tmux → Claude Code
```

tmux es la clave: si se cae la conexión del iPad, la sesión del agente sigue corriendo. Al reconectar: `tmux attach`.

## Codespaces vs VM dedicada

| | Codespaces | Hetzner CX32 |
|---|---|---|
| **Free** | 120 core-hours/mes (~60h en 2-core) | Ninguno (pago desde día 1) |
| **Siempre encendida** | No (muere a los 30min idle) | Sí |
| **Costo mensual** | Gratis hasta límite, $0.18/hr después | ~$8/mes flat |
| **Setup** | Cero | ~30 min |
| **Acceso iPad** | Browser | SSH via Blink/Termius |
| **Agentes persistentes** | No | Sí (tmux) |
| **Mejor para** | Coding sessions por repo | Agentes long-running |

**Setup ideal:**
- **Codespaces** → trabajo de código por proyecto (VS Code + GitHub integration, ya en el workflow)
- **Hetzner CX32** → host de agentes persistentes, tareas long-running, cron jobs

## Claude Code 24/7 en VPS

Claude Code puede correr indefinidamente en una VPS con tmux. El costo real es el API key de Anthropic (por tokens consumidos), no el server.

Característica relevante: **Claude Remote Control** (lanzada en 2026) permite interactuar con una instancia de Claude Code via API calls sin tener un terminal abierto — podés triggear y monitorear agentes sin mantener la conexión SSH activa.

## Configuración mínima viable

Para agent workloads de Claude Code: **2 vCPU, 4 GB RAM mínimo**.
- Hetzner CPX11 (2 vCPU, 2 GB) — $5/mes, funciona pero justo con múltiples tools simultáneos
- Hetzner CX32 (4 vCPU, 8 GB) — $8/mes, cómodo sin ansiedad de recursos

## Dispatch Mode — trabajar sin estar presente

Dispatch mode es el patrón de trabajo donde Federico manda un brief claro a un agente que corre en una máquina remota y revisa los resultados después — sin monitorear el proceso en tiempo real.

### Cuándo usar Dispatch Mode

- Tareas largas (>30 min) que no requieren decisiones intermedias
- Research cycles completos
- Audits o sweeps sobre múltiples archivos
- Cualquier task donde el output final es más importante que el proceso paso a paso

### Requisitos de diseño para runs desatendidos

| Requisito | Por qué |
|-----------|---------|
| **Brief completo y sin ambigüedad** | El agente no puede preguntar — si el brief es ambiguo, el agente asume o se bloquea |
| **Output estructurado obligatorio** | El agente escribe el resultado en GitHub, un archivo, o un formato parseable — no en stdout que nadie ve |
| **Error handling explícito** | El agente documenta lo que falló y por qué, en vez de fallar silenciosamente |
| **Límites de tokens / steps** | Sin un bound, un agente desatendido puede consumir todos los tokens disponibles |
| **Commit al finalizar** | El resultado debe sobrevivir al final de la sesión — push a GitHub o export a archivo |

### Opciones de Dispatch Mode en 2026

| Opción | Cómo funciona | Costo | Estado |
|--------|--------------|-------|--------|
| **Claude Code en VPS (SSH + tmux)** | Federico SSH-ea, lanza el task, cierra el iPad — el agente sigue en tmux | $8/mes (Hetzner) | Funciona hoy |
| **Claude Code Remote Control** | Triggerear y monitorear agentes via API sin terminal abierta | Incluido en API | Disponible desde 2026 |
| **Claude Code web sessions** | Sessions en la nube de Anthropic, no requiere VPS propio | Incluido en plan | Activo (pero expiran por inactividad) |
| **Grok Build headless** | Grok corriendo en un cloud computer persistente | Según plan | Según lo que Grok ofrezca |

### Template de brief para Dispatch Mode

```markdown
# Dispatch Brief — [nombre del task]

**Objetivo:** [qué tiene que hacer el agente, específico]
**Output esperado:** [dónde escribe el resultado — archivo, commit, PR]
**Formato de output:** [JSON / Markdown / capability file / etc.]
**Límites:**
- Máximo steps: [N]
- Si bloqueado: documentar el bloqueo en [archivo] y terminar limpio
- No preguntar al humano — asumir [X] si ambiguo
**Criterio de éxito:** [cómo sabe el agente que terminó correctamente]
**Contexto mínimo:** [qué archivos leer — STATUS.md + los específicos, no el repo entero]
```

### Disciplina de tokens en runs desatendidos

Los runs desatendidos son donde el token waste es más costoso — nadie está mirando para cortar un loop infinito. Aplicar siempre:
- Bound explícito en steps y retries
- Output estructurado (schema JSON) en vez de texto libre
- El agente escribe `STATUS: COMPLETE | PARTIAL | BLOCKED` al final del output
- Si hay budget object disponible: monitorear `budget.remaining()` en cada iteración

Ver [Token Efficiency](token-efficiency.md) para el detalle completo.

---

## Delegation level

**3/5** — Federico provisiona el servidor (30 min, una vez). Claude Code genera los scripts de setup y configuración. Las tareas que corren en el server son completamente delegadas.

## Ponytail score

**6/10** — El server en sí es infraestructura, no una abstracción. El Ponytail viene de lo que corre encima: Claude Code + tmux + el API key = agentes que trabajan mientras Federico duerme.

## Related capabilities

- [AI Coding Agent](ai-coding-agent.md) — el agente que corre en este compute
- [Agent Orchestration](agent-orchestration.md) — los patrones que se ejecutan sobre el server
- [Memory MCP](memory-mcp.md) — persistent memory que se instala en esta máquina

## Learning records

| Date | Problem | Outcome | Link |
|------|---------|---------|------|
| 2026-08 | Investigación de opciones para iPad + agentes persistentes | Research completo | este repo |

## Notes

- **Bandwidth**: 20 TB/mes en Hetzner es prácticamente ilimitado para uso normal de agentes. No hay sorpresas de facturación.
- **Región**: Hetzner tiene data centers en Alemania y Finlandia. Latencia desde LATAM: ~150ms — fine para SSH y agent workloads, no para APIs de baja latencia serving end users.
- **Backups**: Hetzner cobra extra por backups automáticos (20% del precio de la instancia). Para un server de agentes, hacer `git push` al finalizar una sesión es suficiente backup.
- **Oracle actualmente**: si creás cuenta hoy, las probabilidades de aprobación son bajas. No pongas el plan de trabajo en esto.
- **Siguiente paso**: si se decide por Hetzner, el setup completo (provisionar + instalar Node + Claude Code + tmux + SSH key para iPad) es una tarea delegable a Claude Code en ~30 minutos.
