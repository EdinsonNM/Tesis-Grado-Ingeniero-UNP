# Cap 3 — Marco Metodológico

> Tercer capítulo. Define cómo se hace la investigación: enfoque, diseño, nivel, tipo, sujetos, métodos, técnicas e instrumentos, y aspectos éticos.

← [[Cap 2 - Marco Teorico]] | → [[Cap 4 - Aspectos Administrativos]]

Ver página detallada: [[Diseno metodologico]]

---

## 3.1 Enfoque

**Cuantitativo.** La investigación mide variables numéricas (métricas del [[IQCR]]: exactitud, tasa de alucinación, coherencia, tokens, latencia) y contrasta hipótesis mediante análisis estadístico inferencial.

---

## 3.2 Diseño

**Experimental puro** con grupo de control y grupos de tratamiento.

- **Control**: [[Baseline]] — agente LLM multi-MCP sin técnicas de memoria.
- **Tratamientos**: [[Tool gating]], [[SessionFacts]], [[MemoryBank]], [[Caching semantico]], [[RAG]], y combinaciones.
- **Estructura**: [[Diseno factorial 2k]] para evaluar interacciones entre técnicas.

---

## 3.3 Nivel

**Explicativo.** No solo describe la degradación (nivel descriptivo) sino que mide el efecto causal de cada intervención sobre el [[Context rot]].

---

## 3.4 Tipo

**Aplicado.** El resultado es un protocolo experimental reproducible, no un nuevo modelo teórico.

---

## 3.5 Sujetos de la Investigación

**Unidad de análisis**: el turno de conversación de un [[Agente LLM]] conectado a múltiples [[Servidor MCP|servidores MCP]].

**Unidad experimental**: sesiones de hasta 100 turnos con configuración de herramientas controlada (20, 50 y 100 herramientas disponibles).

---

## 3.6 Métodos y Procedimientos

Fases del experimento:

1. **Preparación del entorno** — despliegue de servidores MCP, configuración del modelo base.
2. **Línea base** — sesiones con [[Baseline]] para curvas de degradación sin intervención.
3. **Técnicas individuales** — una técnica por fase, métricas comparadas contra baseline.
4. **Tool gating** — evaluación específica con [[ToolHaystack]] y catálogos de 20/50/100 herramientas.
5. **Diseño factorial** — combinaciones de técnicas con [[Diseno factorial 2k]].
6. **Análisis estadístico** — [[PELT]] para umbrales, [[TOST]] para equivalencia, ANOVA para efectos.

**Datasets de evaluación**:
- [[LongMemEval]] — memoria conversacional a largo plazo
- [[LoCoMo]] — coherencia y consistencia multi-sesión
- [[SimpleToolHalluBench]] — alucinación de herramientas
- [[ToolHaystack]] — selección en catálogos grandes
- [[Escenarios multi-MCP sinteticos]] — condiciones específicas multi-servidor

Cada dataset aporta o permite construir [[Ground truth]] para calcular el [[IQCR]].

---

## 3.7 Técnicas e Instrumentos

**Instrumentos técnicos**:
- API del modelo LLM base (variable de control fija).
- ChromaDB para [[RAG]] y recuperación vectorial.
- SQLite para [[MemoryBank]].
- RedisVL para [[Caching semantico]].
- Módulo de [[SessionFacts]].
- [[BERTScore]] para [[Coherencia conversacional]].
- Python + scipy + statsmodels + pingouin + ruptures para análisis estadístico.

**Métricas del [[IQCR]]**:
- [[Exactitud de respuesta]] — comparación contra [[Ground truth]]
- [[Tasa de alucinacion]] — detección de afirmaciones incorrectas
- [[Coherencia conversacional]] — BERTScore sobre respuestas consecutivas
- [[Eficiencia de tokens]] — tokens consumidos por turno
- [[Latencia p50 p95]] + [[TTFT]] — distribución de tiempos de respuesta

**[[Normalizacion de metricas]]**: [[AHP]] para ponderar los componentes del IQCR.

---

## 3.8 Aspectos Éticos

- Los datos generados son sintéticos o de benchmarks públicos: no hay información personal identificable.
- Los experimentos no implican participantes humanos.
- Los costos de API (tokens) se presupuestan y controlan para evitar gastos no autorizados.
- Los resultados se reportarán con transparencia completa, incluyendo los casos donde las técnicas no mejoren el baseline.
