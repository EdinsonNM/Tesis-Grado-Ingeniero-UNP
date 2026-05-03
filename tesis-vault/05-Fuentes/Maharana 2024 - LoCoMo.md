# Maharana et al. (2024) — LoCoMo: Long Context Modeling Benchmark

## Referencia APA

Maharana, A., Lee, D., Tulyakov, S., Bansal, M., Barbieri, F., & Fang, Y. (2024). LoCoMo: Long context modeling benchmark. *arXiv preprint*. https://arxiv.org/abs/2402.17753

Proyecto: https://snap-research.github.io/locomo/ | Código: https://github.com/snap-research/locomo

## Pregunta que responde

¿Cómo evaluar la capacidad de los LLMs para mantener coherencia y comprensión en conversaciones extremadamente largas (miles de turnos) que exceden la ventana de contexto?

## Método

LoCoMo: conversaciones multi-sesión de hasta 9000 turnos entre personas virtuales con eventos de vida, recuerdos y relaciones. Las preguntas requieren razonamiento sobre eventos pasados, relaciones entre personajes y líneas temporales. Se evalúa con QA, resumen y generación de eventos futuros.

## Métricas reportadas

- Los LLMs con contexto largo superan a los de contexto corto, pero todos degradan significativamente en conversaciones muy largas.
- El resumen de conversación como estrategia de compresión mejora la precisión vs. truncar el contexto.
- Evidencia de que la coherencia conversacional es más difícil de mantener que la exactitud factual puntual.

## Aporte a la tesis

LoCoMo es uno de los [[Dataset de evaluacion|datasets de evaluación]] para la dimensión de [[Coherencia conversacional]] del [[IQCR]]. Proporciona escenarios que prueban si las técnicas de memoria ([[MemoryBank]], [[SessionFacts]], [[Mem0]]) mantienen coherencia en conversaciones largas, que es análogo a lo que ocurre en sesiones multi-MCP extendidas.

## Conceptos relacionados

- [[LoCoMo]]
- [[Coherencia conversacional]]
- [[Dataset de evaluacion]]
- [[MemoryBank]]
- [[Context rot]]
- [[Compaction]]
