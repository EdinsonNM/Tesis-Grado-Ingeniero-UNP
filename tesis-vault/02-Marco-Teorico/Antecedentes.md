# Antecedentes de la Investigación

→ Sección 2.1 del capítulo [[Cap 2 - Marco Teorico]]

---

## Antecedentes sobre degradación de contexto en LLMs

**Liu et al. (2023) — Lost in the Middle** → [[Liu 2023 - Lost in the Middle]]
Primer estudio sistemático de cómo la posición de la información dentro del contexto afecta la capacidad del LLM para recuperarla. Evidencia el efecto [[Lost in the middle]]: rendimiento en U (alto al inicio y al final, bajo en el medio). Antecedente directo del mecanismo de [[Context rot]].

**Yao et al. (2022) — ReAct** → [[Yao 2022 - ReAct]]
Define el ciclo razonamiento-acción-observación que es el patrón de operación del [[Agente LLM]]. Cada observación (resultado de herramienta) se acumula en el [[Contexto activo]], estableciendo el mecanismo de crecimiento que esta tesis busca controlar.

---

## Antecedentes sobre técnicas de memoria

**Packer et al. (2023) — MemGPT** → [[Packer 2023 - MemGPT]]
Propone tratar el LLM como un sistema operativo con RAM (contexto en ventana) y disco (almacenamiento externo). Primera solución arquitectural al problema de contexto limitado. Antecedente de [[MemoryBank]] y [[SessionFacts]].

**Zhong et al. (2023) — MemoryBank** → [[Zhong 2023 - MemoryBank]]
Implementa banco de memoria externa con priorización inspirada en la curva de olvido de Ebbinghaus. Muestra mejora significativa en coherencia y consistencia en conversaciones largas.

**Chhikara et al. (2025) — Mem0** → [[Chhikara 2025 - Mem0]]
Estado del arte en memoria adaptativa para agentes. Logra reducción del 91% en uso de tokens respecto a full context, con mejora del 26% en precisión de memoria vs. GPT-4 full context. Resultado de referencia para la tesis.

---

## Antecedentes sobre filtrado de herramientas

**Schick et al. (2023) — Toolformer** → [[Schick 2023 - Toolformer]]
Demuestra que los LLMs pueden aprender a seleccionar herramientas de forma selectiva. El principio —llamar herramientas solo cuando son necesarias— es el fundamento del [[Tool gating]].

**Tang y Gan (2025) — RAG-MCP** → [[Tang 2025 - RAG-MCP]]
Aplica RAG al espacio de herramientas MCP: en lugar de pasar todos los esquemas al LLM, recupera solo los k más relevantes para cada consulta. Antecedente directo más próximo a la propuesta de esta tesis.

**Vercel (2025, diciembre) — Caso agente d0** → [[Vercel 2025 - d0 Agent Tool Removal]]
Caso de producción: el equipo de infraestructura de Vercel identificó que su agente d0 de CI/CD recibía 17-18 herramientas MCP de las cuales solo usaba un subconjunto mínimo en la práctica. Al eliminar estáticamente las herramientas no esenciales, la tasa de éxito pasó de 80% a 100%, el consumo de tokens cayó un 37%, la velocidad aumentó 3.5× y los pasos por tarea se redujeron un 42%. **Distinción clave**: la reducción de Vercel es estática (herramientas eliminadas permanentemente); la tesis propone filtrado dinámico via [[RAG-MCP]] (herramientas filtradas por relevancia por consulta). El caso sirve como evidencia de producción de que el [[Tool overload]] tiene impacto cuantificable y que su mitigación produce ganancias sustanciales.

---

## Antecedentes sobre evaluación y benchmarks

**Wu, Truong y Ho (2024) — LongMemEval** → [[Wu 2024 - LongMemEval]]
Benchmark de 500 preguntas para evaluar 5 tipos de memoria en conversaciones multi-sesión de hasta 115K tokens. Base metodológica para la dimensión de exactitud de memoria.

**Maharana et al. (2024) — LoCoMo** → [[Maharana 2024 - LoCoMo]]
Conversaciones de hasta 9000 turnos con preguntas de razonamiento temporal y relacional. Base para la dimensión de coherencia conversacional del [[IQCR]].

**Yin et al. (2026) — SimpleToolHalluBench** → [[Yin 2026 - SimpleToolHalluBench]]
Primer benchmark con reasoning traps diseñados para medir alucinación de herramientas. Base para la dimensión de selección correcta de herramientas en escenarios [[Tool overload]].

---

## Antecedentes sobre marcos teóricos unificadores

**Zhou et al. (2026) — Externalization in LLM Agents** → [[Zhou 2026 - Externalization in LLM Agents]]
Revisión unificada de 54 páginas que propone el paradigma de *externalización* para explicar la evolución de los agentes LLM: memoria (externaliza estado), skills (externaliza conocimiento procedural), protocolos (externaliza estructura de interacción) y harness engineering (capa de coordinación gobernada). El paper cita directamente MemGPT, MemoryBank y Mem0 — fuentes centrales de la tesis. Su contribución principal es una progresión histórica: *pesos → contexto → harness*. La tesis opera en la tercera era, generando evidencia empírica sobre qué configuraciones de harness son más efectivas en entornos multi-MCP.

---

## Brecha identificada

Los antecedentes abordan el problema de forma fragmentada:
- Los benchmarks de memoria no incluyen el fenómeno multi-MCP.
- Las técnicas de memoria se evalúan sin comparación sistemática entre sí.
- No existe protocolo que compare simultáneamente técnicas de memoria, filtrado y caching en condiciones multi-MCP controladas.

Esta brecha es el espacio que la tesis busca llenar.
