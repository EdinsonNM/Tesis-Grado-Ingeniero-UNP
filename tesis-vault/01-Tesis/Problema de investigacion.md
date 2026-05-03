# Problema de Investigación

→ Sección 1.2 del capítulo [[Cap 1 - Aspectos de la Problematica]]
Fuente: `DOC-07_Formulacion_Problema.docx`

---

## Problema General

> **PG:** ¿En qué medida la aplicación de técnicas de memoria y gestión de contexto reduce la degradación de respuestas ([[Context rot]]) en [[Agente LLM|agentes LLM]] conectados a múltiples [[Servidor MCP|servidores MCP]], en comparación con una arquitectura base sin dichas técnicas?

La pregunta encapsula el problema en tres dimensiones: (a) la variable independiente — técnicas de memoria y gestión de contexto; (b) la variable dependiente — degradación medida mediante el [[IQCR]]; y (c) el contexto — arquitectura multi-MCP.

---

## Mecanismos del Problema

La degradación se manifiesta por tres vías que se potencian mutuamente en arquitecturas multi-MCP:

**1. [[Tool overload]]** — el catálogo de herramientas de múltiples servidores se expone completo al modelo en cada turno. Para 3–5 servidores con 20 herramientas cada uno: 12,000–20,000 tokens de overhead *antes de procesar ninguna consulta* (Tang et al., 2025).

**2. Acumulación de resultados intermedios** — cada ciclo ReAct agrega observaciones de herramientas al [[Contexto activo]], que terminan en la región central del contexto donde los LLMs pierden atención efectiva (efecto [[Lost in the middle]]; Liu et al., 2023: −40% utilización efectiva).

**3. Mezcla de estados de sesión** — metadatos de múltiples servidores (errores, autenticación, paginación) coexisten sin separación semántica, confundiendo al modelo sobre qué servidor respondió qué (Chroma Research, 2025: tasa de error de atribución del 3% con 1 servidor → 18% con 5 servidores).

---

## Problemas Específicos

### PE1 — Cuantificación de la Degradación Base
¿Cómo y en qué magnitud se manifiesta el [[Context rot]] en agentes LLM multi-MCP cuando **no se aplica ninguna técnica** de memoria?

Establece el [[Baseline]] del experimento mediante ejecución de agentes en configuración sin memoria sobre sesiones de 10, 30, 60 y 100 turnos, registrando exactitud, alucinación, latencia y tokens por turno.

### PE2 — Efectividad de Técnicas Individuales de Memoria
¿En qué medida cada técnica individual — [[RAG]] semántico, [[SessionFacts]], [[MemoryBank]] y [[Caching semantico|semantic caching]] — reduce la degradación medida en exactitud, coherencia y consumo de tokens?

Examina el efecto aislado de cuatro técnicas representativas para estimar el efecto marginal de cada una sobre el IQCR e identificar la mejor relación mejora/overhead.

### PE3 — Efectividad de Tool Gating
¿En qué medida las estrategias de [[Tool gating]] — carga diferida y filtrado semántico — reducen la sobrecarga de contexto en agentes con catálogos de herramientas MCP de 20, 50 y 100 herramientas?

Métricas de interés: tasa de selección correcta de herramientas, tasa de alucinación de parámetros, tokens consumidos por descripción de herramientas.

### PE4 — Sinergia de Técnicas Combinadas
¿Qué combinación de técnicas produce el mayor impacto positivo sobre la calidad de respuestas, considerando conjuntamente exactitud, coherencia, latencia y consumo de recursos?

Evalúa sinergias e interferencias entre técnicas mediante [[Diseno factorial 2k|diseño factorial 2^k reducido]]. Determina si la combinación, por ejemplo, de RAG + tool gating + SessionFacts supera a cualquier técnica individual o produce efecto de saturación.

### PE5 — Umbrales de Degradación y Puntos Críticos
¿Existen umbrales de longitud de contexto o número de servidores MCP a partir de los cuales la degradación se vuelve estadísticamente significativa e irreversible, con y sin técnicas de memoria?

La localización de umbrales tiene implicaciones directas para el diseño de sistemas en producción: permite implementar políticas de activación automática de técnicas basadas en contadores de tokens o número de servidores activos.

---

## Variables del Estudio

**Variable independiente:** tipo y combinación de técnicas de memoria aplicadas. Cinco niveles: (a) baseline sin técnica, (b) RAG semántico, (c) SessionFacts, (d) tool gating, (e) combinación óptima.

**[[Variable dependiente]]:** nivel de [[Context rot]], medido mediante el [[IQCR]] — índice compuesto de (a) exactitud de respuesta vs. [[Ground truth]], (b) tasa de alucinación, (c) coherencia conversacional ([[BERTScore]]), (d) consumo de tokens por turno.

**Variables de control:** modelo LLM base (Claude Sonnet 4.5), temperatura (0.0), dataset de evaluación, número y tipo de servidores MCP, infraestructura de cómputo.

**Variables moderadoras:** longitud de la conversación (turnos y tokens acumulados); número de servidores MCP activos (determina el volumen de herramientas disponibles).

---

## La Brecha que Justifica la Investigación

Cada técnica ha sido evaluada en escenarios distintos con métricas inconsistentes. Ningún estudio las compara sistemáticamente en el contexto específico de **arquitecturas multi-MCP**. No existe evidencia empírica de qué combinaciones producen los mejores resultados ni a qué costo, ni se han identificado los **umbrales estadísticos** a partir de los cuales el context rot se vuelve significativo.

Esta brecha es el espacio que la presente tesis busca llenar mediante un protocolo experimental unificado.

---

## Correspondencia con Hipótesis y Objetivos

| Problema | Hipótesis | Objetivo |
|---|---|---|
| PG | [[Hipotesis de investigacion\|HG]] | OG |
| PE1 | HE1 | OE1 |
| PE2 | HE2 | OE2 |
| PE3 | HE3 | OE3 |
| PE4 | HE4 | OE4 |
| PE5 | HE5 | OE5 |

---

## Fuentes

- [[Realidad Problematica]] — evidencia empírica del problema
- [[Context rot]] — definición operacional del fenómeno
- [[Tool overload]] — mecanismo principal
- [[Hipotesis de investigacion]] — las proposiciones verificables derivadas
