# Objetivos de Investigación

→ Sección 1.4 del capítulo [[Cap 1 - Aspectos de la Problematica]]
Fuente: `DOC-09_Objetivos.docx`

Los objetivos están formulados con verbo de acción verificable, objeto de estudio delimitado y condición de aplicación. Cada objetivo se corresponde biunívocamente con un problema específico (DOC-07) y una hipótesis (DOC-13).

---

## Objetivo General

> **OG:** Medir el impacto de las técnicas de memoria y gestión de contexto sobre la degradación de respuestas ([[Context rot]]) en [[Agente LLM|agentes LLM]] conectados a múltiples [[Servidor MCP|servidores MCP]], identificando qué técnicas o combinaciones de técnicas reducen significativamente dicha degradación y bajo qué condiciones de longitud de contexto y escala de herramientas.

El objetivo integra tres dimensiones: (a) medición cuantitativa del fenómeno → requiere definir y operacionalizar el [[IQCR]]; (b) comparación sistemática de técnicas → requiere diseño experimental controlado; (c) caracterización de las condiciones de aplicación → requiere modelar la relación entre longitud de contexto, número de servidores y efectividad de cada técnica.

---

## Objetivos Específicos

### OE1 — Establecer la Línea Base

> Establecer la línea base cuantitativa de degradación de respuestas en agentes LLM multi-MCP **sin aplicación de técnicas** de memoria, mediante conversaciones de longitud creciente y registro sistemático de exactitud, coherencia, alucinación y consumo de tokens por turno.

**Actividades clave:** configurar ≥3 servidores MCP de dominios distintos (búsqueda, código, datos SQL); diseñar conversaciones de 10, 30, 60 y 100 turnos; instrumentar el agente para registro por turno.

**Entregable:** curvas de degradación [[Baseline]] + caracterización estadística descriptiva del fenómeno.

---

### OE2 — Comparar Técnicas Individuales de Memoria

> Comparar el impacto individual de cuatro técnicas representativas — [[RAG]] semántico, [[SessionFacts]], [[MemoryBank]] y [[Caching semantico|semantic caching]] — sobre las métricas del [[IQCR]], determinando el efecto marginal de cada técnica respecto a la línea base de OE1.

**Método:** pruebas t de Student o Mann-Whitney U (según distribución), d de Cohen, ANOVA con α = 0.05.

**Entregable:** tabla comparativa de efectividad con intervalos de confianza al 95%.

---

### OE3 — Evaluar Tool Gating

> Evaluar el impacto de estrategias de [[Tool gating]] — carga diferida y filtrado semántico dinámico — sobre la sobrecarga generada por catálogos de herramientas MCP de **20, 50 y 100 herramientas**, midiendo tasa de selección correcta, tasa de alucinación de parámetros y reducción porcentual en tokens de descripción.

**Método:** filtrado semántico por similitud coseno (umbral optimizado por validación cruzada). Verificación de equivalencia mediante [[TOST]] con margen del 10%.

**Entregable:** módulo validado de filtrado semántico de herramientas + tabla de resultados por tamaño de catálogo.

---

### OE4 — Identificar la Combinación Óptima

> Identificar la combinación de técnicas de memoria y gestión de contexto que maximiza la calidad de respuesta en agentes LLM multi-MCP, minimizando simultáneamente la degradación y el overhead computacional, mediante un [[Diseno factorial 2k|diseño factorial 2^k reducido]] aplicado a las técnicas evaluadas en OE2 y OE3.

**Método:** diseño 2^(5-1) fraccionado resolución IV; función objetivo = IQCR ponderado por [[AHP]]; criterio de Lenth para efectos activos.

**Entregable:** recomendación de configuración óptima para arquitecturas multi-MCP en producción.

---

### OE5 — Localizar Umbrales de Degradación

> Localizar empíricamente los umbrales de longitud de contexto (en tokens acumulados) y número de servidores MCP activos a partir de los cuales la degradación se vuelve estadísticamente significativa, **con y sin** las técnicas evaluadas, mediante análisis de segmentación de series temporales y modelización de puntos de cambio.

**Método:** algoritmo [[PELT]] sobre series temporales de exactitud y alucinación. Bootstrapping (1,000 muestras), IC al 95%. Análisis independiente para 2, 3 y 5 servidores MCP activos.

**Entregable:** mapa de umbrales con intervalos de confianza en unidades operacionales (tokens y número de servidores).

---

## Síntesis de Objetivos y Entregables

| Obj. | Verbo | Método principal | Entregable |
|---|---|---|---|
| OG | Medir | Diseño experimental completo | Protocolo de comparación + recomendaciones |
| OE1 | Establecer | Registro por turno | Curvas baseline de degradación |
| OE2 | Comparar | ANOVA + d de Cohen | Tabla comparativa de efectividad |
| OE3 | Evaluar | Filtrado coseno + TOST | Módulo de tool gating validado |
| OE4 | Identificar | Factorial 2^k + AHP | Configuración óptima recomendada |
| OE5 | Localizar | PELT + bootstrap | Mapa de umbrales de context rot |

**OE1 a OE5 son condición necesaria y suficiente para OG:** OE1 da la referencia; OE2 y OE3 caracterizan técnicas individuales; OE4 integra en configuración optimizada; OE5 caracteriza las condiciones límite del fenómeno.

---

## Fuentes

- [[Problema de investigacion]] — los problemas que estos objetivos responden
- [[Hipotesis de investigacion]] — las proposiciones que verifican el logro de los objetivos
- [[IQCR]] — el índice que se mide en OG y OE2
- [[Diseno factorial 2k]] — diseño experimental de OE4
- [[PELT]] — algoritmo de OE5
- [[TOST]] — prueba de equivalencia en OE3
