# Glosario de Términos

→ Sección 2.3 del capítulo [[Cap 2 - Marco Teorico]]

Definiciones operacionales de los términos técnicos usados en la tesis. Cada término tiene su página propia en `04-Conceptos/` con definición expandida.

---

## El fenómeno central

**[[Context rot]]** — Proceso de degradación progresiva y acumulativa de la calidad de respuestas de un agente LLM producido por el crecimiento del contexto activo en conversaciones multi-turno con múltiples servidores MCP.

**[[Tool overload]]** — Sobrecarga cognitiva del agente LLM por exposición excesiva de herramientas disponibles en el contexto, que dificulta la selección correcta e infla el consumo de tokens.

**[[Lost in the middle]]** — Fenómeno por el cual la atención del modelo se concentra en los extremos del contexto, degradando la recuperación de información en posiciones centrales.

---

## La arquitectura

**[[Agente LLM]]** — Sistema de software que usa un LLM como motor de razonamiento y lo conecta con herramientas externas para ejecutar acciones, consultar datos o interactuar con APIs.

**[[Model Context Protocol]]** — Protocolo estándar de Anthropic para conectar LLMs a herramientas, recursos y prompts externos de forma estructurada e interoperable.

**[[Servidor MCP]]** — Servidor que expone herramientas, recursos y prompts a un agente LLM vía MCP. En una arquitectura multi-MCP, varios servidores operan simultáneamente.

**[[Ventana de contexto]]** — Límite máximo de tokens que un LLM puede procesar en una sola llamada de inferencia.

**[[Contexto activo]]** — Porción de la ventana de contexto efectivamente ocupada en un momento dado: instrucciones, historial, esquemas de herramientas, resultados de llamadas.

**[[Namespaces]]** — Mecanismo que agrupa herramientas de distintos servidores MCP bajo identificadores separados para evitar colisiones de nombres.

---

## Las técnicas de mitigación

**[[Tool gating]]** — Filtrado dinámico del conjunto de herramientas disponibles para el agente según la relevancia semántica de la consulta actual.

**[[SessionFacts]]** — Mecanismo de extracción y persistencia de hechos clave de la sesión en almacenamiento externo, para recuperarlos sin mantenerlos en el contexto activo.

**[[MemoryBank]]** — Sistema de memoria externa a largo plazo para agentes LLM, con priorización de recuerdos por relevancia y frecuencia de acceso.

**[[Mem0]]** — Capa de memoria adaptativa que extrae, indexa y recupera automáticamente información relevante del historial conversacional.

**[[Caching semantico]]** — Reutilización de resultados de llamadas a herramientas anteriores cuando una nueva consulta es semánticamente similar, evitando llamadas redundantes.

**[[Recuperacion federada]]** — Recuperación distribuida de información desde múltiples fuentes heterogéneas (servidores MCP, bases de datos, documentos) en una sola operación.

**[[RAG]]** — Retrieval-Augmented Generation: arquitectura que recupera documentos relevantes para aumentar la generación del LLM sin mantenerlos en contexto permanente.

**[[RAG-MCP]]** — Extensión de RAG para recuperar herramientas MCP relevantes dinámicamente en lugar de incluir todos los esquemas en el contexto.

**[[Compaction]]** — Reducción del contexto activo mediante resumen, poda o compresión de turnos anteriores.

**[[Prompt caching]]** — Reutilización del procesamiento previo de prefijos de prompt idénticos, reduciendo costo y latencia.

**[[Hybrid retrieval]]** — Combinación de recuperación léxica (BM25) y semántica (vectores) para maximizar precisión y cobertura.

**[[Sharding]]** — Particionamiento del espacio de herramientas en subconjuntos para reducir el espacio de búsqueda efectivo.

---

## Las métricas

**[[IQCR]]** — Índice de Calidad de Respuesta en Contexto: métrica compuesta que agrega exactitud, tasa de alucinación, coherencia conversacional y eficiencia de tokens mediante ponderación [[AHP]].

**[[Exactitud de respuesta]]** — Proporción de respuestas correctas sobre el total, comparadas contra [[Ground truth]].

**[[Tasa de alucinacion]]** — Frecuencia de afirmaciones factuales incorrectas o inventadas en las respuestas del agente.

**[[Coherencia conversacional]]** — Consistencia semántica de las respuestas a lo largo de la conversación, medida con [[BERTScore]].

**[[Eficiencia de tokens]]** — Relación entre tokens consumidos y calidad de respuesta obtenida.

**[[Latencia p50 p95]]** — Percentiles 50 y 95 de la distribución de tiempos de respuesta.

**[[TTFT]]** — Time to First Token: tiempo hasta el primer token generado, indicador de latencia percibida.

**[[Normalizacion de metricas]]** — Proceso de escalar métricas heterogéneas a un rango común [0,1] antes de agregarlas en el IQCR.

**[[AHP]]** — Proceso Analítico Jerárquico: método para ponderar los componentes del IQCR según su importancia relativa.

**[[BERTScore]]** — Métrica de similitud semántica basada en embeddings de BERT, usada para evaluar coherencia conversacional.

**[[Baseline]]** — Condición de control sin técnicas de mitigación. Representa la degradación natural del agente sin intervención.

**[[Ground truth]]** — Respuestas de referencia verificadas para calcular exactitud y detectar alucinaciones.

---

## Los conceptos metodológicos

**[[Diseno factorial 2k]]** — Diseño experimental con k factores a 2 niveles que permite evaluar efectos principales e interacciones entre técnicas.

**[[PELT]]** — Pruned Exact Linear Time: algoritmo de detección de puntos de cambio estadísticos en series de métricas.

**[[TOST]]** — Two One-Sided Tests: prueba de equivalencia estadística para demostrar que una técnica no degrada una métrica más allá de un margen aceptable.
