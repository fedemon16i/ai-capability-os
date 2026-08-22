# Tech & Growth Stack 2026 — research catalog

Densidad técnica. Sin relleno. Alineado al prompt de arquitectura de vanguardia.

---

## 1. Presentation builders (AI-driven)

| Tool | Rol 2026 | Notas técnicas |
|------|----------|----------------|
| **Gamma** | Líder prompt/markdown → decks + micro-sitios | Bloques dinámicos, tipografía custom, historias interactivas |
| **Tome** | Narrativa AI-first | Bueno para storytelling B2B |
| **Beautiful.ai** | Templates + constraints de diseño | Menos “vibe”, más consistencia |
| **Marp** | Markdown → slides (Git-Ops) | Ideal repo + CI; no AI nativo pero composable con LLMs |

**Features clave a exigir en stack propio:** widgets live (PostHog/Amplitude embeds), prototipos Figma embebidos, opcional Spline/3D en slide, export web.

**Skills relacionados:** `ppt-generation`, `pptx` (SkillsMP / doc skills).

---

## 2. UX/UI cases (modes, motion, 3D, a11y)

### Dashboard alta densidad
- **Compact vs Cozy:** spacing tokens 4/8 vs 16/24; densidades tipográficas (tabular nums, mono para data).
- Preferir **CSS Container Queries** sobre breakpoints globales para paneles.
- Density toggle = design token set, no CSS suelto.

### E-commerce inmersivo
- Catálogo 2D → visor **WebGPU / Spline**.
- Transiciones de ruta: **View Transitions API**.
- Motion síncrono con física del 3D = un solo timeline de estado, no animaciones desacopladas.

### A11y contextual
- Temas daltonismo (protanopía/deuteranopía) vía **CSS variables** inyectadas.
- Respetar `prefers-contrast`, `prefers-reduced-motion`.
- Hard gate: UI Integrity / DESIGN.md del portfolio.

**Skills:** `ui-ux-pro-max`, `frontend-design`, `baseline-ui`, `hallmark`.

---

## 3. Marketing / Growth stack

| Capa | Tools 2026 | Uso |
|------|------------|-----|
| Orquestación mensajes | **Customer.io**, **Loops.so** | Email/push por eventos FE/BE en tiempo real |
| Atribución privacy-first | **Jentis**, **Factors.ai** | Server-side, menos dependencia de cookies 3p |
| Product analytics | **PostHog**, Pendo, Mixpanel | Flags + funnels + session (ya en capabilities/sources) |
| Demanda programática | **LlamaIndex** + edge personalization | Landings por intención semántica |

**Skills marketing (AtCyrus):** page-cro, seo-audit, copywriting, email-sequence, analytics-tracking.

---

## 4. Video / generative media

| Uso | Tools |
|-----|-------|
| Demo B2B / ads | **Sora**, **Runway Gen-3**, **Kling** |
| Avatar soporte/ventas | **HeyGen** + **ElevenLabs** (voz + lip-sync) |
| Clipping changelog/talks | **Opus Clip**, **Vizard** |
| Video en código | **Remotion** (skill AtCyrus) |

---

## 5. Features de producto plug-and-play

| Feature | Implementación 2026 |
|---------|---------------------|
| Búsqueda semántica local | **Orama** / **MiniSearch** (cliente o edge) |
| Command menu | **cmdk** + acciones → agentes/MCP |
| Feature flags | **PostHog Flags** o **LaunchDarkly**; evaluación en edge (Workers) |

---

## Arquitectura unificada (conclusión)

```
Frontend: Next.js + Tailwind v4 + tokens (DESIGN.md / density modes)
    ↓
Product intelligence: PostHog/Pendo (events, flags, replay)
    ↓
Growth: Loops/Customer.io ← eventos; CRO skills en agentes
    ↓
Content: Gamma/Marp (decks) + Remotion/Runway (video)
    ↓
Agents: skills curados (marketplaces) + MCP solo donde hay data live
```

**Principio:** capabilities de ejecución en `ai-capability-os`; knowledge de dominio en `federico-skills`; **sources/** = material externo verificado (Pendo, marketplaces, este catálogo).

*Última actualización: 2026-08-22*
