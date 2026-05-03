# Bases Teóricas

→ Sección 2.2 del capítulo [[Cap 2 - Marco Teorico]]
Fuente: `DOC-11_Bases_Teoricas.docx`

Las bases teóricas organizan el fundamento conceptual en **siete bloques temáticos** que siguen el orden lógico de construcción de la problemática: desde los fundamentos del modelo hasta las técnicas de mitigación y los instrumentos de medición.

---

## Bloque 1 — Modelos de Lenguaje de Gran Escala

→ [[Modelo de lenguaje de gran escala]]

Los [[Modelo de lenguaje de gran escala|LLMs]] son sistemas de IA entrenados sobre vastos corpus de texto mediante predicción del siguiente token (*next-token prediction*). Su arquitectura subyacente es el **transformer** (Vaswani et al., 2017), que introdujo el mecanismo de **atención multi-cabezal** (*multi-head self-attention*) como alternativa a las redes recurrentes.

Los LLM modernos — GPT (Brown et al., 2020), LLaMA (Touvron et al., 2023), Gemini (Anil et al., 2023), Claude (Anthropic, 2024) — escalan esta arquitectura a miles de millones de parámetros y aplican RLHF para alinear el comportamiento con las preferencias del usuario.

**La ventana de contexto** → [[Ventana de contexto]]

Los modelos actuales van desde 128,000 tokens (Claude Sonnet 4.5) hasta 1,000,000 tokens (Gemini 1.5 Pro). Sin embargo, la capacidad nominal no equivale a atención uniforme: **Liu et al. (2023) demostraron que los LLMs exhiben sesgo de posición que reduce la atención efectiva sobre los tokens ubicados en el centro de contextos largos** — el efecto [[Lost in the middle]]. Esto ocurre con independencia del tamaño de la ventana.

**Capacidades de razonamiento y limitaciones**

Los LLMs tienen capacidades emergentes de razonamiento en cadena (*chain-of-thought*; Wei et al., 2022) que son la base de los sistemas agentes. Pero presentan tres limitaciones estructurales relevantes para la tesis:
1. Su conocimiento está congelado en la fecha de corte del entrenamiento.
2. No tienen acceso nativo a herramientas externas.
3. Su comportamiento en contextos muy largos se degrada.

---

## Bloque 2 — Agentes LLM y Marcos de Razonamiento-Acción

→ [[Agente LLM]]

Un **agente LLM** es un sistema de software que utiliza un LLM como motor de razonamiento y lo combina con la capacidad de ejecutar acciones — llamadas a herramientas, búsquedas, ejecución de código, interacciones con APIs — para completar tareas que van más allá de la generación de texto estático (Wang et al., 2024).

**El marco ReAct** (Yao et al., 2022)

ReAct (*Reasoning and Acting*) formalizó el ciclo del agente:
1. **Pensamiento** — razona sobre el estado actual
2. **Acción** — especifica la herramienta y sus parámetros
3. **Observación** — incorpora el resultado al contexto

Cada ciclo **acumula tokens en el contexto**: pensamientos intermedios, llamadas a herramientas y sus resultados se concatenan al historial. Esta acumulación es el mecanismo directo que produce el [[Context rot]] en conversaciones largas.

**Toolformer** (Schick et al., 2023)

Demostró que los LLMs pueden aprender a usar herramientas de forma autónoma mediante autoentrenamiento. Estableció el precedente para el *function calling* de OpenAI (2023) y el [[Model Context Protocol]] de Anthropic (2024).

**Arquitecturas multi-agente**

Aunque la tesis se enfoca en agentes individuales conectados a múltiples servidores MCP, los principios de gestión de contexto son transferibles a arquitecturas multi-agente (Hong et al., 2023).

---

## Bloque 3 — Model Context Protocol

→ [[Model Context Protocol]] · [[Servidor MCP]]

El MCP fue publicado por Anthropic en **noviembre de 2024** como estándar abierto para integrar agentes LLM con herramientas y fuentes de datos externas. La motivación: resolver la fragmentación de integraciones ad hoc donde cada herramienta requería código de integración específico.

**Arquitectura cliente-servidor**

- El **servidor MCP** expone herramientas (*tools*), recursos (*resources*) y prompts mediante esquema JSON estandarizado.
- El **cliente MCP** (el agente) negocia capacidades en la inicialización y recibe el catálogo completo de herramientas.

**Flujo estándar**: inicialización → `tools/list` → `tools/call` → `notifications/tools/list_changed`

**Impacto sobre el contexto — el dato clave**

> En la implementación estándar de MCP, el cliente recibe y **mantiene en el contexto del modelo las descripciones completas de todas las herramientas** de todos los servidores conectados.

Para un servidor típico con 20 herramientas × 200 tokens/herramienta = **4,000 tokens** solo del catálogo. En arquitecturas multi-servidor con 3–5 servidores MCP:

| Servidores MCP | Overhead de herramientas | % de ventana de 128K |
|---|---|---|
| 1 servidor | ~4,000 tokens | ~3% |
| 3 servidores | ~12,000 tokens | ~9% |
| 5 servidores | ~20,000 tokens | ~16% |

...y esto **antes de que el agente haya procesado una sola consulta** (Tang et al., 2025).

---

## Bloque 4 — Degradación de Contexto y Context Rot

→ [[Context rot]]

**Definición operacional**:
> *Context rot* es el proceso de degradación progresiva y acumulativa de la calidad de las respuestas de un agente LLM, medida a través de métricas cuantificables, como consecuencia del crecimiento del contexto activo en conversaciones multi-turno con acceso a múltiples servidores MCP. (DOC-11)

**Tres mecanismos en arquitecturas multi-MCP**

**1. Tool overload** → [[Tool overload]]
- Patil et al. (2023): los LLMs exhiben degradación en la selección de herramientas cuando el catálogo supera las **20 herramientas** en contexto.
- Tang et al. (2025): la tasa de alucinación en parámetros de herramientas **aumenta 23%** cuando el número de herramientas pasa de 10 a 50.

**2. Acumulación de resultados intermedios** → [[Contexto activo]]
- Liu et al. (2023): los LLMs exhiben **reducción de hasta 40%** en la utilización efectiva de información ubicada en el centro del contexto vs. los extremos.
- Los resultados de herramientas son verbosos y ocupan la región central — exactamente donde el modelo "pierde" la atención.

**3. Mezcla de estados de sesión**
- Chroma Research (2025): los agentes multi-MCP muestran tasas de error en la atribución de resultados a servidores que aumentan del **3% (1 servidor) al 18% (5 servidores)**.

**Evidencia empírica acumulada**
- Liu et al. (2023): degradación demostrada en tareas de recuperación con contextos de hasta 4,000 tokens.
- Shi et al. (2023): la presencia de información irrelevante reduce la exactitud en razonamiento **hasta un 65%**.
- **Chroma Research (2025): degradaciones superiores al 30% en la exactitud de respuestas de agentes en producción después de 50 turnos**. → Este es el umbral de referencia para la HG.
- Redis Labs (2025): el **67% del costo operativo de inferencia** en sistemas multi-herramienta se atribuye a acumulación de contexto, no a generación nueva.

---

## Bloque 5 — Técnicas de Memoria y Gestión de Contexto

**Taxonomía** (Wang et al., 2024):
- **Memoria en contexto** — historial completo en la ventana → produce context rot.
- **Memoria externa** — bases de datos vectoriales/relacionales → las técnicas evaluadas en la tesis.
- **Memoria en parámetros** — fine-tuning → fuera del alcance (requiere modificar el modelo).
- **Memoria en caché** — reutilización de estados de activación → [[Prompt caching]].

*La tesis se enfoca en memoria externa y en caché, ya que son implementables a nivel de agente sin modificar el modelo base — condición necesaria al usar APIs comerciales.*

**RAG** → [[RAG]] · [[RAG-MCP]]

Lewis et al. (2020) propusieron recuperar solo los documentos relevantes para cada consulta en lugar de mantenerlos en contexto. En agentes multi-MCP tiene dos aplicaciones:
1. **RAG de historial**: recupera los turnos pasados más relevantes vs. mantener el historial completo.
2. **RAG-MCP** (Tang et al., 2025): aplica recuperación semántica al catálogo de herramientas → expone solo las más relevantes para cada consulta.

> Tang et al. (2025): en catálogos de 128 herramientas, RAG-MCP logra **reducción del 68% en tokens de descripción con pérdida de exactitud inferior al 2%** en selección de herramientas.

**SessionFacts** → [[SessionFacts]]

Comprime el estado de sesión en una estructura clave-valor que reemplaza el historial completo por un resumen compacto. El agente invoca un paso de *summarization* que extrae entidades, hechos y restricciones relevantes.

> Packer et al. (2023 — MemGPT): **reducción de hasta el 70% en consumo de tokens de historial** con técnicas similares.

**MemoryBank** → [[MemoryBank]]

Hu et al. (2023): banco de memoria externa a largo plazo con política de olvido inspirada en la **curva de Ebbinghaus**. El peso de relevancia de cada memoria decrece exponencialmente con el tiempo desde su última recuperación.

> Hu et al. (2023): **mejora del 37% en coherencia conversacional** en simulaciones de hasta 500 turnos vs. agentes sin memoria externa.

**Semantic Caching** → [[Caching semantico]]

Reutiliza respuestas previas para consultas semánticamente equivalentes (similitud coseno > umbral, típicamente 0.92–0.95 en RedisVL). No reduce el context rot directamente, pero **reduce el número de invocaciones de herramientas MCP**, disminuyendo la acumulación de observaciones.

**Mem0** → [[Mem0]]

Chhikara et al. (2025): distingue entre memorias de usuario, de agente y de sesión, gestionando cada tipo con estrategias diferenciadas. Combina recuperación vectorial con grafos de conocimiento.

---

## Bloque 6 — Estrategias de Tool Gating

→ [[Tool gating]]

Las estrategias de *tool gating* controlan qué herramientas del catálogo MCP se exponen al modelo en cada turno, en lugar de exponer el catálogo completo estáticamente.

**Filtrado semántico por relevancia**

La consulta del usuario se convierte en un vector de embeddings que se compara con los embeddings de las descripciones de herramientas. Las herramientas con similitud por encima del umbral se exponen; las restantes permanecen en el catálogo pero no ocupan tokens.

> Tang et al. (2025): exposición selectiva de las **k herramientas más relevantes (k típicamente 3–10)** preserva exactitud de selección superior al 95% incluso con 128 herramientas en el catálogo total.

**Carga diferida** (*lazy loading*)

El agente razona primero sobre qué categorías de herramientas necesita, luego solicita que se carguen solo esas. Introduce latencia adicional (un ciclo extra de razonamiento) pero es especialmente adecuada para agentes conectados a servidores de dominios heterogéneos.

---

## Bloque 7 — Evaluación y Benchmarks

→ [[Dataset de evaluacion]] · [[IQCR]]

**Dimensiones de evaluación para context rot**:
1. Exactitud de respuesta vs. ground truth → [[Exactitud de respuesta]]
2. Tasa de alucinación factual → [[Tasa de alucinacion]]
3. Coherencia conversacional → [[Coherencia conversacional]]
4. Exactitud en selección de herramientas
5. Eficiencia computacional (tokens + latencia) → [[Eficiencia de tokens]] · [[Latencia p50 p95]]

**Benchmarks de referencia**

| Benchmark | Evalúa | Relevancia para la tesis |
|---|---|---|
| [[LongMemEval]] | Memoria a largo plazo, 5 tipos de recuperación | Dimensión de exactitud y memoria |
| [[LoCoMo]] | Coherencia en conversaciones de hasta 9,000 turnos | Dimensión de coherencia conversacional |
| [[SimpleToolHalluBench]] | Alucinación de herramientas en 3 dimensiones | Dimensión de tool overload |
| [[ToolHaystack]] | Selección correcta en catálogos grandes | Dimensión de tool gating |
| [[Escenarios multi-MCP sinteticos]] | Condiciones específicas multi-servidor | Validez ecológica del experimento |

**Métricas complementarias**

- **Tokens**: contadores nativos de la API de Anthropic, distinguiendo prompt tokens vs. completion tokens.
- **Latencia**: [[TTFT]] (tiempo al primer token) y latencia total de generación.
- **Coherencia**: [[BERTScore]] — similitud semántica mediante embeddings BERT (Zhang et al., 2020).

---

## Síntesis: la cadena causal

```
LLM (transformer) → ventana de contexto limitada
    ↓
Agente LLM conectado a múltiples servidores MCP (ciclo ReAct)
    ↓
Tool overload + acumulación de observaciones + mezcla de estados
    ↓
Context rot: degradación progresiva de exactitud, coherencia, tokens, latencia
    ↓
[Intervenciones evaluadas en la tesis]
RAG-MCP / Tool gating → reduce overhead de herramientas
SessionFacts / MemoryBank / Mem0 → comprime historial de sesión
Semantic Caching → reduce llamadas redundantes a herramientas
    ↓
Medición mediante IQCR + LongMemEval + LoCoMo + SimpleToolHalluBench
```

*(DOC-11 — Síntesis del Marco Teórico)*

---

## Bloque 8 — Harness Engineering como Marco Unificador

→ [[Zhou 2026 - Externalization in LLM Agents]]

Zhou et al. (2026) proponen el paradigma de **externalización** para explicar la evolución de los agentes LLM: el progreso práctico ya no depende principalmente de mejorar los pesos del modelo sino de reorganizar la infraestructura que lo rodea.

Las capacidades se externalizan en cuatro capas:

| Capa | Qué externaliza | Ejemplo en la tesis |
|---|---|---|
| Memoria | Estado a lo largo del tiempo | [[SessionFacts]], [[MemoryBank]], [[Mem0]] |
| Skills | Conocimiento procedural | Prompts de sistema, documentación |
| Protocolos | Estructura de interacción | [[Model Context Protocol]] |
| Harness | Coordinación gobernada de todas las capas | La arquitectura experimental de la tesis |

> *"Memory externalizes state across time, skills externalize procedural expertise, protocols externalize interaction structure, and harness engineering serves as the unification layer that coordinates them into governed execution."* (Zhou et al., 2026)

**Posicionamiento de la tesis**: el presente estudio contribuye al paradigma de externalización generando evidencia empírica cuantitativa sobre qué combinaciones de capas de memoria y protocolo minimizan el [[Context rot]] en escenarios multi-MCP. Los resultados informan el diseño de harnesses efectivos para entornos multi-servidor.

---

## Referencias clave de este bloque

- [[Vaswani 2017 - Attention is All You Need]] — arquitectura transformer
- [[Brown 2020 - Language Models are Few-Shot Learners]] — LLMs a escala
- [[Yao 2022 - ReAct]] — ciclo razonamiento-acción
- [[Schick 2023 - Toolformer]] — uso autónomo de herramientas
- [[Lewis 2020 - RAG]] — recuperación aumentada
- [[Liu 2023 - Lost in the Middle]] — degradación por posición
- [[Packer 2023 - MemGPT]] — memoria virtual para LLMs
- [[Zhong 2023 - MemoryBank]] — memoria con olvido adaptativo
- [[Zhou 2026 - Externalization in LLM Agents]] — marco unificador de externalización
- [[Chhikara 2025 - Mem0]] — memoria adaptativa por tipo
- [[Tang 2025 - RAG-MCP]] — tool gating semántico
- [[Wu 2024 - LongMemEval]] — benchmark de memoria
- [[Maharana 2024 - LoCoMo]] — benchmark de coherencia
- [[Yin 2026 - SimpleToolHalluBench]] — benchmark de alucinación de herramientas
