# Mapa del marco teorico

## Bloques teoricos

1. [[Modelo de lenguaje de gran escala]]
2. [[Agente LLM]]
3. [[Model Context Protocol]]
4. [[Context rot]]
5. Tecnicas de memoria y gestion de contexto
6. Estrategias de [[Tool gating]]
7. Evaluacion y benchmarks

## Cadena causal

Los LLM operan dentro de una ventana de contexto. Cuando se convierten en agentes y se conectan a multiples servidores MCP, el contexto crece por herramientas, resultados y estado de sesion. Ese crecimiento produce [[Context rot]]. Las tecnicas de memoria, recuperacion y filtrado buscan reducir el ruido contextual sin perder informacion relevante.

## Tecnicas del marco teorico

- [[RAG]]
- [[RAG-MCP]]
- [[SessionFacts]]
- [[MemoryBank]]
- [[Mem0]]
- [[Caching semantico]]
- [[Tool gating]]
- [[Recuperacion federada]]

## Benchmarks

- [[Dataset de evaluacion]]
- [[Ground truth]]
- [[LongMemEval]]
- [[LoCoMo]]
- [[SimpleToolHalluBench]]
- [[ToolHaystack]]
- [[Escenarios multi-MCP sinteticos]]
