# RAG-MCP

## Definición

Aplicación del paradigma [[RAG]] al catálogo de herramientas MCP. En lugar de exponer el catálogo completo al modelo en cada turno, se recuperan semánticamente solo las herramientas más relevantes para la consulta actual. (DOC-11, Bloque 5–6; Tang et al., 2025)

Es la implementación concreta del [[Tool gating]] mediante filtrado semántico por relevancia.

## Evidencia empírica

> Tang et al. (2025) evaluaron RAG-MCP en escenarios con catálogos de **128 herramientas** y reportaron una **reducción del 68% en el consumo de tokens de descripción de herramientas** con una pérdida de exactitud inferior al **2%** en tareas de selección de herramientas.

| Métrica | Resultado Tang et al. (2025) |
|---|---|
| Reducción de tokens de descripción | **−68%** |
| Pérdida de exactitud en selección | **<2%** |
| Tamaño de catálogo evaluado | 128 herramientas |
| k óptimo (herramientas expuestas) | 3–10 por turno |
| Umbral de preservación de exactitud | >95% con k=5 |

Este resultado es la base empírica de la hipótesis específica **HE3**:
> *Tool gating reduce al menos 50% los tokens de descripción de herramientas sin dañar significativamente la selección correcta.* → verificado con [[TOST]] para la dimensión de exactitud.

## Arquitectura

```
Consulta del usuario
      ↓
  Embedding de la consulta (e.g. text-embedding-3-small)
      ↓
  Búsqueda coseno en índice vectorial de descripciones de herramientas
      ↓
  Top-k herramientas más relevantes (k configurable, típicamente 3–10)
      ↓
  Solo esas k descripciones se inyectan en el contexto del modelo
      ↓
  El modelo selecciona herramienta → invoca → recibe resultado
```

Las herramientas no seleccionadas permanecen en el catálogo pero **no consumen tokens** en ese turno.

## Problema que aborda

Mitiga directamente el [[Tool overload]]: el overhead de 12,000–20,000 tokens de descripción (3–5 servidores MCP) se reduce a los tokens de k herramientas relevantes por turno, antes de procesar ninguna consulta.

## Diferencia entre RAG-MCP y RAG de historial

| Dimensión | RAG de historial | RAG-MCP |
|---|---|---|
| Objeto recuperado | Turnos pasados del historial | Descripciones de herramientas del catálogo |
| Índice vectorial | Embeddings de mensajes | Embeddings de esquemas de herramientas |
| Problema mitigado | Acumulación de observaciones | Tool overload |
| Benchmark de evaluación | [[LongMemEval]], [[LoCoMo]] | [[ToolHaystack]], [[SimpleToolHalluBench]] |

## Indicadores de evaluación en la tesis

- **Tokens de descripción por turno** — reducción esperada: ≥50% (HE3).
- **Tasa de selección correcta de herramienta** — pérdida aceptable: <2% (equivalencia por TOST).
- **Tasa de alucinación de parámetros** — debería reducirse al reducir el catálogo visible.
- **Latencia adicional** — el paso de embedding + búsqueda coseno agrega latencia antes de la generación.

## Relación con otras técnicas

- [[Tool gating]] — concepto padre; RAG-MCP es su implementación semántica
- [[Hybrid retrieval]] — combina BM25 + vectores para mejorar la recuperación
- [[Sharding]] — divide el catálogo en particiones antes del filtrado semántico
- [[Tool overload]] — el problema que RAG-MCP ataca directamente
- [[TOST]] — prueba estadística para verificar la equivalencia de exactitud

## Fuentes

- [[Bases Teoricas]] — bloques 5 y 6
- [[Tang 2025 - RAG-MCP]]
- [[Lewis 2020 - RAG]] — fundamento del paradigma de recuperación aumentada

