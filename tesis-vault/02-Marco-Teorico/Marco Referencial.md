# Marco Referencial

→ Sección 2.4 del capítulo [[Cap 2 - Marco Teorico]]
Fuente: `DOC-02_Catalogo_Fuentes.docx`

El marco referencial centraliza las fuentes primarias y secundarias que fundamentan la investigación, organizadas en seis categorías temáticas según su función en el marco teórico y metodológico.

Criterios de inclusión: fuentes que abordan al menos uno de los tres ejes temáticos — (a) técnicas de memoria en LLMs, (b) gestión de context rot, o (c) arquitecturas de agentes con herramientas y MCP. Se priorizan fuentes primarias publicadas en NeurIPS, ICLR, ACL, AAAI o arXiv peer-reviewed.

---

## Categoría A — Papers Fundacionales: Razonamiento y Uso de Herramientas

Establecen los fundamentos del [[Agente LLM]] y el ciclo de uso de herramientas.

| Fuente | Aporte al marco teórico |
|---|---|
| [[Vaswani 2017 - Attention is All You Need]] | Arquitectura transformer; base de la [[Ventana de contexto]] y el mecanismo de atención |
| [[Brown 2020 - Language Models are Few-Shot Learners]] | LLMs a escala; paradigma de razonamiento general sin fine-tuning |
| [[Yao 2022 - ReAct]] | Ciclo razonamiento-acción-observación del agente; mecanismo de crecimiento del [[Contexto activo]] |
| [[Schick 2023 - Toolformer]] | Selección autónoma de herramientas; principio del [[Tool gating]] |
| Wang et al. (2024) — Survey on LLM Agents | Taxonomía de sistemas de memoria en agentes LLM |
| Wei et al. (2022) — Chain-of-Thought | Razonamiento en cadena como base de las capacidades agentes |
| Patil et al. (2023) — Gorilla | Degradación con catálogos grandes de APIs; umbral de 20 herramientas |

---

## Categoría B — Memoria en LLMs: Sistemas y Arquitecturas

Técnicas de mitigación del [[Context rot]] basadas en memoria externa.

| Fuente | Aporte al marco teórico |
|---|---|
| [[Packer 2023 - MemGPT]] | Memoria virtual RAM/disco para LLMs; [[Compaction]] del historial (-70% tokens) |
| [[Zhong 2023 - MemoryBank]] | Banco de memoria con olvido de Ebbinghaus (+37% coherencia en 500 turnos) |
| [[Chhikara 2025 - Mem0]] | Memoria adaptativa por tipo; reducción del 91% en tokens |
| Ouyang et al. (2022) — RLHF | Alineación de modelos con preferencias del usuario |

---

## Categoría C — Recuperación Aumentada (RAG) y Variantes

Técnicas de recuperación selectiva aplicadas a contexto y herramientas.

| Fuente | Aporte al marco teórico |
|---|---|
| [[Lewis 2020 - RAG]] | RAG original; principio de recuperar solo lo relevante |
| [[Tang 2025 - RAG-MCP]] | RAG aplicado al catálogo MCP; -68% tokens con <2% pérdida de exactitud |
| Liu et al. (2023) — Lost in the Middle | Evidencia de degradación por posición en contextos largos (-40% atención central) |
| Shi et al. (2023) — Distractors | Información irrelevante reduce exactitud de razonamiento hasta 65% |

---

## Categoría D — Benchmarks de Herramientas y Evaluación

Instrumentos de medición para las hipótesis experimentales.

| Fuente | Benchmark | Evalúa |
|---|---|---|
| [[Wu 2024 - LongMemEval]] | [[LongMemEval]] | Memoria a largo plazo: 5 tipos, hasta 115K tokens de historial |
| [[Maharana 2024 - LoCoMo]] | [[LoCoMo]] | Coherencia en conversaciones de hasta 9,000 turnos |
| [[Yin 2026 - SimpleToolHalluBench]] | [[SimpleToolHalluBench]] | Alucinación de herramientas: nombre, parámetros, valores |
| Bwook et al. (2025) | [[ToolHaystack]] | Selección correcta en catálogos de alta dimensionalidad |
| Qin et al. (2023) — ToolLLM | ToolBench | 16,000+ APIs reales; base comparativa general |

---

## Categoría E — Protocolos, Frameworks y Especificaciones Técnicas

| Fuente | Relevancia |
|---|---|
| Anthropic (2024) — MCP Specification | Estándar del [[Model Context Protocol]] v1.0; define el flujo de comunicación |
| OpenAI (2023) — Function Calling | Precursor del MCP; establece el patrón de invocación de herramientas |
| Chroma Research (2025) — Context Rot Benchmark | Evidencia empírica de producción: >30% degradación en 50 turnos |
| Redis Labs (2025) — Enterprise AI Patterns | 67% del costo de inferencia atribuible a acumulación de contexto |

---

## Categoría F — Herramientas de Evaluación y Observabilidad

| Herramienta | Uso en la tesis |
|---|---|
| ChromaDB | Base vectorial para [[RAG]] de historial y RAG-MCP |
| RedisVL | Implementación de [[Caching semantico]] (umbral coseno 0.92–0.95) |
| MLflow | Tracking de experimentos y métricas por condición experimental |
| BERTScore (Zhang et al., 2020) | Medición de [[Coherencia conversacional]] |
| scipy / statsmodels / pingouin | Análisis estadístico: ANOVA, Wilcoxon, [[TOST]] |
| ruptures | Implementación de [[PELT]] para detección de puntos de cambio |

---

## Notas metodológicas

- **Actualización**: este marco debe actualizarse antes de la defensa para incluir publicaciones nuevas en benchmarks de memoria — el campo avanza rápidamente (LongMemEval, LoCoMo y ToolHaystack son de 2024–2025).
- **Idioma**: la mayoría de fuentes primarias sobre MCP, memory layers y guardrails está en inglés. No se identificó un cuerpo equivalente de papers primarios en español sobre este subproblema al momento de la revisión (abril 2026).
- **Fichas individuales**: ver `05-Fuentes/` para la ficha completa de cada paper con referencia APA, método, métricas reportadas y aporte específico a la tesis.

## Fuentes relacionadas

- [[Antecedentes]] — síntesis narrativa de los antecedentes más directos
- [[Catalogo inicial de fuentes]] — tabla completa con URLs de datasets y benchmarks
- [[Bases Teoricas]] — desarrollo conceptual de las fuentes
