# log.md — Registro de actividad del wiki

Registro cronológico append-only. Cada entrada: `## [YYYY-MM-DD] tipo | descripción`.
Tipos: `init`, `ingest`, `expand`, `query`, `lint`, `schema`.

Usar: `grep "^## \[" log.md | tail -10` para ver las últimas 10 entradas.

---

## [2026-05-01] init | Inicialización del wiki con patrón llm-wiki

Creación de la infraestructura base del wiki siguiendo el patrón llm-wiki:

- Creado `CLAUDE.md` con schema completo: estructura de carpetas, formatos de páginas, operaciones estándar.
- Creado `index.md` con catálogo de todas las páginas existentes y las que se crearán.
- Creado `log.md` (este archivo).

Estado al momento de la inicialización:
- Páginas de conceptos existentes: 26
- Fichas de fuentes existentes: 1 (catálogo general, sin fichas individuales)
- Términos en inbox pendientes: 12

---

## [2026-05-01] expand | Ventana de contexto

Creada página `04-Conceptos/Ventana de contexto.md`. Concepto base para entender el límite físico del LLM que da origen al problema del context rot.

## [2026-05-01] expand | Contexto activo

Creada página `04-Conceptos/Contexto activo.md`. Distinción clave entre la ventana total disponible y la porción efectivamente ocupada durante la sesión.

## [2026-05-01] expand | Latencia p50 p95

Creada página `04-Conceptos/Latencia p50 p95.md`. Métricas de distribución de latencia usadas en el diseño experimental.

## [2026-05-01] expand | TTFT

Creada página `04-Conceptos/TTFT.md`. Tiempo hasta el primer token como indicador de latencia percibida.

## [2026-05-01] expand | Diseno factorial 2k

Creada página `04-Conceptos/Diseno factorial 2k.md`. Diseño experimental que permite estudiar efectos principales e interacciones de k factores binarios.

## [2026-05-01] expand | TOST

Creada página `04-Conceptos/TOST.md`. Prueba estadística para demostrar equivalencia entre condiciones experimentales.

## [2026-05-01] expand | PELT

Creada página `04-Conceptos/PELT.md`. Algoritmo para detectar puntos de cambio estadísticos en series de métricas de calidad.

## [2026-05-01] expand | Namespaces

Creada página `04-Conceptos/Namespaces.md`. Mecanismo de aislamiento de herramientas entre servidores MCP.

## [2026-05-01] expand | Sharding

Creada página `04-Conceptos/Sharding.md`. Particionamiento de espacios de herramientas para mejorar recuperación.

## [2026-05-01] expand | Hybrid retrieval

Creada página `04-Conceptos/Hybrid retrieval.md`. Combinación de BM25 y recuperación vectorial para mejorar relevancia.

## [2026-05-01] expand | Compaction

Creada página `04-Conceptos/Compaction.md`. Técnica de compresión del contexto activo para reducir el context rot.

## [2026-05-01] expand | Prompt caching

Creada página `04-Conceptos/Prompt caching.md`. Mecanismo de reutilización de prefijos de prompt procesados por la API.

## [2026-05-01] ingest | Vaswani 2017 — Attention is All You Need

Creada ficha `05-Fuentes/Vaswani 2017 - Attention is All You Need.md`.

## [2026-05-01] ingest | Brown 2020 — Language Models are Few-Shot Learners

Creada ficha `05-Fuentes/Brown 2020 - Language Models are Few-Shot Learners.md`.

## [2026-05-01] ingest | Yao 2022 — ReAct

Creada ficha `05-Fuentes/Yao 2022 - ReAct.md`.

## [2026-05-01] ingest | Schick 2023 — Toolformer

Creada ficha `05-Fuentes/Schick 2023 - Toolformer.md`.

## [2026-05-01] ingest | Lewis 2020 — RAG

Creada ficha `05-Fuentes/Lewis 2020 - RAG.md`.

## [2026-05-01] ingest | Liu 2023 — Lost in the Middle

Creada ficha `05-Fuentes/Liu 2023 - Lost in the Middle.md`.

## [2026-05-01] ingest | Packer 2023 — MemGPT

Creada ficha `05-Fuentes/Packer 2023 - MemGPT.md`.

## [2026-05-01] ingest | Zhong 2023 — MemoryBank

Creada ficha `05-Fuentes/Zhong 2023 - MemoryBank.md`.

## [2026-05-01] ingest | Chhikara 2025 — Mem0

Creada ficha `05-Fuentes/Chhikara 2025 - Mem0.md`.

## [2026-05-01] ingest | Tang 2025 — RAG-MCP

Creada ficha `05-Fuentes/Tang 2025 - RAG-MCP.md`.

## [2026-05-01] ingest | Yin 2026 — SimpleToolHalluBench

Creada ficha `05-Fuentes/Yin 2026 - SimpleToolHalluBench.md`.

## [2026-05-01] ingest | Maharana 2024 — LoCoMo

Creada ficha `05-Fuentes/Maharana 2024 - LoCoMo.md`.

## [2026-05-01] ingest | Wu 2024 — LongMemEval

Creada ficha `05-Fuentes/Wu 2024 - LongMemEval.md`.

## [2026-05-01] schema | Actualizado Terminos por expandir y Catalogo de fuentes

- `99-Inbox/Terminos por expandir.md` actualizado: todos los términos expandidos ahora tienen su página y están enlazados.
- `05-Fuentes/Catalogo inicial de fuentes.md` actualizado con enlaces a las fichas individuales.

## [2026-05-01] ingest | Bases Teoricas desde DOC-11

Creada `02-Marco-Teorico/Bases Teoricas.md` con 7 bloques temáticos completos extraídos de DOC-11:
Bloque 1 LLMs, Bloque 2 Agentes ReAct, Bloque 3 MCP, Bloque 4 Context rot (evidencia empírica), Bloque 5 Técnicas de memoria, Bloque 6 Tool gating, Bloque 7 Evaluación y benchmarks. Incluye tabla de overhead de tokens (4K/12K/20K) y cadena causal completa.

## [2026-05-01] ingest | Realidad Problematica desde DOC-06

Creada `01-Tesis/Realidad Problematica.md` con cifras de mercado (80% crecimiento IA, $37B gasto 2025, 92% Fortune 500), tres mecanismos de context rot con evidencia empírica, y la brecha de investigación que justifica la tesis.

## [2026-05-01] ingest | Marco Referencial desde DOC-02

Creada `02-Marco-Teorico/Marco Referencial.md` con 6 categorías de fuentes (A-F): papers fundacionales, memoria, RAG, benchmarks, protocolos, herramientas. Criterios de inclusión y notas metodológicas.

## [2026-05-01] expand | Context rot — enriquecimiento con DOC-11

Enriquecida `04-Conceptos/A-Problema/Context rot.md` con tabla de evidencia empírica completa (Liu −40%, Shi −65%, Chroma >30%, Redis 67%, Tang +23%), referencia al umbral HG, y nota sobre detección con PELT.

## [2026-05-01] expand | Tool gating — enriquecimiento con DOC-11

Enriquecida `04-Conceptos/C-Mitigacion/Tool gating.md` con tabla de overhead de tokens por nº de servidores, resultados de Tang et al. (−68% tokens, >95% exactitud), hipótesis HE3 con TOST.

## [2026-05-01] expand | SessionFacts — enriquecimiento con DOC-11

Enriquecida `04-Conceptos/C-Mitigacion/SessionFacts.md` con evidencia de Packer 2023 (−70% tokens historial en MemGPT), hipótesis HE2, contenido estándar de una SessionFact, e indicadores de evaluación.

## [2026-05-01] expand | MemoryBank — enriquecimiento con DOC-11

Enriquecida `04-Conceptos/C-Mitigacion/MemoryBank.md` con evidencia de Hu 2023 (+37% coherencia en 500 turnos), hipótesis HE4, mecanismo de recuperación paso a paso, tabla comparativa vs. SessionFacts.

## [2026-05-01] expand | RAG-MCP — enriquecimiento con DOC-11

Enriquecida `04-Conceptos/C-Mitigacion/RAG-MCP.md` con tabla de resultados Tang 2025 (−68% tokens, <2% pérdida), arquitectura de flujo de recuperación, tabla comparativa RAG-MCP vs. RAG de historial.

## [2026-05-01] schema | Cap 2 actualizado — secciones 2.2 y 2.4

`00-Mapa/Cap 2 - Marco Teorico.md` actualizado:
- Sección 2.2 ahora apunta a [[Bases Teoricas]] (antes: [[Mapa del marco teorico]])
- Sección 2.4 ahora apunta a [[Marco Referencial]] (antes: [[Catalogo inicial de fuentes]])
- Añadidos datos empíricos clave junto a cada técnica del Bloque 4

## [2026-05-02] ingest | Hipótesis de investigación desde DOC-13

Reescrita `01-Tesis/Hipotesis de investigacion.md` con contenido completo de DOC-13:
HG + HG₀ con umbral del 30% (referencia Chroma 2025). HE1–HE5 con hipótesis nulas, criterios de verificación, pruebas estadísticas específicas (Wilcoxon, ANOVA+Tukey, TOST, factorial, PELT+bootstrap). Tabla de correspondencia hipótesis-problemas-objetivos. Nivel de significancia α=0.05, potencia 1-β=0.80.

## [2026-05-02] ingest | Diseño Metodológico desde DOC-14

Reescrito `03-Metodologia/Diseno metodologico.md` con contenido completo de DOC-14:
Enfoque cuantitativo, diseño experimental puro, nivel explicativo-causal, tipo aplicada. Unidad de análisis: turno de conversación. Muestra: 200 conv./grupo (LongMemEval 100 + LoCoMo 50 + sintéticos 50). Agente: Claude Sonnet 4.5 temperatura=0.0. 6 fases experimentales detalladas. Tabla de técnicas e instrumentos (ChromaDB, RedisVL, MLflow, BERTScore, ruptures). Aspectos éticos.

## [2026-05-02] ingest | Problema e Hipótesis desde DOC-07 y DOC-09

Reescritas `01-Tesis/Problema de investigacion.md` y `01-Tesis/Objetivos de investigacion.md` con contenido completo de DOC-07 y DOC-09 respectivamente. Incluyen PG/PE1–PE5 con enunciados formales, variables (VI, VD, control, moderadoras), y OG/OE1–OE5 con verbos de acción, actividades clave y entregables.

## [2026-05-02] ingest | Aspectos Administrativos desde DOC-15

Reescrita `01-Tesis/Aspectos Administrativos.md` con presupuesto completo (USD 354.09 / S/. 1,327.84 en 11 ítems) y cronograma Gantt detallado julio 2025–junio 2026 (4 fases, 17 actividades).

## [2026-05-02] ingest | Matriz de Consistencia desde DOC-16

Reescrita `03-Metodologia/Matriz de consistencia.md` con la matriz completa extraída de DOC-16: 6 filas (PG + PE1–PE5), cada una con problema, objetivo, hipótesis, VI, VD, indicadores de medición y metodología estadística. Tabla de resumen de correspondencia al final.

## [2026-05-02] ingest | Caso Vercel 2025 — d0 Agent Tool Removal

Creada ficha `05-Fuentes/Vercel 2025 - d0 Agent Tool Removal.md`: blog post técnico de Vercel (diciembre 2025) documentando la eliminación del 80% de las herramientas del agente d0. Métricas: tasa de éxito 80%→100%, −37% tokens, 3.5× velocidad, −42% pasos. Distinción clave: reducción estática (Vercel) vs. filtrado dinámico RAG-MCP (tesis).

## [2026-05-02] expand | Tool overload — evidencia de producción Vercel

Enriquecida `04-Conceptos/A-Problema/Tool overload.md` con tabla de evidencia empírica (Patil 2023, Tang 2025, Vercel 2025) y nota sobre la distinción entre reducción estática y filtrado dinámico.

## [2026-05-02] expand | Antecedentes — caso Vercel como antecedente de industria

Enriquecida `02-Marco-Teorico/Antecedentes.md`: añadido párrafo de Vercel 2025 en la sección "Antecedentes sobre filtrado de herramientas", con referencia a la ficha y nota sobre la distinción estático/dinámico.

## [2026-05-02] expand | Realidad Problemática — Vercel como tercer caso de evidencia

Enriquecida `01-Tesis/Realidad Problematica.md`: añadido Vercel 2025 como cuarto punto en la lista de evidencia empírica (junto a Chroma, Redis Labs, Tang et al.).

## [2026-05-02] schema | Catálogo de fuentes actualizado — Categoría G

`05-Fuentes/Catalogo inicial de fuentes.md` actualizado: añadida nueva sección "Casos de producción" con entrada para Vercel 2025.

## [2026-05-02] ingest | DOC-02, DOC-06, DOC-11 actualizados con caso Vercel

Actualizados tres documentos Word del directorio `investigación/`:
- `DOC-06_Realidad_Problematica.docx`: añadido párrafo de Vercel en evidencia empírica y referencia APA.
- `DOC-11_Bases_Teoricas.docx`: añadido párrafo en Bloque 4 (evidencia context rot) y nota estático/dinámico en Bloque 6 (tool gating), más referencia APA.
- `DOC-02_Catalogo_Fuentes.docx`: añadida Categoría G (Casos de Producción) con tabla G-01 Vercel 2025.

---

## [2026-05-03] ingest | Zhou 2026 y Gartner 2025 — vault completo

Ingresadas dos nuevas fuentes al vault:

**Zhou et al. (2026) — Externalization in LLM-Based Agents (arXiv:2604.08224)**
- Creada ficha `05-Fuentes/Zhou 2026 - Externalization in LLM Agents.md` con referencia APA, taxonomía de externalización (memoria/skills/protocolos/harness) y dos citas clave.
- Añadido Bloque 8 "Harness Engineering como Marco Unificador" en `02-Marco-Teorico/Bases Teoricas.md`.
- Añadida sección "Antecedentes sobre marcos teóricos unificadores" en `02-Marco-Teorico/Antecedentes.md`.
- Añadida sección "Marcos teóricos unificadores" en `05-Fuentes/Catalogo inicial de fuentes.md`.

**Gartner (2025) — Over 40% of Agentic AI Projects Will Be Canceled by 2027**
- Creada ficha `05-Fuentes/Gartner 2025 - Agentic AI Projects Cancellation.md` con nota de uso correcto (no citar como evidencia directa de context rot).
- Añadido bullet Gartner en cifras clave de `01-Tesis/Realidad Problematica.md`.
- Añadida sección "Fuentes institucionales" en `05-Fuentes/Catalogo inicial de fuentes.md`.

## [2026-05-03] ingest | DOC-02, DOC-06, DOC-11 actualizados con Zhou 2026 y Gartner 2025

Actualizados documentos Word del directorio `investigación/`:
- `DOC-11_Bases_Teoricas.docx`: añadido Bloque 8 "Harness Engineering como Marco Unificador" antes de Referencias (tabla de 4 capas de externalización, cita directa de Zhou, posicionamiento de la tesis) + referencia APA de Zhou al final. Total: 262 párrafos.
- `DOC-06_Realidad_Problematica.docx`: añadido párrafo con predicción Gartner (2025) después del párrafo Databricks + referencia APA de Gartner. Total: 99 párrafos.
- `DOC-02_Catalogo_Fuentes.docx`: añadidas Categoría H (Marcos Teóricos Unificadores, H-01 Zhou 2026) y Categoría I (Fuentes Institucionales, I-01 Gartner 2025) antes de Categoría G. Total: 463 párrafos.
