# Realidad Problemática

→ Sección 1.1 del capítulo [[Cap 1 - Aspectos de la Problematica]]
Fuente: `DOC-06_Realidad_Problematica.docx`

---

## La expansión global de la IA generativa

La inteligencia artificial generativa ha experimentado una expansión sin precedentes, transformando de forma estructural cómo organizaciones y personas interactúan con los sistemas computacionales.

**Cifras clave (2024-2025)**:
- Adopción de IA generativa creció **más del 80%** entre octubre 2024 y mediados 2025 (Microsoft, 2025).
- Aproximadamente **1 de cada 6 personas** en el mundo usa activamente herramientas de IA generativa.
- Adopción empresarial global: **78% de las organizaciones** en 2024.
- **92% de las empresas Fortune 500** reportan uso activo de IA generativa en sus flujos de trabajo (Menlo Ventures, 2025).
- Gasto empresarial en IA generativa: **$37 mil millones en 2025** vs. $11.5 mil millones en 2024 (crecimiento 3.2×).
- Mercado de LLMs empresariales proyecta: **$8.8B (2025) → $71.1B (2034)**, CAGR del 26.1%.
- Las organizaciones pusieron **11 veces más modelos en producción** en 2025 vs. el año anterior (Databricks, 2025).
- **Gartner (2025) predice que más del 40% de los proyectos de IA agéntica serán cancelados antes de 2027** por costos escalantes y complejidad técnica de despliegue en producción — evidencia de que construir agentes confiables sigue siendo un problema no resuelto.

En el centro de esta transformación están los **agentes LLM**: sistemas que dotan a los modelos de herramientas externas, capacidad de planificación y memoria persistente (Yao et al., 2022; Schick et al., 2023).

---

## El surgimiento del MCP y los agentes multi-herramienta

En **noviembre de 2024**, Anthropic publicó el [[Model Context Protocol]] (MCP): un estándar abierto que define cómo los asistentes de IA se integran con repositorios de contenido, herramientas de gestión empresarial y entornos de desarrollo.

El MCP resolvió el problema de la fragmentación de integraciones: cada herramienta requería código ad hoc. Con MCP, cualquier [[Servidor MCP|servidor MCP]] compatible puede ser invocado por cualquier cliente MCP sin desarrollo adicional. Esta estandarización aceleró exponencialmente la adopción de arquitecturas multi-servidor.

---

## El problema: context rot en arquitecturas multi-MCP

A medida que los agentes LLM se conectan a más servidores MCP simultáneamente, emergen tres mecanismos de degradación que se potencian mutuamente:

**1. [[Tool overload]]** — El catálogo de herramientas de múltiples servidores se expone completo al modelo en cada turno. Para 3–5 servidores MCP con 20 herramientas cada uno, el overhead de tokens de descripción alcanza 12,000–20,000 tokens *antes de procesar ninguna consulta* (Tang et al., 2025).

**2. Acumulación de resultados intermedios** — En el ciclo ReAct, cada invocación de herramienta agrega su resultado al [[Contexto activo]]. En conversaciones de 50+ turnos con múltiples herramientas por turno, estos resultados enterran en el centro del contexto las instrucciones y el historial más relevantes, activando el efecto [[Lost in the middle]].

**3. Mezcla de estados de sesión** — Los metadatos de múltiples servidores coexisten sin separación: mensajes de error, avisos de autenticación, paginación de resultados. Esta mezcla introduce ruido que confunde al modelo sobre qué servidor respondió qué.

El resultado acumulado es el **[[Context rot]]**: degradación progresiva de exactitud, aumento de alucinaciones, pérdida de coherencia, mayor latencia y costo creciente de tokens.

**Evidencia empírica**:
- Chroma Research (2025): **degradación superior al 30%** en exactitud de respuestas de agentes en producción después de 50 turnos.
- Redis Labs (2025): el **67% del costo operativo de inferencia** en sistemas multi-herramienta se atribuye a acumulación de contexto, no a generación nueva.
- Tang et al. (2025): la tasa de alucinación en parámetros de herramientas **aumenta 23%** al pasar de 10 a 50 herramientas disponibles.
- **Vercel (2025)**: el equipo de infraestructura redujo las herramientas expuestas al agente d0 (CI/CD) de 17-18 a las operaciones mínimas necesarias. Resultado: tasa de éxito 80%→**100%**, consumo de tokens **−37%**, velocidad **3.5×**, pasos por tarea **−42%**. Primer caso documentado de mejora cuantificable mediante reducción de herramientas en un agente de producción real.

---

## La brecha: ausencia de un protocolo de comparación

Existen técnicas de mitigación documentadas en la literatura — [[RAG]], [[Tool gating]], [[SessionFacts]], [[MemoryBank]], [[Caching semantico]] — pero:

- Cada técnica ha sido evaluada en escenarios distintos con métricas inconsistentes.
- Ningún estudio las compara sistemáticamente en el contexto específico de **arquitecturas multi-MCP**.
- No existe evidencia empírica de qué combinaciones producen los mejores resultados ni a qué costo.
- No se han identificado los **umbrales estadísticos** a partir de los cuales el context rot se vuelve significativo.

Esta brecha — la falta de un protocolo experimental unificado para arquitecturas multi-MCP — es el espacio que la presente tesis busca llenar.

---

## Conceptos relacionados

- [[Context rot]] — [[Tool overload]] — [[Lost in the middle]]
- [[Agente LLM]] — [[Model Context Protocol]] — [[Servidor MCP]]
- [[Contexto activo]] — [[Ventana de contexto]]
- [[Problema de investigacion]] — [[Justificacion e Importancia]]
