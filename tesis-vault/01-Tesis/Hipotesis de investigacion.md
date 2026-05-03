# Hipótesis de Investigación

→ Sección 2.5 del capítulo [[Cap 2 - Marco Teorico]]
Fuente: `DOC-13_Hipotesis.docx`

Las hipótesis son proposiciones tentativas sobre la relación entre variables, formuladas de manera verificable mediante análisis estadístico. Cada hipótesis específica corresponde biunívocamente con un problema específico (DOC-07) y un objetivo específico (DOC-09), garantizando la coherencia interna del diseño.

---

## Hipótesis General

**HG:** La aplicación de técnicas de memoria y gestión de contexto reduce significativamente la degradación de respuestas ([[Context rot]]) en [[Agente LLM|agentes LLM]] conectados a múltiples [[Servidor MCP|servidores MCP]], produciendo una mejora medible en el [[IQCR]] respecto a una arquitectura base sin dichas técnicas, con **al menos una configuración que alcanza una mejora superior al 30% en el IQCR después de 50 turnos** de conversación.

**HG₀:** La aplicación de técnicas de memoria y gestión de contexto no produce una mejora estadísticamente significativa en el IQCR respecto a la arquitectura base (α = 0.05).

> El umbral del 30% se deriva de Chroma Research (2025), que documentó degradaciones superiores al 30% en sistemas de producción. La HG exige revertir al menos la totalidad de esa degradación observada.

**Verificación:** prueba t de una cola en turno 50, baseline vs. mejor grupo de tratamiento. Tamaño del efecto: d de Cohen ≥ 0.8 como criterio de relevancia práctica.

---

## Hipótesis Específicas

### HE1 — Degradación Base

**HE1:** En ausencia de técnicas de memoria, los agentes LLM multi-MCP exhiben una degradación estadísticamente significativa de **al menos el 25% en exactitud** y un **incremento de al menos el 15% en tasa de alucinación** al comparar el turno 10 con el turno 50.

**HE1₀:** No existe diferencia estadísticamente significativa (α = 0.05) en exactitud ni alucinación entre el turno 10 y el turno 50 sin técnicas de memoria.

> Establece la existencia y magnitud del context rot como condición previa. Umbrales conservadores respecto a Liu et al. (2023) −40% y Chroma Research (2025) >30%.

**Verificación:** Prueba de Wilcoxon de rangos con signo. Mínimo 30 conversaciones independientes de 50 turnos (potencia 1−β ≥ 0.80). Corrección de Bonferroni para comparaciones múltiples.

---

### HE2 — Técnicas Individuales de Memoria

**HE2:** Al menos una de las técnicas individuales evaluadas — RAG semántico, [[SessionFacts]], [[MemoryBank]] o [[Caching semantico|semantic caching]] — produce una reducción estadísticamente significativa en la tasa de degradación, con efecto de tamaño **medio o grande (d de Cohen ≥ 0.5)** en al menos dos de las cuatro métricas primarias del [[IQCR]].

**HE2₀:** Ninguna técnica individual produce reducción significativa (α = 0.05), o el tamaño del efecto es pequeño (d < 0.5) para todas las métricas del IQCR.

**Verificación:** ANOVA de un factor con post-hoc de Tukey. Shapiro-Wilk para normalidad de residuos. Análisis separado para cada longitud de conversación (30, 50, 100 turnos).

---

### HE3 — Tool Gating

**HE3:** Las estrategias de [[Tool gating]] reducen el consumo de tokens de descripción de herramientas en **al menos el 50%** en catálogos de 50 y 100 herramientas MCP, sin producir una reducción estadísticamente significativa en la tasa de selección correcta (p > 0.05) ni un incremento mayor al **10%** en la tasa de alucinación de parámetros.

**HE3₀:** Tool gating no produce reducción del 50% o mayor en tokens de descripción, O produce reducción significativa en la tasa de selección correcta, O incrementa la alucinación de parámetros en más del 10%.

> Hipótesis compuesta: requiere simultáneamente verificar el beneficio (reducción de tokens) y la ausencia de daño (mantenimiento de exactitud). Umbral del 50% derivado de Tang et al. (2025) para RAG-MCP en 128 herramientas.

**Verificación:** Prueba t de una cola para beneficio. [[TOST]] (Two One-Sided Tests) con margen de equivalencia del 10% para verificar ausencia de daño — esto proporciona evidencia positiva de equivalencia, no solo ausencia de evidencia de daño.

---

### HE4 — Sinergia de Técnicas Combinadas

**HE4:** La combinación óptima de técnicas, identificada mediante [[Diseno factorial 2k|diseño factorial 2^k reducido]], produce un IQCR significativamente superior al de cualquier técnica individual, con una **mejora adicional de al menos el 15%** sobre la mejor técnica individual en conversaciones de 50 o más turnos con tres o más servidores MCP activos.

**HE4₀:** La combinación óptima no produce IQCR estadísticamente superior (α = 0.05) al de la mejor técnica individual, o la mejora adicional es menor al 15%.

> El umbral del 15% es conservador respecto a los efectos principales — reconoce que los efectos de sinergia son típicamente menores. La condición de ≥50 turnos restringe la verificación al régimen donde el context rot es clínicamente significativo.

**Verificación:** Coeficientes de interacción de segundo orden en el modelo factorial (criterio de Lenth para efectos activos). Prueba t con corrección de Bonferroni para comparar combinación óptima vs. técnicas individuales.

---

### HE5 — Umbrales de Degradación

**HE5:** Existen umbrales discretos y estadísticamente detectables de longitud de contexto acumulado y número de servidores MCP activos a partir de los cuales la degradación se vuelve significativa (p < 0.05), localizables en el rango de **20,000 a 60,000 tokens acumulados** sin técnicas y en el rango de **50,000 a 100,000 tokens** con la combinación óptima.

**HE5₀:** No existen umbrales discretos estadísticamente detectables dentro de los rangos de experimentación con potencia estadística suficiente (1−β ≥ 0.80).

> Mayor valor práctico: si los umbrales son predecibles, es posible implementar políticas de activación automática de técnicas basadas en contadores de tokens. Los rangos se derivan de Liu et al. (2023) escalados al overhead multi-MCP de 10,000–20,000 tokens.

**Verificación:** Algoritmo [[PELT]] aplicado a series temporales de exactitud y alucinación. Validación mediante bootstrapping (1,000 muestras), intervalos de confianza al 95%. Análisis independiente para 2, 3 y 5 servidores MCP activos.

---

## Nivel de Significancia y Potencia

- **α = 0.05** para todas las hipótesis confirmatorias.
- Corrección de Bonferroni para comparaciones múltiples (5 tratamientos): α' = 0.01 por prueba.
- **Potencia objetivo: 1−β = 0.80**. Tamaño mínimo calculado con G*Power 3.1 (d = 0.5, α = 0.05): n = 34 por grupo. La muestra de 200 conversaciones por grupo garantiza potencia para efectos pequeños (d = 0.2).
- Se reportarán d de Cohen (2 grupos) y η² parcial (ANOVA) con intervalos de confianza al 95% en todos los análisis, siguiendo APA 7.

---

## Correspondencia Hipótesis — Problemas — Objetivos

| Hip. | Problema | Objetivo | Prueba estadística | Umbral |
|---|---|---|---|---|
| HG | PG | OG | t de una cola | IQCR >30% en turno 50 |
| HE1 | PE1 | OE1 | Wilcoxon | −25% exactitud, +15% alucinación |
| HE2 | PE2 | OE2 | ANOVA + Tukey | d ≥ 0.5 en ≥2 métricas |
| HE3 | PE3 | OE3 | t + TOST | −50% tokens, equivalencia ±10% |
| HE4 | PE4 | OE4 | Factorial + Bonferroni | +15% sobre mejor individual |
| HE5 | PE5 | OE5 | PELT + bootstrap | Umbral en rangos definidos |

---

## Fuentes

- [[Bases Teoricas]] — bloques 4 y 6 (evidencia empírica de los umbrales)
- [[IQCR]] — el índice compuesto que se mide en HG y HE2
- [[TOST]] — prueba de equivalencia para HE3
- [[PELT]] — detección de puntos de cambio para HE5
- [[Diseno factorial 2k]] — diseño experimental para HE4
