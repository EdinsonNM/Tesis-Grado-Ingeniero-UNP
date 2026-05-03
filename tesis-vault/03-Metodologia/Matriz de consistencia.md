# Matriz de Consistencia

→ Capítulo [[Cap 3 - Marco Metodologico]] · [[Cap 6 - Anexos]]
Fuente: `DOC-16_Matriz_Consistencia.docx`

La matriz vincula formalmente cada problema con su objetivo, hipótesis, variables, indicadores de medición y metodología estadística. Garantiza la coherencia interna del diseño de investigación.

---

## Nivel General

| Componente | Enunciado |
|---|---|
| **Problema general** | ¿En qué medida la aplicación de técnicas de memoria y gestión de contexto reduce el [[Context rot]] en [[Agente LLM\|agentes LLM]] conectados a múltiples [[Servidor MCP\|servidores MCP]]? |
| **Objetivo general** | Medir el impacto de las técnicas sobre el context rot, identificando qué técnicas o combinaciones reducen significativamente la degradación y bajo qué condiciones. |
| **Hipótesis general** | La aplicación de técnicas de memoria reduce significativamente el context rot, con al menos una configuración que alcanza una mejora >30% en el [[IQCR]] después de 50 turnos. |
| **Variable independiente** | Tipo y combinación de técnicas (5 niveles: baseline / RAG / SessionFacts / MemoryBank / caching / combinación óptima). |
| **Variable dependiente** | Nivel de context rot medido mediante el IQCR (índice ponderado [0,1]). |
| **Indicadores** | IQCR · Exactitud (%) · Tasa de alucinación (%) · Coherencia [[BERTScore]] · Tokens/turno |
| **Metodología** | Enfoque cuantitativo · Diseño experimental puro · Nivel explicativo-causal · Tipo aplicada · 200 conv./grupo · ANOVA, t-test, [[PELT]] |

---

## Nivel Específico

### PE1 — Degradación Base

| Componente | Enunciado |
|---|---|
| **Problema** | ¿Cómo y en qué magnitud se manifiesta el context rot **sin técnicas** de memoria? |
| **Objetivo (OE1)** | Establecer la línea base cuantitativa ejecutando conversaciones de longitud creciente (10, 30, 50, 100 turnos). |
| **Hipótesis (HE1)** | Sin técnicas, los agentes exhiben degradación ≥25% en exactitud y aumento ≥15% en alucinación entre los turnos 10 y 50. |
| **VI** | Ausencia de técnicas (condición [[Baseline]]). *Moderadores:* longitud de conversación; nº servidores MCP (2, 3, 5). |
| **VD** | Exactitud y tasa de alucinación a lo largo de la conversación. |
| **Indicadores** | Exactitud por turno (%) · Tasa de alucinación por turno (%) · Tokens acumulados · Curva de degradación |
| **Prueba estadística** | Wilcoxon rangos con signo · Corrección Bonferroni · Potencia 1−β = 0.80 · n mín. = 34 |

---

### PE2 — Técnicas Individuales

| Componente | Enunciado |
|---|---|
| **Problema** | ¿En qué medida cada técnica individual — [[RAG]], [[SessionFacts]], [[MemoryBank]], [[Caching semantico|caching]] — reduce la degradación? |
| **Objetivo (OE2)** | Comparar el impacto individual de las cuatro técnicas sobre las métricas del IQCR respecto al baseline. |
| **Hipótesis (HE2)** | Al menos una técnica produce reducción significativa con d de Cohen ≥ 0.5 en ≥2 métricas del IQCR. |
| **VI** | Tipo de técnica de memoria. *Control:* modelo base, temperatura, escenarios de prueba. |
| **VD** | IQCR por turno · Exactitud · Tasa de alucinación · Coherencia BERTScore |
| **Indicadores** | IQCR turno 50 vs baseline · d de Cohen por métrica · Reducción % exactitud · Reducción % alucinación |
| **Prueba estadística** | ANOVA 1 factor · Post-hoc Tukey HSD · d de Cohen · IC 95% · α' = 0.01 (Bonferroni) |

---

### PE3 — Tool Gating

| Componente | Enunciado |
|---|---|
| **Problema** | ¿En qué medida el [[Tool gating]] reduce la sobrecarga de contexto en catálogos de herramientas MCP de gran escala? |
| **Objetivo (OE3)** | Evaluar el impacto del tool gating en catálogos de 20, 50 y 100 herramientas MCP. |
| **Hipótesis (HE3)** | Tool gating reduce ≥50% el consumo de tokens de herramientas sin reducción significativa en selección correcta ni aumento >10% en alucinación de parámetros. |
| **VI** | Estrategia de tool gating (sin gating / filtrado semántico / carga diferida). *Moderador:* tamaño del catálogo. |
| **VD** | Tokens de descripción de herramientas · Tasa de selección correcta · Tasa de alucinación de parámetros |
| **Indicadores** | Tokens herramientas/turno · Selección correcta (%) · Alucinación de parámetros (%) · Reducción % tokens |
| **Prueba estadística** | Beneficio: t-test 1 cola · Ausencia de daño: [[TOST]] · Margen equivalencia ±10% · α = 0.05 |

---

### PE4 — Sinergia de Técnicas Combinadas

| Componente | Enunciado |
|---|---|
| **Problema** | ¿Qué combinación de técnicas produce el mayor impacto positivo sobre la calidad de respuestas? |
| **Objetivo (OE4)** | Identificar la combinación óptima mediante [[Diseno factorial 2k|diseño factorial 2^k reducido]], considerando calidad y overhead. |
| **Hipótesis (HE4)** | La combinación óptima produce IQCR significativamente superior al de cualquier técnica individual, con mejora adicional ≥15% en sesiones de ≥50 turnos. |
| **VI** | Combinación de técnicas (diseño 2^(4-1) fraccionado, 16 corridas). Función objetivo: IQCR ponderado por [[AHP]]. |
| **VD** | IQCR de la combinación vs. mejor técnica individual. *Secundaria:* overhead en latencia y tokens. |
| **Indicadores** | IQCR combinación vs. individual · Coeficientes de interacción 2FI · Overhead latencia (ms) · Overhead tokens (%) |
| **Prueba estadística** | Factorial 2^(4-1) Res. IV · Criterio de Lenth para efectos activos · t-test + Bonferroni para comparación final |

---

### PE5 — Umbrales de Degradación

| Componente | Enunciado |
|---|---|
| **Problema** | ¿Existen umbrales de longitud de contexto o nº de servidores MCP a partir de los cuales el context rot es estadísticamente significativo? |
| **Objetivo (OE5)** | Localizar empíricamente los umbrales en tokens acumulados y nº de servidores, con y sin técnicas de memoria. |
| **Hipótesis (HE5)** | Existen umbrales discretos en el rango 20,000–60,000 tokens (sin memoria) y 50,000–100,000 tokens (con combinación óptima), detectables con IC 95%. |
| **VI** | Longitud de contexto acumulado (tokens) · Nº de servidores MCP activos (2, 3, 5). |
| **VD** | Puntos de cambio estadísticos en las series temporales de exactitud y alucinación. |
| **Indicadores** | Umbrales en tokens (IC 95%) · Puntos de cambio por nº de servidores · Velocidad de degradación pre/post umbral |
| **Prueba estadística** | Algoritmo [[PELT]] (ruptures) · Bootstrap n = 1,000 · IC 95% por percentiles · Análisis por 3 configuraciones de servidores |

---

## Resumen de Correspondencia

| Hip. | Prob. | Obj. | Prueba estadística | Criterio de rechazo HG₀ |
|---|---|---|---|---|
| HG | PG | OG | t de una cola | IQCR mejora >30% en turno 50 |
| HE1 | PE1 | OE1 | Wilcoxon | −25% exactitud, +15% alucinación |
| HE2 | PE2 | OE2 | ANOVA + Tukey | d ≥ 0.5 en ≥2 métricas |
| HE3 | PE3 | OE3 | t + TOST | −50% tokens, equivalencia ±10% |
| HE4 | PE4 | OE4 | Factorial + Bonferroni | +15% sobre mejor individual |
| HE5 | PE5 | OE5 | PELT + bootstrap | Umbral dentro de rangos definidos |
