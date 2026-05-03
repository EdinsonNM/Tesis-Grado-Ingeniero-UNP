# Cap 1 — Aspectos de la Problemática

> Primer capítulo de la tesis. Establece el contexto del problema, lo formula, justifica su importancia, define los objetivos y delimita el alcance.

← [[Arbol de la tesis]] | → [[Cap 2 - Marco Teorico]]

---

## 1.1 Descripción de la Realidad Problemática

El auge de los [[Agente LLM|agentes LLM]] conectados a servicios externos mediante el [[Model Context Protocol]] introduce un problema operativo no resuelto: a medida que la sesión avanza, el [[Contexto activo]] crece de forma acumulativa y sin control. Las herramientas disponibles se describen completas en cada llamada ([[Tool overload]]), los resultados intermedios se apilan turno a turno, y el estado de la sesión se mezcla sin separación clara.

El resultado es el [[Context rot]]: degradación progresiva de exactitud, aumento de alucinaciones, pérdida de coherencia conversacional, mayor costo de tokens y mayor latencia. El fenómeno se intensifica en arquitecturas **multi-MCP** —cuando el agente está conectado simultáneamente a varios [[Servidor MCP|servidores MCP]]— donde el espacio de herramientas puede superar las 100 entradas.

El efecto [[Lost in the middle]] agrava el problema: la atención del modelo se concentra en los extremos del contexto y degrada la información enterrada en posiciones centrales, que es precisamente donde se acumulan los resultados intermedios de herramientas.

**Conceptos clave de esta sección:**
- [[Context rot]] — el fenómeno central
- [[Tool overload]] — sobrecarga de herramientas
- [[Lost in the middle]] — degradación por posición
- [[Agente LLM]] — unidad de análisis
- [[Model Context Protocol]] — arquitectura de conexión
- [[Servidor MCP]] — fuente del espacio de herramientas
- [[Ventana de contexto]] — el límite físico
- [[Contexto activo]] — lo que crece con la sesión

---

## 1.2 Formulación del Problema de Investigación

→ [[Problema de investigacion]]

**Problema general**: ¿En qué medida la aplicación de técnicas de memoria y gestión de contexto reduce el [[Context rot]] en [[Agente LLM|agentes LLM]] conectados a múltiples [[Servidor MCP|servidores MCP]], en comparación con una arquitectura base sin dichas técnicas?

**Problemas específicos** (ver página completa):
1. Cuantificar la degradación base sin técnicas de memoria.
2. Medir el impacto individual de cada técnica.
3. Evaluar el efecto de [[Tool gating]] sobre catálogos MCP grandes.
4. Identificar combinaciones de técnicas con mejor efecto conjunto.
5. Localizar umbrales de degradación según longitud de contexto y número de servidores.

---

## 1.3 Justificación e Importancia

→ [[Justificacion e Importancia]]

La confiabilidad de los agentes LLM en producción depende directamente de que sus respuestas no degraden conforme la sesión avanza. El context rot convierte sesiones funcionales en sesiones fallidas sin que el usuario cambie nada: el único factor que cambia es la longitud de la conversación.

En contextos con presupuestos limitados (organizaciones latinoamericanas, startups, sectores públicos), reducir el consumo de tokens y la latencia no es solo una optimización de rendimiento, es una condición de viabilidad económica.

La investigación aporta un **protocolo experimental reproducible** que cualquier equipo puede aplicar para evaluar y seleccionar técnicas de mitigación en su propio entorno.

---

## 1.4 Objetivos de Investigación

→ [[Objetivos de investigacion]]

**Objetivo general**: Medir el impacto de técnicas de memoria y gestión de contexto sobre la degradación de respuestas en agentes LLM multi-MCP, identificando qué técnicas o combinaciones la reducen significativamente.

**Objetivos específicos**:
1. Establecer una línea base cuantitativa de degradación → [[Baseline]]
2. Comparar el impacto individual de [[RAG]], [[SessionFacts]], [[MemoryBank]] y [[Caching semantico]]
3. Evaluar [[Tool gating]] en catálogos de 20, 50 y 100 herramientas
4. Identificar la combinación óptima mediante [[Diseno factorial 2k]]
5. Localizar umbrales con [[PELT]]

---

## 1.5 Delimitación de la Investigación

→ [[Delimitacion]]

- **Temática**: técnicas de memoria y gestión de contexto en agentes LLM multi-MCP.
- **Lo que no cubre**: fine-tuning de modelos, modificación de pesos, infraestructura de producción.
- **Modelo LLM**: uno o dos modelos de frontera fijos (variable de control).
- **Alcance geográfico/institucional**: investigación aplicada sin caso de negocio específico.
- **Temporal**: el experimento evalúa sesiones de hasta 100 turnos.
