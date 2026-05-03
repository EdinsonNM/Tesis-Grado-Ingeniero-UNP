# Cap 2 — Marco Teórico

> Segundo capítulo. Sitúa la investigación en su contexto académico: antecedentes, bases teóricas, glosario de términos, marco referencial, hipótesis y operacionalización de variables.

← [[Cap 1 - Aspectos de la Problematica]] | → [[Cap 3 - Marco Metodologico]]

---

## 2.1 Antecedentes de la Investigación

→ [[Antecedentes]]

Los antecedentes más relevantes son trabajos que abordan el problema de la degradación de contexto y las técnicas de memoria en agentes LLM:

| Paper | Aporte |
|---|---|
| [[Yao 2022 - ReAct]] | Define el ciclo agente que produce el crecimiento del contexto |
| [[Liu 2023 - Lost in the Middle]] | Evidencia empírica del fenómeno de posición central |
| [[Packer 2023 - MemGPT]] | Primer sistema de memoria virtual para LLMs |
| [[Zhong 2023 - MemoryBank]] | Memoria externa con modelo de olvido adaptativo |
| [[Chhikara 2025 - Mem0]] | Reducción del 91% en tokens con memoria adaptativa |
| [[Tang 2025 - RAG-MCP]] | RAG aplicado al espacio de herramientas MCP |
| [[Yin 2026 - SimpleToolHalluBench]] | Benchmark de alucinación de herramientas |

---

## 2.2 Bases Teóricas

→ [[Bases Teoricas]]

La cadena causal del marco teórico:

```
LLM → Agente → multi-MCP → Contexto activo crece → Context rot
                                         ↓
                    [Técnicas de mitigación]
                    Tool gating | Memoria | RAG | Caching
```

**Bloque 1 — El LLM como motor**
- [[Modelo de lenguaje de gran escala]] — arquitectura y propiedades
- [[Ventana de contexto]] — el límite físico
- [[Lost in the middle]] — distribución no uniforme de la atención

**Bloque 2 — El agente y MCP**
- [[Agente LLM]] — ciclo ReAct de razonamiento-acción-observación
- [[Model Context Protocol]] — estándar de conexión a herramientas (publicado Nov 2024)
- [[Servidor MCP]] — fuentes del espacio de herramientas
- [[Namespaces]] — aislamiento entre servidores

**Bloque 3 — El problema**
- [[Context rot]] — el fenómeno central (>30% degradación en 50 turnos, Chroma 2025)
- [[Tool overload]] — +23% alucinación de parámetros al pasar de 10 a 50 herramientas
- [[Contexto activo]] — el componente que crece sin control

**Bloque 4 — Técnicas de mitigación**
- [[Tool gating]] + [[RAG-MCP]] — −68% tokens, <2% pérdida exactitud (Tang 2025)
- [[SessionFacts]] — −70% tokens de historial (Packer 2023)
- [[MemoryBank]] — +37% coherencia conversacional en 500 turnos (Hu 2023)
- [[Mem0]] — −91% tokens con memoria adaptativa (Chhikara 2025)
- [[Caching semantico]] + [[Prompt caching]]

---

## 2.3 Glosario de Términos

→ [[Glosario]]

Términos técnicos con definición operacional para la tesis. Ver la página completa para definiciones expandidas. Términos principales:

- [[Context rot]] — [[Tool overload]] — [[Lost in the middle]]
- [[Ventana de contexto]] — [[Contexto activo]]
- [[Tool gating]] — [[Caching semantico]] — [[Compaction]]
- [[IQCR]] — [[Exactitud de respuesta]] — [[Tasa de alucinacion]]
- [[Coherencia conversacional]] — [[Eficiencia de tokens]]
- [[Namespaces]] — [[Sharding]] — [[Hybrid retrieval]]
- [[PELT]] — [[TOST]] — [[Diseno factorial 2k]]

---

## 2.4 Marco Referencial

→ [[Marco Referencial]]

Fuentes primarias agrupadas por rol en la tesis:

**Arquitectura base**: [[Vaswani 2017 - Attention is All You Need]] · [[Brown 2020 - Language Models are Few-Shot Learners]]

**El problema**: [[Liu 2023 - Lost in the Middle]] · [[Yao 2022 - ReAct]]

**Técnicas de mitigación**: [[Lewis 2020 - RAG]] · [[Schick 2023 - Toolformer]] · [[Packer 2023 - MemGPT]] · [[Zhong 2023 - MemoryBank]] · [[Chhikara 2025 - Mem0]] · [[Tang 2025 - RAG-MCP]]

**Evaluación**: [[Wu 2024 - LongMemEval]] · [[Maharana 2024 - LoCoMo]] · [[Yin 2026 - SimpleToolHalluBench]]

---

## 2.5 Hipótesis

→ [[Hipotesis de investigacion]]

**Hipótesis general**: La aplicación de técnicas de memoria y gestión de contexto reduce significativamente el [[Context rot]] en agentes LLM multi-MCP, produciendo una mejora medible en el [[IQCR]] respecto al [[Baseline]].

**Hipótesis específicas** (HE1–HE5): ver página completa.

**Pruebas estadísticas**: Wilcoxon · ANOVA + Tukey · [[TOST]] · [[Diseno factorial 2k]] · [[PELT]] + bootstrap.

---

## 2.6 Definición y Operacionalización de Variables

→ [[Variables e indicadores]]

| Variable | Tipo | Indicadores |
|---|---|---|
| Técnica de mitigación | Independiente | Ninguna / RAG / SessionFacts / MemoryBank / Caching / Tool gating / Combinación |
| Nivel de degradación (IQCR) | Dependiente | [[Exactitud de respuesta]] · [[Tasa de alucinacion]] · [[Coherencia conversacional]] · [[Eficiencia de tokens]] · [[Latencia p50 p95]] |
| Longitud de conversación | Moderadora | Tokens acumulados · número de turnos |
| Nº de servidores MCP | Moderadora | Servidores activos · tamaño del catálogo |
