# Justificación e Importancia

→ Sección 1.3 del capítulo [[Cap 1 - Aspectos de la Problematica]]

---

## Por qué es un problema relevante

El [[Context rot]] no es un problema teórico: afecta directamente la confiabilidad de los [[Agente LLM|agentes LLM]] en producción. Un agente que degrada conforme avanza la sesión pierde la confianza del usuario sin señal visible de fallo: no lanza un error, simplemente responde cada vez peor.

## Por qué es un problema no resuelto

La literatura existente aborda la degradación de contexto de forma parcial:
- Los benchmarks de memoria ([[LongMemEval]], [[LoCoMo]]) miden el fenómeno pero no proveen protocolos de comparación entre técnicas.
- Las técnicas de mitigación ([[MemoryBank]], [[Mem0]], [[RAG-MCP]]) se evalúan en escenarios distintos y con métricas inconsistentes.
- No existe un protocolo experimental unificado que compare técnicas en el contexto específico de arquitecturas **multi-MCP**.

## Por qué importa en el contexto latinoamericano

En organizaciones con presupuestos limitados (PyMEs, sector público, startups latinoamericanas), el costo de los tokens no es una optimización opcional. Si el [[Context rot]] multiplica el consumo de tokens en sesiones largas, puede hacer inviable económicamente la adopción de agentes LLM.

## Aporte de la investigación

1. **Protocolo experimental reproducible**: cualquier equipo puede replicar el experimento con su propio modelo y servidores MCP.
2. **Métrica compuesta unificada**: el [[IQCR]] integra exactitud, alucinación, coherencia y eficiencia en un solo índice comparable.
3. **Mapa de umbrales**: identificar en qué punto del crecimiento del contexto aparece la degradación permite diseñar sistemas con márgenes de seguridad explícitos.
4. **Recomendación de configuración**: la combinación óptima de técnicas identificada es directamente aplicable.

## Referencias

- [[Context rot]]
- [[IQCR]]
- [[Problema de investigacion]]
- [[Objetivos de investigacion]]
