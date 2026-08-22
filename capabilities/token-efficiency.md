# Capability: Token Efficiency & Cost Control

**Domain:** ai-engineering  
**Status:** ADOPT  
**Delegation level:** 3 / 5  
**Score:** 60 / 80  
**Last updated:** 2026-08-22

---

## Problem class

Cuando el costo de tokens (latencia, dinero, o rate limits) se convierte en un constraint real para operar agentes — especialmente en runs largos, ciclos de research multi-agente, o sesiones desatendidas donde no hay humano monitoreando el consumo.

El problema no es solo costo monetario. Un agente que consume tokens ineficientemente también es más lento, más propenso a cortar contexto en el momento incorrecto, y más difícil de predecir.

## Principio rector

> **Contexto curado > contexto completo.**  
> Un modelo bien dirigido por un STATUS.md + index actualizado necesita menos tokens para llegar al mismo resultado que un modelo al que se le vuelca el repo entero.  
> El primer lugar donde buscar eficiencia es en la estructura de información, no en los prompts.

## Las 7 técnicas de alto impacto (2026)

### 1. Prompt / Context Caching

La API de Anthropic cachea el prefijo del prompt si no cambia entre calls. En sesiones largas donde el system prompt o el CLAUDE.md se repite, el cacheado puede reducir el costo hasta un 90% en los tokens cached.

**Cómo activarlo:** los primeros N tokens del prompt que sean idénticos entre calls se cachean automáticamente en Claude Sonnet 3.5+ con `cache_control`. En Claude Code, el CLAUDE.md se carga una vez y se cachea para la sesión.

**Regla práctica:** poner el contexto estático (CLAUDE.md, STATUS.md, system prompt fijo) PRIMERO en el prompt, antes del contenido dinámico. El caché se invalida en el primer token que cambia.

### 2. Retrieve Once, Reuse

No releer el mismo archivo en cada step del agente. Si el agente lee `shared.css` al principio de la sesión, ese contenido está en contexto — no hay que leerlo de nuevo.

**Anti-patrón:** un agente que hace `Read(shared.css)` tres veces en la misma sesión porque sus pasos no comparten contexto. Esto sucede cuando un Workflow fan-out no pasa el contenido relevante a los sub-agentes.

**Regla práctica:** en orquestaciones, el Supervisor lee los archivos relevantes una vez y pasa el contenido directamente al Worker via el prompt — no le dice al Worker "leé el archivo X".

### 3. Model Routing

No todos los pasos de un pipeline necesitan el modelo más inteligente. Usar el modelo correcto para cada tarea.

| Tarea | Modelo apropiado |
|-------|-----------------|
| Pasos mecánicos: formatear, deduplicar, extraer campos | Claude Haiku 4.5 (más barato, más rápido) |
| Análisis de calidad, evaluación de edge cases, síntesis | Claude Sonnet 5 |
| Decisiones complejas, adversarial review, arquitectura | Claude Opus 5 |

**En la práctica:** en un Workflow de research, los Workers de discovery pueden correr en Haiku; el Quality Guardian corre en Sonnet o Opus.

```javascript
// Ejemplo en Workflow script
const discoveries = await pipeline(DOMAINS, 
  d => agent(d.prompt, { model: 'haiku', phase: 'Discover' }),  // barato
  r => agent(verifyPrompt(r), { model: 'sonnet', phase: 'Verify' })  // calidad
)
```

### 4. Bound Agent Loops (límites duros)

Los bucles de agentes sin límite son el error más caro. Siempre definir:
- Máximo de steps por tarea
- Máximo de retries por error
- Budget de tokens explícito para el Workflow

**En Claude Code Workflows:**
```javascript
// Usar el budget object del Workflow
while (budget.total && budget.remaining() > 50_000) {
  const result = await agent("siguiente paso")
  // ...
}
// Si no hay budget definido, usar un contador manual
let steps = 0;
while (steps < 10) { steps++; /* ... */ }
```

**Regla práctica:** cualquier loop de agente debe tener un exit condition que no dependa de que el agente "termine correctamente". Los agentes se pueden quedar en loops si el task description es ambiguo.

### 5. Prune MCP Tool Definitions

Cada MCP server conectado agrega sus definiciones de herramientas al context window de cada call. Un MCP server con 30 tools puede agregar 20,000–50,000 tokens por call — aunque no uses esas tools.

**Regla práctica:** no conectar MCP servers que no vas a usar en esa sesión. Si Figma MCP está conectado pero el task es solo git, desconectarlo reduce el overhead por call.

**Verificación:** el campo `tool_use_tokens` en el usage response de la API muestra cuántos tokens consumen las tool definitions. Si es alto proporcionalmente → revisar qué MCP servers están activos.

### 6. Summarize Intermediate Results

En pipelines largos, no reenviar el output completo de cada step al siguiente. Resumir antes de pasar.

**Anti-patrón:**
```javascript
const rawResearch = await agent("investigá 20 candidatos en detalle") // 8,000 tokens de output
const evaluation = await agent(`evaluá esto: ${rawResearch}`) // manda 8,000 tokens al próximo agente
```

**Patrón correcto:**
```javascript
const rawResearch = await agent("investigá 20 candidatos, devolvé JSON estructurado con top 5", { schema: TOP5_SCHEMA })
const evaluation = await agent(`evaluá estos 5: ${JSON.stringify(rawResearch)}`) // 500 tokens
```

Los schemas de output estructurado (JSON Schema) en los Workflows son la forma más efectiva de forzar summarización automática.

### 7. Preferir Conocimiento Curado sobre Dump de Contexto

El patrón más costoso: darle al agente todo el repo y decirle "entendé el contexto". El patrón eficiente: darle STATUS.md + `_index.md` + el archivo específico que necesita.

**Jerarquía de contexto (de menor a mayor costo):**

| Nivel | Qué se pasa | Tokens aprox |
|-------|------------|--------------|
| Referencia curada | STATUS.md + índice relevante | ~500-1,000 |
| Archivo específico | El capability file o template del task | ~500-2,000 |
| Sección de repo | Solo los archivos del dominio relevante | ~2,000-5,000 |
| Repo completo | Dump de todo | ~50,000+ |

**Regla práctica:** el Supervisor pasa el contexto mínimo necesario. El Worker no hace `Read` de archivos que el Supervisor ya puede resumir en 3 líneas.

---

## Visibilidad de consumo

### En Claude Code Web Sessions

El contexto usado se muestra en el header de la sesión (tokens remaining). Observar:
- ¿El contexto crece linealmente? → normal
- ¿Hay un salto grande de golpe? → un tool result o MCP response grande
- ¿Se está acercando al límite antes de terminar la tarea? → dividir la tarea o resumir contexto

### En Workflows (API)

El objeto `budget` es el medidor nativo:
```javascript
log(`Tokens gastados: ${budget.spent()}, restantes: ${budget.remaining()}`)
```

### Señales de ineficiencia

| Señal | Causa probable | Fix |
|-------|---------------|-----|
| Sesión lenta a pesar de task simple | MCP servers pesados activos | Desconectar los no usados |
| Worker relee archivos que ya están en contexto | No se está pasando el contenido, se está pasando la referencia | Pasar el contenido directamente |
| Rate limits frecuentes en Workflows | Demasiados agentes en paralelo / loops sin bound | Añadir límites, reducir concurrencia |
| Output de un step es enorme | No se está usando schema de output estructurado | Agregar JSON Schema al agent call |

---

## Relación con otras capabilities

**Agent Orchestration:** el Supervisor es responsable de la eficiencia de tokens del ciclo completo. Los Workers solo reciben lo que necesitan — no el repo entero.

**Quality Guardian:** puede agregar un check de eficiencia: ¿el output del Worker es proporcional a la complejidad del task? Un Worker que devuelve 5,000 tokens para un task de clasificación simple es una señal de prompt mal diseñado.

**STATUS.md como herramienta de eficiencia:** mantener STATUS.md actualizado no es solo orden — es la forma más económica de dar contexto a un agente nuevo. Un STATUS.md bien escrito de 500 tokens reemplaza 5,000 tokens de exploración del repo.

---

## When to use

- Antes de diseñar cualquier Workflow con más de 5 agentes
- Cuando el costo mensual de API empieza a ser relevante
- En runs desatendidos (dispatch mode) donde no hay humano monitoreando
- Cuando se agregan MCP servers nuevos (verificar overhead de tool definitions)
- Cuando un pipeline se siente lento sin razón obvia

## When NOT to use

- Para tasks únicos y cortos donde la eficiencia es irrelevante
- Como excusa para dar al agente contexto insuficiente — la calidad del output depende de la calidad del contexto

## Delegation level

**3/5** — El diseño de la estrategia de eficiencia es trabajo de Federico. La implementación (schemas, budget objects, model routing en Workflows) es delegable a Claude Code.

## Ponytail score

**5/10** — Las técnicas son bien definidas pero requieren aplicación consciente por diseño, no son automáticas. No hay un botón de "ser eficiente". El valor está en el conocimiento de los patterns, no en una tool.

## Related capabilities

- [Agent Orchestration](agent-orchestration.md) — el contexto donde se aplican estas técnicas
- [Cloud Compute](cloud-compute.md) — runs desatendidos en VPS requieren disciplina de tokens
- [Memory MCP](memory-mcp.md) — alternativa a re-pasar contexto: guardarlo en memoria persistente

## Notes

- **El mayor desperdicio de tokens en la práctica:** agentes que leen el mismo archivo 3 veces en una sesión larga porque los sub-steps no comparten el contenido leído.
- **Caching en Claude Code:** el CLAUDE.md se cachea automáticamente para la sesión. Si hacés cambios frecuentes al CLAUDE.md durante una sesión de trabajo, cada cambio invalida el caché — hacé los cambios todos juntos al principio o al final.
- **Tool definitions overhead:** si Figma MCP tiene 33 tools definidas y cada call agrega ~1,000 tokens de tool definitions, una sesión de 50 tool calls = 50,000 tokens solo en definiciones. Relevante cuando Figma MCP está conectado pero no se usa.
