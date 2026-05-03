# Delimitación de la Investigación

→ Sección 1.5 del capítulo [[Cap 1 - Aspectos de la Problematica]]

---

## Delimitación temática

La investigación se enfoca exclusivamente en la **capa de arquitectura del agente**: cómo se gestiona la memoria, el contexto y las herramientas alrededor del LLM. No incluye:

- Fine-tuning o ajuste de pesos del modelo.
- Ingeniería de prompts sin cambios arquitecturales.
- Modificaciones al protocolo MCP en sí.
- Sistemas de agentes multi-agente (más de un agente coordinado).

## Qué sí incluye

- Técnicas de memoria externa: [[SessionFacts]], [[MemoryBank]], [[Mem0]].
- Técnicas de recuperación: [[RAG]], [[RAG-MCP]], [[Recuperacion federada]], [[Hybrid retrieval]].
- Técnicas de filtrado de herramientas: [[Tool gating]], [[Sharding]], [[Namespaces]].
- Técnicas de optimización de contexto: [[Caching semantico]], [[Compaction]], [[Prompt caching]].

## Delimitación del modelo LLM

Se seleccionan uno o dos modelos de frontera como variable de control fija. Los resultados son específicos para esos modelos, aunque se espera que los patrones sean generalizables. No se evalúa la degradación diferencial entre modelos.

## Delimitación temporal de las sesiones

El experimento evalúa sesiones de hasta **100 turnos** y contextos de hasta **el 80% de la ventana de contexto** del modelo seleccionado. No se evalúan escenarios que superen la ventana de contexto (truncación).

## Delimitación del entorno multi-MCP

Se evalúan configuraciones de **2, 3 y 5 servidores MCP activos simultáneamente**, con catálogos de **20, 50 y 100 herramientas** en total. Esto cubre el rango relevante para aplicaciones empresariales sin llegar a infraestructuras de escala masiva.

## Lo que la tesis no busca probar

- Que una técnica es mejor en todos los contextos posibles (imposible de generalizar).
- Que el [[Context rot]] es el único factor que afecta la calidad de los agentes.
- Resultados de producción en entornos reales con usuarios humanos.

## Referencias

- [[Contexto activo]]
- [[Ventana de contexto]]
- [[Servidor MCP]]
- [[Diseno metodologico]]
