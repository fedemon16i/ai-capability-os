# Karpathy Autoresearch — patrón (no el pipeline ML completo)

**Repo:** https://github.com/karpathy/autoresearch  
**Estado en nuestro stack:** STUDY → aplicar el *patrón* a producto/UI; no correr training GPU salvo proyecto ML explícito.

---

## Qué es

Loop autónomo de investigación:

1. Agente lee **`program.md`** (instrucciones humanas — el “real benchmark”).
2. Edita **un solo archivo** permitido (en el original: `train.py`).
3. Corre experimento con **presupuesto fijo** (ej. 5 min).
4. Mide **una métrica** (ej. val_bpb).
5. Si mejora → **commit**; si no → **rollback**.
6. Repite (overnight ~100 runs; multi-día ~700).

El humano **no** edita el código de entrenamiento día a día: itera el markdown que programa al agente.

---

## Por qué importa para Federico

| Idea Karpathy | Equivalente en AI Capability OS |
|---------------|----------------------------------|
| `program.md` como contrato de research | CONTEXT-BRIEF + HANDOFF + skills |
| Un scope editable | Un archivo / una pantalla / un capability |
| Métrica ratchet | Playwright score, a11y, Lighthouse, test pass, conversion proxy |
| Keep/discard con git | Quality Guardian + handoff |
| Overnight autonomy | Dispatch Mode / cloud-compute |

Encaja con **grill-me** (afilar antes), **handoff** (cerrar con log), y la cadena en `skill-execution-chain.md`.

---

## Cómo usarlo sin GPU de training

**Producto / UI experiment branch**

```
program.md  →  objetivo + métrica + archivos prohibidas
archivo(s)  →  solo los que el agente puede tocar
métrica     →  ej. “0 fallos Playwright en /dashboard” o “contrast WCAG AA”
loop        →  cambio → test → keep/discard → log en coordination/
```

**No hacer:** clonar autoresearch y esperar mejoras de LLM sin hardware ni dataset.

**Sí hacer:** cuando haya un experimento medible (portfolio light/dark, onboarding funnel, design token density), escribir un `program.md` mínimo y un agente con budget de N intentos.

---

## Relación con capabilities existentes

- `agent-orchestration.md` — supervisor + workers
- `token-efficiency.md` — bound loops, no divagar
- `cloud-compute.md` / Dispatch — runs desatendidos
- `design-automation.md` + UI Integrity — métricas de UI
- `skill-execution-chain.md` — orden humano antes del loop ciego

---

## Decisión

| Acción | Cuándo |
|--------|--------|
| Documentar patrón (este archivo) | **Hecho** |
| Capability formal ADOPT | Cuando el primer experiment branch real use el loop |
| Correr karpathy/autoresearch ML | Solo si hay GPU + objetivo de training |

*Última actualización: 2026-08-22 — Grok*
