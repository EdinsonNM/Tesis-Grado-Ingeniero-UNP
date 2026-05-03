# Vercel (2025) — We removed 80% of our agent's tools

## Referencia APA

Vercel. (2025, diciembre). *We removed 80% of our agent's tools*. Vercel Blog. https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools

## Tipo de fuente

Reporte técnico de industria / caso de producción real.

## Contexto

El equipo de Vercel desarrolló el agente **d0** para gestión autónoma de infraestructura y CI/CD. El agente recibía acceso completo a los servidores MCP del entorno: 17-18 herramientas relacionadas con operaciones de filesystem, ejecución de comandos y despliegues.

---

## Problema identificado

Al analizar los patrones de uso real del agente, el equipo descubrió que d0 solo utilizaba un subconjunto muy pequeño de las herramientas disponibles en la práctica. La presencia de herramientas no utilizadas producía:

- Confusión en la selección (el modelo consideraba opciones irrelevantes en cada turno).
- Overhead de tokens en las descripciones de herramientas (presentes en cada llamada).
- Decisiones subóptimas cuando el espacio de opciones era demasiado amplio.

---

## Intervención

Reducción **estática** del catálogo: eliminación permanente de todas las herramientas que no eran esenciales para las tareas del agente, conservando solo las operaciones mínimas de filesystem necesarias para su rol.

---

## Resultados cuantificados

| Métrica | Antes | Después | Cambio |
|---|---|---|---|
| Tasa de éxito por tarea | 80% | 100% | +20 pp |
| Consumo de tokens | 100% (base) | 63% | −37% |
| Velocidad de ejecución | 1× | 3.5× | +250% |
| Pasos por tarea | 100% (base) | 58% | −42% |

---

## Relevancia para la tesis

**Evidencia de producción del impacto de [[Tool overload]]**: el caso d0 demuestra empíricamente, en un entorno real de CI/CD, que reducir el número de herramientas expuestas produce mejoras sustanciales en exactitud, eficiencia de tokens, velocidad y coherencia de ejecución.

**Distinción clave con la propuesta de la tesis**:
- Vercel aplicó reducción *estática*: herramientas eliminadas permanentemente según el rol específico del agente.
- La tesis propone filtrado *dinámico* via [[RAG-MCP]]: recuperar en cada turno solo las herramientas semánticamente relevantes para la consulta actual, sin eliminar nada del catálogo.
- El enfoque dinámico es más general: aplica a agentes multi-propósito donde el conjunto óptimo de herramientas varía por turno.

**Uso en el documento**:
- [[Realidad Problematica]] — como tercer caso de evidencia empírica junto a Chroma y Redis Labs.
- [[Bases Teoricas]] (Bloque 4) — evidencia empírica del [[Context rot]] por [[Tool overload]].
- [[Bases Teoricas]] (Bloque 6) — distinción estático vs. dinámico en sección de [[Tool gating]].
- [[Marco Referencial]] — Categoría G: Casos de Producción.
- Antecedentes (2.1) — como antecedente de industria en la sección de filtrado de herramientas.

---

## Notas metodológicas

- Es un blog post técnico, no un paper revisado por pares. Citar como evidencia de industria, no como evidencia académica.
- Los resultados son observacionales (A/B en producción), no provienen de un experimento controlado.
- Las métricas exactas son públicas y reproducibles para el agente d0 específico; no son generalizables sin replicación.

---

## Conceptos relacionados

[[Tool overload]] · [[Tool gating]] · [[RAG-MCP]] · [[Context rot]] · [[Servidor MCP]]
