# Resumen de la tesis

## Titulo

Medicion del impacto de tecnicas de memoria y gestion de contexto sobre la degradacion de respuestas en agentes LLM conectados a multiples servidores MCP.

## Idea principal

La investigacion estudia el [[Context rot]] en [[Agente LLM|agentes LLM]] conectados a multiples [[Servidor MCP|servidores MCP]]. El fenomeno aparece cuando el crecimiento del contexto activo, la exposicion de muchas herramientas y la acumulacion de resultados intermedios reducen la exactitud, aumentan alucinaciones, elevan latencia y encarecen el uso de tokens.

## Aporte esperado

El aporte es un protocolo experimental reproducible para comparar tecnicas de mitigacion:

- [[Tool gating]]
- [[SessionFacts]]
- [[MemoryBank]]
- [[Caching semantico]]
- [[Recuperacion federada]]

La comparacion se hara mediante metricas cuantitativas: [[IQCR]], exactitud, tasa de alucinacion, coherencia conversacional, consumo de tokens y latencia.

## Alcance

La tesis no busca entrenar un nuevo modelo ni modificar pesos neuronales. Su foco esta en la arquitectura del agente que envuelve al LLM: memoria, recuperacion, filtrado de herramientas, control de contexto y evaluacion.

## Relacion con otros nodos

- Problema: [[Problema de investigacion]]
- Objetivos: [[Objetivos de investigacion]]
- Hipotesis: [[Hipotesis de investigacion]]
- Variables: [[Variables e indicadores]]
- Metodo: [[Diseno metodologico]]

