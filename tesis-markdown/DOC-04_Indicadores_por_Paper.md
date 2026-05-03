# DOC-04 — Indicadores y Métricas por Paper

> **Tipo:** Analítico  
> **Descripción:** Tabla comparativa de métricas usadas en cada referencia bibliográfica.

---

**PROYECTO DE TESIS — DOCUMENTO 04**

**INDICADORES Y MÉTRICAS POR PAPER / PROYECTO**

*Análisis sistemático de las métricas utilizadas en cada fuente y su muestra experimental*

**1. Propósito y criterios**

Este documento cataloga los indicadores y métricas empleados en cada paper o proyecto de referencia, especificando: nombre del indicador, definición técnica, valor o resultado reportado, unidad de medida y si el trabajo incluye una muestra o dataset experimental. Al final se incluye una tabla consolidada de todos los indicadores únicos con su relevancia directa para el diseño experimental de la tesis.

Criterio de inclusión de indicadores: se incluye todo indicador que mida calidad de respuesta, uso de herramientas, capacidad de memoria, costo computacional (tokens, latencia) o degradación de contexto. Se excluyen métricas internas de entrenamiento (loss, perplexidad de entrenamiento) salvo cuando son reportadas como resultado de evaluación.

**2. Indicadores por paper**

**Categoría A: Papers Fundacionales**

<table>
<tbody>
<tr class="odd">
<td><p><strong>A01</strong></p>
<p>2022 / ICLR 2023</p></td>
<td><strong>ReAct: Synergizing Reasoning and Acting in Language Models</strong></td>
<td><em>Yao et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> 4 benchmarks estándar: HotPotQA (1 K preguntas multi-hop), Fever (1 K afirmaciones), ALFWorld (134 juegos de texto), WebShop (200 instrucciones de compra). Todos conjuntos de test públicos.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Exact Match (EM)</strong></td>
<td>Coincidencia exacta entre la respuesta generada y la respuesta gold.</td>
<td>66.6% (ReAct) vs 60.5% (CoT) en HotPotQA</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>F1 Score</strong></td>
<td>Media armónica de precisión y recall a nivel token.</td>
<td>Reportado por benchmark (HotPotQA)</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Accuracy (Fever)</strong></td>
<td>Porcentaje de afirmaciones correctamente clasificadas como SUPPORTS / REFUTES.</td>
<td>80% (ReAct)</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Success Rate (ALFWorld)</strong></td>
<td>Porcentaje de juegos completados con éxito.</td>
<td>71% (ReAct) vs 45% (Act-only)</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Success Rate (WebShop)</strong></td>
<td>Porcentaje de instrucciones de compra completadas satisfactoriamente.</td>
<td>40% (ReAct)</td>
<td>%</td>
</tr>
<tr class="odd">
<td><strong>Notas</strong></td>
<td><em>No reporta métricas de costo de tokens ni latencia. Métricas de calidad de respuesta puras.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>A02</strong></p>
<p>2023 / NeurIPS 2023</p></td>
<td><strong>Toolformer: Language Models Can Teach Themselves to Use Tools</strong></td>
<td><em>Schick et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> 5 herramientas (calculadora, Q&amp;A, 2 motores de búsqueda, traducción, calendario). Evaluado en 5 benchmarks zero-shot: LAMA, ARC, PIQA, NLI, SocialIQA. Modelos base: GPT-J (6.7B), OPT (6.7B).</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Accuracy (zero-shot)</strong></td>
<td>Precisión en cada benchmark sin ejemplos de entrenamiento específicos.</td>
<td>Supera a GPT-3 (175B) en LAMA, ARC, NLI con un modelo 25x más pequeño</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Perplexity (language modeling)</strong></td>
<td>Calidad del modelado de lenguaje para verificar que el uso de tools no degrada la capacidad base.</td>
<td>Sin degradación significativa respecto al modelo base</td>
<td>perplexity</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Tool call rate</strong></td>
<td>Porcentaje de tokens donde el modelo decide invocar una herramienta.</td>
<td>Aprendido automáticamente; varía por tarea</td>
<td>%</td>
</tr>
<tr class="odd">
<td><strong>Notas</strong></td>
<td><em>Pionero en métricas de tool call rate como indicador de eficiencia. No reporta latencia ni costo de tokens.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

**Categoría B: Memoria en LLMs**

<table>
<tbody>
<tr class="odd">
<td><p><strong>B01</strong></p>
<p>2023</p></td>
<td><strong>MemGPT: Towards LLMs as Operating Systems</strong></td>
<td><em>Packer et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> 2 dominios de evaluación: (1) análisis de documentos multi-parte (MemGPT vs. GPT-4 con contexto largo) con datasets de QA sobre documentos extensos; (2) conversación multi-sesión con un asistente personal simulado en 5 sesiones de 30 turnos cada una.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>QA Accuracy (multi-doc)</strong></td>
<td>Precisión en preguntas que requieren información de múltiples partes de un documento que excede la ventana de contexto.</td>
<td>MemGPT: 75.8% vs GPT-4 fixed context: 52.1%</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Consistency score (multi-session)</strong></td>
<td>Evaluación humana de coherencia entre sesiones consecutivas.</td>
<td>Mejora significativa sobre baseline sin memoria.</td>
<td>Escala 1–5 (evaluadores humanos)</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Context window utilization</strong></td>
<td>Uso eficiente de la ventana de contexto mediante paginación de memoria.</td>
<td>Permite operar sobre documentos 10x mayores que la ventana.</td>
<td>Ratio de extensión</td>
</tr>
<tr class="odd">
<td><strong>Notas</strong></td>
<td><em>Métricas de evaluación humana + automáticas. Sin reporte explícito de costo de tokens.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>B02</strong></p>
<p>2023 / AAAI 2024</p></td>
<td><strong>MemoryBank: Enhancing Large Language Models with Long-Term Memory</strong></td>
<td><em>Zhong et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> Dataset de conversaciones de SiliconFriend (asistente de IA compañero) con usuarios reales. Evaluación en conversaciones de hasta 30 sesiones. Modelo base: ChatGLM-6B. Anotadores humanos para evaluación cualitativa.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Memory Recall Rate</strong></td>
<td>Porcentaje de hechos del usuario correctamente recuperados cuando son relevantes.</td>
<td>Mejora de ~35% sobre baseline sin memoria</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Empathy Score</strong></td>
<td>Evaluación humana de la empatía percibida en las respuestas del asistente.</td>
<td>4.2/5 con MemoryBank vs 3.1/5 sin memoria</td>
<td>Escala 1–5</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Consistency Score</strong></td>
<td>Coherencia de las respuestas con información previa del usuario.</td>
<td>4.0/5 con MemoryBank vs 2.8/5 sin memoria</td>
<td>Escala 1–5</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Forgetting curve compliance</strong></td>
<td>Qué tan bien el mecanismo de olvido imita la curva de Ebbinghaus (retención de memorias importantes, olvido de triviales).</td>
<td>Reportado cualitativamente</td>
<td>Cualitativo</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>Combina métricas automáticas y evaluación humana. Sin métricas de costo de tokens ni latencia.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>B03</strong></p>
<p>2025</p></td>
<td><strong>Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory</strong></td>
<td><em>Chhikara et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> Benchmark LOCOMO y benchmark propietario de Mem0 (público en mem0.ai/research). Comparación contra: OpenAI Assistants API, full context, RAG, y otros sistemas de memoria. Dataset de conversaciones multi-sesión con ground truth de preferencias y hechos.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>LLM-as-a-Judge score</strong></td>
<td>Evaluación de la calidad de respuesta usando un LLM juez (GPT-4o) comparando respuesta generada vs. respuesta de referencia.</td>
<td>+26% relativo vs. OpenAI Assistants API</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Latencia p95</strong></td>
<td>Percentil 95 del tiempo de respuesta end-to-end.</td>
<td>91% de reducción vs. baseline de contexto completo</td>
<td>ms</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Costo de tokens (input)</strong></td>
<td>Tokens consumidos en el prompt por consulta.</td>
<td>&gt;90% de reducción vs. full context baseline</td>
<td>tokens</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Memory precision</strong></td>
<td>Precisión de los hechos almacenados en memoria (sin duplicados ni contradicciones).</td>
<td>Reportado en benchmark público</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Memory recall</strong></td>
<td>Porcentaje de hechos relevantes correctamente recuperados cuando son necesarios.</td>
<td>Reportado en benchmark público</td>
<td>%</td>
</tr>
<tr class="odd">
<td><strong>Notas</strong></td>
<td><em>El paper con las métricas económicas (tokens, latencia) más explícitas de la categoría. Benchmarks reproducibles públicamente.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>B04</strong></p>
<p>2025 / COLING 2025</p></td>
<td><strong>CarMem: Enhancing Long-Term Memory in LLM Voice Assistants through Category-Bounding</strong></td>
<td><em>Kirmayr et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> Dataset CarMem sintético multi-turno y multi-sesión, basado en datos industriales de asistentes en automóvil. Dataset público. Evaluado en 4 categorías de preferencias de usuario (música, temperatura, navegación, entretenimiento).</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Preference extraction F1</strong></td>
<td>F1 en la extracción correcta de preferencias del usuario desde la conversación.</td>
<td>Reportado por categoría</td>
<td>F1 (0–1)</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Redundancy rate</strong></td>
<td>Porcentaje de preferencias almacenadas que son duplicadas o redundantes.</td>
<td>Reducción significativa vs. memoria no categorizada</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Contradiction rate</strong></td>
<td>Porcentaje de pares de preferencias almacenadas que se contradicen entre sí.</td>
<td>Reducción significativa vs. baseline</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Category hit rate</strong></td>
<td>Porcentaje de preferencias correctamente asignadas a su categoría predefinida.</td>
<td>Reportado por categoría</td>
<td>%</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>Introduce métricas de calidad de la memoria (redundancia y contradicción) que son directamente aplicables a la tesis. Dataset público.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

**Categoría C: Recuperación (RAG)**

<table>
<tbody>
<tr class="odd">
<td><p><strong>C01</strong></p>
<p>2023 / ICLR 2024</p></td>
<td><strong>Self-RAG: Learning to Retrieve, Generate and Critique through Self-Reflection</strong></td>
<td><em>Asai et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> 6 benchmarks públicos: PopQA (open-domain QA), TriviaQA-unfiltered, PubHealth (health fact-checking), ARC-Challenge, ASQA (long-form QA), FactScore (biography generation). Modelo base: Llama2 7B y 13B fine-tuned.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Accuracy / EM (QA)</strong></td>
<td>Exactitud en preguntas de respuesta corta (exact match o accuracy).</td>
<td>Self-RAG 7B supera a ChatGPT en PopQA (54.9% vs 50.8%) y TriviaQA</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>FactScore</strong></td>
<td>Precisión de afirmaciones factuales en texto generado, evaluadas contra una base de conocimiento.</td>
<td>Self-RAG 13B: 70.8% vs ChatGPT: 52.0%</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>MAUVE (fluency)</strong></td>
<td>Medida de fluidez y naturalidad del texto generado.</td>
<td>Comparable a modelos base</td>
<td>0–1</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Retrieval frequency</strong></td>
<td>Porcentaje de tokens donde el modelo decide recuperar pasajes (indicador de selectividad).</td>
<td>Varía por tarea: más frecuente en QA, menos en generación simple</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Citation accuracy</strong></td>
<td>Porcentaje de afirmaciones correctamente respaldadas por pasajes recuperados.</td>
<td>Mejora significativa vs. RAG estándar</td>
<td>%</td>
</tr>
<tr class="odd">
<td><strong>Notas</strong></td>
<td><em>Introduce el token de reflexión como indicador de comportamiento del modelo. Sin métricas de tokens ni latencia.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>C02</strong></p>
<p>2025</p></td>
<td><strong>RAG-MCP: Mitigating Prompt Bloat in LLM Tool Selection via RAG</strong></td>
<td><em>Gan &amp; Sun</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> MCP stress test con catálogos de herramientas de tamaño creciente (10, 50, 100, 200 tools). Dataset de consultas de evaluación con ground truth de tool correcta. Comparación directa: RAG-MCP vs. exposición total de tools.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Tool selection accuracy</strong></td>
<td>Porcentaje de consultas donde el modelo selecciona la herramienta correcta del catálogo.</td>
<td>43.13% (RAG-MCP) vs 13.62% (baseline, todas las tools)</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Prompt token reduction</strong></td>
<td>Reducción porcentual en el número de tokens del prompt al usar recuperación semántica de tools.</td>
<td>&gt;50% de reducción</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Retrieval precision@k</strong></td>
<td>Precisión de las k tools recuperadas semánticamente en relación con la tool correcta.</td>
<td>Reportado para k=1, k=3</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Accuracy vs. catálogo size</strong></td>
<td>Degradación de la precisión conforme crece el número de tools en el catálogo (curva de escalado).</td>
<td>Sin RAG: degrada fuertemente. Con RAG-MCP: se mantiene estable.</td>
<td>%</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>El paper con los indicadores más directamente relevantes para la tesis. Métricas económicas (tokens) explícitas.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>C03</strong></p>
<p>2024</p></td>
<td><strong>From Local to Global: A Graph RAG Approach to Query-Focused Summarization</strong></td>
<td><em>Edge et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> 2 corpora: noticias de podcasts (HackerNews) y artículos académicos de arXiv. Evaluación con consultas de nivel global (requieren síntesis de múltiples documentos) y local (sobre entidades específicas). Jueces LLM para comparación.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Comprehensiveness</strong></td>
<td>Evaluación de la exhaustividad de la respuesta generada, medida por LLM juez.</td>
<td>GraphRAG supera RAG vector en 77% de comparaciones directas</td>
<td>Win rate (%)</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Diversity</strong></td>
<td>Variedad de perspectivas o fuentes integradas en la respuesta.</td>
<td>GraphRAG supera en 90% de comparaciones directas</td>
<td>Win rate (%)</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Empowerment</strong></td>
<td>Utilidad percibida de la respuesta para tomar decisiones informadas.</td>
<td>GraphRAG supera en 72% de comparaciones</td>
<td>Win rate (%)</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Indexing token cost</strong></td>
<td>Costo en tokens para construir el grafo de conocimiento.</td>
<td>Extremadamente alto (el repo advierte). Varía según corpus.</td>
<td>tokens (costo USD reportado)</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>Métricas basadas en evaluación relativa con LLM juez. El paper reporta explícitamente el costo de indexado como limitación.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

**Categoría D: Benchmarks de Evaluación**

<table>
<tbody>
<tr class="odd">
<td><p><strong>D01</strong></p>
<p>2024</p></td>
<td><strong>ToolBeHonest: A Multi-level Hallucination Diagnostic Benchmark</strong></td>
<td><em>Zhang et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> 700 muestras de evaluación en 7 tareas, generadas con anotación manual en múltiples rondas. Modelos evaluados: GPT-4o, Gemini-1.5-Pro, Claude-3, Llama-3, Mistral, Qwen entre otros (&gt;10 modelos).</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Solvability Detection score</strong></td>
<td>Capacidad del modelo para detectar si una tarea es resoluble con las tools disponibles (incluyendo el caso de tools faltantes).</td>
<td>GPT-4o: 37.0/100; Gemini-1.5-Pro: 45.3/100</td>
<td>Puntuación 0–100</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Solution Planning score</strong></td>
<td>Calidad del plan de uso de herramientas generado por el modelo.</td>
<td>Reportado por nivel de dificultad</td>
<td>Puntuación 0–100</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Missing-tool hallucination rate</strong></td>
<td>Tasa con la que el modelo inventa o reutiliza incorrectamente una tool cuando la necesaria está ausente.</td>
<td>Alta en todos los modelos evaluados</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Tool distractor error rate</strong></td>
<td>Tasa de selección de tools distractoras en lugar de la correcta.</td>
<td>Aumenta con el número de distractores</td>
<td>%</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>Benchmark de referencia para medir error de selección de tools. Aplicable directamente a la Fase 2 del experimento de la tesis.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>D02</strong></p>
<p>2025</p></td>
<td><strong>ToolHaystack: Stress-Testing Tool-Augmented LLMs in Long-Term Interactions</strong></td>
<td><em>No publicado completamente</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> 14 agentes LLM evaluados (modelos estado del arte incluyendo GPT-4, Claude, Gemini, Llama series). Conversaciones de hasta N turnos con tareas intercaladas y distractores. Dataset sintético con flujos de tareas compuestos.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Task completion rate (long context)</strong></td>
<td>Porcentaje de tareas completadas correctamente en conversaciones largas.</td>
<td>Degrada significativamente vs. conversaciones cortas en todos los modelos</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Distractor sensitivity</strong></td>
<td>Caída de rendimiento al insertar tareas distractoras intercaladas.</td>
<td>Alta sensibilidad incluso en modelos top</td>
<td>Δ% de accuracy</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Long-term dependency accuracy</strong></td>
<td>Precisión en tareas que requieren información de turnos anteriores (dependencia de largo alcance).</td>
<td>Cae con el número de turnos intermedios</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Consistency score</strong></td>
<td>Coherencia de las respuestas a lo largo de la conversación.</td>
<td>Degrada progresivamente con la longitud</td>
<td>%</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>Benchmark directamente relevante para medir context rot en escenarios multi-tool. Curvas de degradación por longitud de contexto.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>D03</strong></p>
<p>2025</p></td>
<td><strong>The Reasoning Trap: How Enhancing LLM Reasoning Amplifies Tool Hallucination</strong></td>
<td><em>No publicado completamente</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> Benchmark SimpleToolHalluBench con 2 escenarios: (A) ninguna tool disponible (el modelo debe abstenerse) y (B) solo tools distractoras disponibles (el modelo debe detectar que ninguna sirve). Múltiples modelos base + variantes con RL.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Hallucination rate (no-tool)</strong></td>
<td>Tasa con la que el modelo inventa una tool o llama a una inexistente cuando ninguna está disponible.</td>
<td>Aumenta con el nivel de razonamiento reforzado</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Hallucination rate (distractor-only)</strong></td>
<td>Tasa de selección incorrecta cuando solo hay tools distractoras.</td>
<td>Aumenta con RL training</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Utility score</strong></td>
<td>Utilidad de la respuesta final para el usuario (medida con LLM juez).</td>
<td>Cae cuando se mitiga la alucinación</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Reasoning depth vs. hallucination</strong></td>
<td>Correlación entre profundidad de razonamiento (pasos) y tasa de alucinación de tools.</td>
<td>Correlación positiva: más razonamiento → más alucinación de tools</td>
<td>Correlación r</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>Documenta el trade-off precisión/alucinación en tool use. Relevante para justificar técnicas de gating que no dependan solo del razonamiento del modelo.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>D04</strong></p>
<p>2024 / ICLR 2025</p></td>
<td><strong>LongMemEval: Benchmarking Chat Assistants on Long-Term Interactive Memory</strong></td>
<td><em>Wu et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> 500 preguntas curadas embebidas en historiales de conversación de 115K tokens (LongMemEval-S) y hasta 1.5M tokens (LongMemEval-M). 5 tipos de preguntas: extracción, razonamiento multi-sesión, razonamiento temporal, actualización de conocimiento, abstención.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Accuracy (offline reading)</strong></td>
<td>Precisión cuando el modelo lee solo la sesión con la respuesta correcta.</td>
<td>GPT-4o: ~92%</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Accuracy (full interactive)</strong></td>
<td>Precisión en modo interactivo completo con todas las sesiones.</td>
<td>GPT-4o: ~58% (caída de ~34 pp)</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Multi-session reasoning accuracy</strong></td>
<td>Precisión en preguntas que requieren integrar información de múltiples sesiones.</td>
<td>La más difícil; todos los modelos &lt;50%</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Temporal reasoning accuracy</strong></td>
<td>Precisión en preguntas que requieren razonamiento sobre cuándo ocurrió algo.</td>
<td>Moderada; mejor con time-aware query expansion</td>
<td>%</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Knowledge update accuracy</strong></td>
<td>Precisión cuando una preferencia o hecho del usuario ha cambiado entre sesiones.</td>
<td>Baja; los modelos tienden a usar el dato antiguo</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Abstention accuracy</strong></td>
<td>Tasa correcta de abstención cuando la respuesta no está en el historial.</td>
<td>Variable; tendencia a alucinación</td>
<td>%</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>Benchmark más completo para memoria longitudinal. Las 6 métricas corresponden a las 5 habilidades evaluadas. ICLR 2025.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>D05</strong></p>
<p>2024 / ACL 2024</p></td>
<td><strong>LoCoMo: Evaluating Very Long-Term Conversational Memory of LLM Agents</strong></td>
<td><em>Maharana et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> Dataset LoCoMo: conversaciones con 300 turnos promedio, ~9K tokens por sesión, hasta 35 sesiones. Generado con pipeline máquina-humano. Tareas: QA sobre el historial, resumen de eventos, generación dialógica multimodal.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>QA Accuracy (sobre historial)</strong></td>
<td>Precisión en preguntas factuales sobre eventos de la conversación pasada.</td>
<td>Modelos top &lt;60%; humanos ~90%</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Event summarization ROUGE</strong></td>
<td>Calidad del resumen de eventos de la conversación medido con ROUGE-L.</td>
<td>Reportado por modelo evaluado</td>
<td>ROUGE-L</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Temporal causality accuracy</strong></td>
<td>Precisión en preguntas que requieren entender relaciones causales en el tiempo.</td>
<td>La dimensión más difícil para todos los modelos</td>
<td>%</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>RAG improvement Δ</strong></td>
<td>Ganancia de precisión al añadir RAG sobre el historial vs. modelo base.</td>
<td>Mejora parcial; sigue muy por debajo de humanos</td>
<td>Δ%</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>Dataset más largo de conversaciones multi-sesión disponible públicamente. Referencia para diseño experimental multi-sesión de la tesis.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

**Categoría E: Frameworks / Especificaciones**

<table>
<tbody>
<tr class="odd">
<td><p><strong>E01</strong></p>
<p>Nov 2024</p></td>
<td><strong>Model Context Protocol – Especificación Oficial</strong></td>
<td><em>Anthropic</em></td>
<td><strong>✘ Sin muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> Especificación técnica. No incluye benchmarks ni experimentos empíricos.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Número de primitivos del protocolo</strong></td>
<td>Primitivos definidos para servidores (Tools, Resources, Prompts) y clientes (Roots, Sampling).</td>
<td>5 primitivos totales</td>
<td>Conteo</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Overhead de tokens por tool definition</strong></td>
<td>Costo estimado de tokens por cada definición de herramienta expuesta al modelo.</td>
<td>Documentado: decenas de miles de tokens para catálogos grandes</td>
<td>tokens</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Latencia de listChanged notification</strong></td>
<td>Tiempo de propagación de la notificación de cambio en el catálogo de tools.</td>
<td>Definido en el protocolo; depende de la implementación</td>
<td>ms</td>
</tr>
<tr class="odd">
<td><strong>Notas</strong></td>
<td><em>La especificación no es un paper experimental sino una norma técnica. Los indicadores son definiciones del protocolo, no resultados empíricos.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p><strong>E02</strong></p>
<p>2024–2025</p></td>
<td><strong>LangGraph – State Management and Agent Orchestration</strong></td>
<td><em>LangChain Team</em></td>
<td><strong>~ Parcial</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> Documentación técnica con ejemplos de uso. No publica benchmarks propios comparativos, pero LangSmith provee datos de evaluación de usuarios en producción.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Checkpoint overhead</strong></td>
<td>Latencia adicional por persistir el estado del agente en cada paso.</td>
<td>Reportado como bajo en docs; varía por backend de almacenamiento</td>
<td>ms</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Thread recovery time</strong></td>
<td>Tiempo para reanudar un hilo desde un checkpoint fallido.</td>
<td>Sub-segundo en memoria; varía con almacenamiento persistente</td>
<td>ms</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Memory store latency</strong></td>
<td>Latencia de lectura/escritura del long-term store JSON.</td>
<td>Dependiente del backend (SQLite, PostgreSQL, Redis)</td>
<td>ms</td>
</tr>
<tr class="odd">
<td><strong>Notas</strong></td>
<td><em>Framework de producción; los indicadores provienen de documentación técnica y experiencia reportada por usuarios, no de papers académicos.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

**Categoría F: Herramientas de Evaluación**

<table>
<tbody>
<tr class="odd">
<td><p><strong>E03</strong></p>
<p>2023–2025</p></td>
<td><strong>Ragas: Automated Evaluation of RAG Pipelines</strong></td>
<td><em>Es et al.</em></td>
<td><strong>✔ Con muestra</strong></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Muestra/dataset:</strong> Validado contra evaluación humana en datasets de QA (Natural Questions, TriviaQA) y datasets propios de RAG. Paper original 2023, framework en evolución continua.</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Indicadores</strong></td>
<td><strong>Nombre del indicador / métrica</strong></td>
<td><strong>Definición</strong></td>
<td><strong>Valor / resultado reportado</strong></td>
<td><strong>Unidad</strong></td>
</tr>
<tr class="even">
<td></td>
<td><strong>Context Precision</strong></td>
<td>Fracción de los chunks recuperados que son relevantes para la pregunta.</td>
<td>Correlación ~0.75 con evaluación humana en NQ</td>
<td>0–1</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Context Recall</strong></td>
<td>Fracción del ground truth cubierta por los chunks recuperados.</td>
<td>Correlación ~0.72 con evaluación humana</td>
<td>0–1</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Faithfulness</strong></td>
<td>Proporción de afirmaciones en la respuesta que están respaldadas por el contexto recuperado.</td>
<td>Correlación ~0.81 con evaluación humana</td>
<td>0–1</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Answer Relevancy</strong></td>
<td>Relevancia de la respuesta generada respecto a la pregunta original.</td>
<td>Correlación ~0.78 con evaluación humana</td>
<td>0–1</td>
</tr>
<tr class="even">
<td></td>
<td><strong>Noise Sensitivity</strong></td>
<td>Sensibilidad del sistema a la inserción de chunks ruidosos o irrelevantes.</td>
<td>Métrica diagnóstica; varía por modelo</td>
<td>0–1 (mayor = más sensible)</td>
</tr>
<tr class="odd">
<td></td>
<td><strong>Tool Call Accuracy (agentes)</strong></td>
<td>Precisión en la selección y uso de herramientas por el agente.</td>
<td>Métrica para agentes; reportado en Ragas v0.2+</td>
<td>0–1</td>
</tr>
<tr class="even">
<td><strong>Notas</strong></td>
<td><em>Suite de evaluación más completa para RAG y agentes. Las métricas son el estándar de facto para evaluar sistemas de recuperación aumentada.</em></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

**3. Tabla consolidada de indicadores para la tesis**

La siguiente tabla unifica todos los indicadores únicos identificados y su relevancia directa para el protocolo de evaluación experimental de la tesis. Los marcados como 'Directa — métrica primaria' serán las variables dependientes del experimento.

|                                           |                                                       |                                       |            |                                              |
| ----------------------------------------- | ----------------------------------------------------- | ------------------------------------- | ---------- | -------------------------------------------- |
| **Indicador / Métrica**                   | **Definición breve**                                  | **Papers de origen**                  | **Unidad** | **Relevancia para la tesis**                 |
| **Costo de tokens (input/output/cached)** | Tokens consumidos por consulta, desglosados           | Mem0, RAG-MCP, GraphRAG, OpenAI docs  | tokens     | Directa — métrica primaria de la tesis       |
| **Latencia p50 / p95**                    | Percentiles de tiempo de respuesta                    | Mem0                                  | ms         | Directa — métrica primaria de la tesis       |
| **Prompt token reduction (%)**            | Reducción de tokens al aplicar técnica                | RAG-MCP                               | %          | Directa — mide eficiencia de gating          |
| **Tool selection accuracy**               | % de selección correcta de herramienta                | RAG-MCP, ToolBH, SimpleToolHalluBench | %          | Directa — mide context rot por tools         |
| **Task completion rate**                  | % de tareas completadas en contexto largo             | ToolHaystack                          | %          | Directa — mide degradación por longitud      |
| **LLM-as-a-Judge score**                  | Calidad de respuesta evaluada por LLM juez            | Mem0, LoCoMo, LongMemEval             | %          | Directa — calidad de respuesta               |
| **Accuracy / Exact Match**                | Coincidencia con respuesta gold                       | ReAct, Self-RAG, LongMemEval, LoCoMo  | %          | Directa — precisión de respuesta             |
| **Faithfulness**                          | Respuesta respaldada por contexto recuperado          | Ragas                                 | 0–1        | Indirecta — mide context rot por alucinación |
| **Context Precision / Recall**            | Calidad del contexto recuperado                       | Ragas                                 | 0–1        | Indirecta — calidad del retrieval            |
| **Memory Recall Rate**                    | % de hechos relevantes correctamente recuperados      | MemoryBank, LongMemEval               | %          | Directa — mide eficacia de memoria LT        |
| **Redundancy rate**                       | % de memorias duplicadas o redundantes                | CarMem                                | %          | Directa — calidad de memoria categorizada    |
| **Contradiction rate**                    | % de pares de memorias contradictorias                | CarMem                                | %          | Directa — coherencia de memoria              |
| **Knowledge update accuracy**             | % de actualizaciones de hechos captadas correctamente | LongMemEval                           | %          | Directa — stale memory detection             |
| **Hallucination rate (tools)**            | % de invocaciones a tools inexistentes                | ToolBH, SimpleToolHalluBench          | %          | Directa — mide tool overload                 |
| **Missing-tool detection rate**           | % de detección correcta de tools faltantes            | ToolBH                                | %          | Directa — robustez de tool gating            |

**4. Notas sobre replicabilidad**

La mayoría de los benchmarks de evaluación (LongMemEval, LoCoMo, ToolBH, CarMem dataset) están disponibles públicamente, lo que permite replicar los experimentos y comparar los resultados de la tesis directamente con los valores reportados en la literatura. Los benchmarks de Mem0 (mem0.ai/research) también son públicos aunque desarrollados por el propio proveedor.

Para los indicadores económicos (tokens, latencia), los valores de referencia provienen principalmente de la documentación de OpenAI (Prompt Caching), Anthropic (MCP docs) y el paper de Mem0. La tesis medirá estos indicadores de forma experimental propia, lo que permitirá comparar directamente con los valores publicados.
