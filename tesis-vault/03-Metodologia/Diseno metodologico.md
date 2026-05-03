# Diseño Metodológico

→ Sección 3 del capítulo [[Cap 3 - Marco Metodologico]]
Fuente: `DOC-14_Marco_Metodologico.docx`

---

## 3.1 Enfoque de Investigación

La investigación adopta un **enfoque cuantitativo**. Las variables dependientes del estudio — exactitud de respuesta, tasa de alucinación, consumo de tokens, coherencia conversacional — son inherentemente numéricas y mensurables con instrumentos objetivos. El objetivo central es establecer relaciones causales entre las técnicas de memoria y la calidad de respuesta, lo que requiere control experimental y pruebas de significancia estadística con resultados reproducibles.

El enfoque cuantitativo no excluye interpretación cualitativa: en la discusión de resultados se contextualizarán los hallazgos numéricos en el marco de la práctica de ingeniería de sistemas agentes. Sin embargo, la recolección de datos y la verificación de hipótesis se realizan exclusivamente mediante procedimientos cuantitativos.

---

## 3.2 Diseño de la Investigación

El diseño es **experimental puro** con grupos de control y tratamiento, medición pre y post intervención, y asignación controlada de condiciones experimentales.

**Seis grupos experimentales:**
- 1 grupo de control — agente sin técnicas de memoria ([[Baseline]])
- 5 grupos de tratamiento — distintas configuraciones de técnicas

Todos los grupos se exponen a los mismos escenarios de conversación y al mismo conjunto de datos de prueba, garantizando que las diferencias observadas sean atribuibles exclusivamente a la variable independiente.

**Medidas repetidas:** las métricas se registran en cada turno de la conversación, generando series temporales de 30, 50 o 100 puntos. Este diseño longitudinal permite detectar puntos de cambio ([[HE5|hipótesis HE5]]) y analizar la velocidad de degradación como variable secundaria.

**Diseño factorial para combinaciones (HE4):** diseño factorial **2^(k-1)** fraccionado de resolución IV, con k = 5 factores binarios (4 técnicas de memoria + tool gating). La resolución IV garantiza que los efectos principales no estén confundidos con interacciones de dos factores, permitiendo estimar las sinergias más relevantes. → Ver [[Diseno factorial 2k]]

---

## 3.3 Nivel y Tipo de Investigación

**Nivel:** explicativo-causal. El fenómeno de context rot ya está documentado descriptivamente (Liu et al., 2023; Chroma Research, 2025); el paso necesario es la explicación causal de qué técnicas lo mitigan y en qué magnitud.

La investigación tiene una dimensión exploratoria secundaria en la detección de umbrales ([[HE5]]): no existen estudios previos que hayan caracterizado los puntos de cambio del context rot en arquitecturas multi-MCP.

**Tipo:** investigación aplicada. Los resultados tienen aplicación directa en el diseño de sistemas agentes LLM en producción — las recomendaciones sobre qué técnicas implementar y bajo qué condiciones serán utilizables por ingenieros sin adaptación teórica intermedia.

---

## 3.4 Unidad de Análisis y Muestra

**Unidad de análisis:** el turno de conversación de un [[Agente LLM]] conectado a múltiples [[Servidor MCP|servidores MCP]] en sesión experimental controlada. Cada turno registra: identificador de sesión, número de turno, consulta del usuario, respuesta generada, métricas de calidad (exactitud, alucinación, coherencia, tokens) y configuración experimental (técnica activa, nº de servidores, tokens acumulados).

**Muestra experimental:** 200 conversaciones por grupo de tratamiento, construidas desde tres fuentes:

| Fuente | N | Foco |
|---|---|---|
| [[LongMemEval]] (adaptado) | 100 conversaciones | Memoria conversacional a largo plazo |
| [[LoCoMo]] (selección) | 50 conversaciones | Coherencia y consistencia multi-sesión |
| [[Escenarios multi-MCP sinteticos]] (ad hoc) | 50 conversaciones | 3 dominios: búsqueda, código, datos SQL |

**Cálculo de potencia** (G*Power 3.1, d = 0.5, α = 0.05, 1−β = 0.80): mínimo n = 34 por grupo para pruebas t. La muestra de 200 conversaciones supera ampliamente este mínimo y garantiza potencia para efectos pequeños (d = 0.2) en análisis secundarios.

**Longitudes de conversación:** 30, 50 y 100 turnos por sesión, para capturar la trayectoria completa de degradación.

**Modelo LLM base:** Claude Sonnet 4.5, accedido vía API de Anthropic con **temperatura = 0.0** para determinismo y reproducibilidad. Temperatura fija elimina la aleatoriedad: cada experimento es replicable. Los servidores MCP se seleccionan del MCP Registry (2025) en dominios de búsqueda web, ejecución de código Python y consulta de bases de datos SQL.

---

## 3.5 Fases del Experimento

### Fase 1 — Preparación del Entorno Experimental

- Implementación del agente base (sin memoria) con soporte MCP sobre el SDK de Anthropic.
- Configuración y validación de los tres servidores MCP seleccionados.
- Implementación de los módulos de cada técnica:
  - RAG con **ChromaDB** (embeddings + búsqueda HNSW)
  - [[SessionFacts]] — extracción periódica de hechos clave
  - [[MemoryBank]] — política de olvido Ebbinghaus
  - [[Caching semantico|Semantic caching]] con **RedisVL** (umbral coseno 0.92–0.95)
  - [[Tool gating]] — filtrado semántico del catálogo MCP
- Construcción del módulo de evaluación automatizado (exactitud vs. [[Ground truth]], verificación de alucinaciones, [[BERTScore]] para coherencia, contador de tokens vía API).
- Validación del dataset mediante prueba piloto con 20 conversaciones.

### Fase 2 — Establecimiento de la Línea Base

Ejecución del grupo de control sobre las 200 conversaciones en tres configuraciones de servidores (2, 3 y 5 servidores MCP activos). Registro de métricas en cada turno → series temporales de degradación. Los resultados establecen el [[Baseline]] y ajustan el plan de potencia estadística.

### Fase 3 — Evaluación de Técnicas Individuales

Ejecución de los cuatro grupos de tratamiento individuales (RAG, SessionFacts, MemoryBank, caching) sobre el mismo dataset de la línea base. Ejecución independiente por grupo, orden aleatorizado por bloques para controlar efectos de secuencia.

### Fase 4 — Evaluación de Tool Gating

Evaluación aislada de [[Tool gating]] en escenarios con 20, 50 y 100 herramientas MCP simultáneas. Se miden: tasa de selección correcta de herramientas, tasa de alucinación de parámetros y consumo de tokens de descripción, antes y después de filtrado semántico.

### Fase 5 — Diseño Factorial y Optimización

Ejecución del diseño **2^(5-1)** (16 combinaciones) sobre 50 conversaciones seleccionadas aleatoriamente. Análisis factorial para identificar efectos principales e interacciones. Selección de combinación óptima mediante la función objetivo [[IQCR]].

### Fase 6 — Análisis Estadístico y Detección de Umbrales

- Pruebas de hipótesis para HE1–HE5.
- Cálculo de tamaños del efecto (d de Cohen, η² parcial).
- Intervalos de confianza al 95%.
- Algoritmo [[PELT]] para detección de puntos de cambio en series de degradación.
- **Librerías Python:** `scipy`, `statsmodels`, `ruptures` (PELT), `pingouin` (ANOVA, TOST).
- Todo el código se publicará bajo licencia MIT como material suplementario.

---

## 3.6 Técnicas e Instrumentos

| Componente | Tecnología | Fase |
|---|---|---|
| LLM base | Claude Sonnet 4.5 (API Anthropic, T=0.0) | Todas |
| Base vectorial | ChromaDB (HNSW) | F1, F3, F4 |
| Semantic caching | RedisVL (coseno ≥ 0.92) | F1, F3 |
| Memoria a largo plazo | SQLite + política Ebbinghaus | F1, F3 |
| Evaluación de exactitud | Ground truth + scorer automático | F2–F6 |
| Evaluación de coherencia | [[BERTScore]] (Zhang et al., 2020) | F2–F6 |
| Detección de puntos de cambio | ruptures (PELT) | F6 |
| Análisis estadístico | scipy / statsmodels / pingouin | F6 |
| Gestión de experimentos | MLflow (tracking de métricas) | F2–F6 |

---

## 3.7 Aspectos Éticos

- **APIs de IA:** uso en estricto cumplimiento de los términos de servicio de Anthropic. No se intentará extraer parámetros internos del modelo ni vulnerar salvaguardas de seguridad.
- **Datos:** LongMemEval y LoCoMo son de acceso público bajo licencias académicas. Los escenarios ad hoc son completamente sintéticos, sin datos personales identificables.
- **Reproducibilidad:** todo el código del experimento (módulos de técnicas, evaluación, análisis estadístico) se publicará bajo licencia MIT como material suplementario.
- **Impacto ambiental:** consumo estimado de 500,000–1,000,000 tokens de entrada/salida en todo el experimento (comparable a pocas horas de uso intensivo de un PC). Se documentará el consumo por experimento para facilitar estimaciones de replicación.
- **Ausencia de conflicto de intereses:** el investigador declara no tener relación económica ni institucional con Anthropic ni con los proveedores de servidores MCP. Los resultados negativos (hipótesis no confirmadas) se reportarán tal como los produzcan los datos.

---

## Relaciones con otras páginas

- [[Hipotesis de investigacion]] — las hipótesis que este diseño debe verificar
- [[Dataset de evaluacion]] — detalle de los benchmarks utilizados
- [[IQCR]] — el índice compuesto que se mide en cada turno
- [[PELT]] — algoritmo para HE5
- [[TOST]] — prueba de equivalencia para HE3
- [[Diseno factorial 2k]] — estructura del experimento para HE4
- [[Baseline]] — condición de control sin técnicas
