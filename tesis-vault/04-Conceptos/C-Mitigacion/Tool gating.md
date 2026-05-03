# Tool gating

## Definición

Estrategias que controlan qué herramientas del catálogo MCP se exponen al modelo en cada turno de la conversación, en lugar de exponer el catálogo completo de forma estática desde el inicio de la sesión. El objetivo es reducir el overhead de tokens de descripción de herramientas y mejorar la señal-ruido en el contexto del modelo. (DOC-11, Bloque 6)

También denominado *deferred tool loading* o *dynamic tool selection*.

## El problema que resuelve

En la implementación estándar de MCP, todos los esquemas de herramientas se inyectan en el contexto desde el inicio:

| Configuración | Tokens de overhead de herramientas |
|---|---|
| 1 servidor × 20 herramientas × 200 tokens | ~4,000 tokens |
| 3 servidores | ~12,000 tokens (9% de ventana de 128K) |
| 5 servidores | ~20,000 tokens (16% de ventana de 128K) |

Este overhead ocurre **antes de procesar ninguna consulta** y se mantiene fijo turno a turno (Tang et al., 2025).

## Estrategias principales

**1. Filtrado semántico por relevancia** → [[RAG-MCP]]
La consulta del usuario se convierte en un vector de embeddings que se compara con los embeddings de las descripciones de herramientas. Solo las herramientas con similitud coseno por encima del umbral se exponen al modelo.

> Tang et al. (2025): exposición selectiva de las **k herramientas más relevantes (k típicamente 3–10)** preserva exactitud de selección superior al **95%** incluso con 128 herramientas en el catálogo, con **reducción del 68% en tokens de descripción**.

**2. Carga diferida** (*lazy loading*)
El agente primero razona sobre qué categorías de herramientas necesita, luego solicita que se carguen solo esas categorías. Introduce una ronda extra de razonamiento pero reduce el overhead significativamente en sesiones multi-dominio. Ver [[Sharding]] para la segmentación por dominio.

**3. Selección top-k** (*k* configurable)
Siempre se exponen exactamente las k herramientas más relevantes según el retriever semántico, sin umbral fijo de similitud. Es más predecible que el filtrado por umbral pero menos adaptativo.

## Indicadores de evaluación en la tesis

- **Tokens de descripción de herramientas por turno** — reducción esperada: ~68% (Tang et al., 2025).
- **Tasa de selección correcta de herramienta** — pérdida aceptable: <2% (hipótesis HE3 → [[TOST]]).
- **Tasa de alucinación de parámetros** — debería reducirse al exponer catálogos más pequeños.
- **Latencia adicional** — el filtrado semántico agrega un paso de retrieval que puede subir el p50 levemente.

Hipótesis específica HE3:
> *Tool gating reduce al menos 50% los tokens de descripción de herramientas sin dañar significativamente la selección correcta.* → verificado con [[TOST]] para la dimensión de exactitud.

## Relación con otras técnicas

- [[RAG-MCP]] — implementación concreta del filtrado semántico
- [[Hybrid retrieval]] — mejora la recuperación combinando BM25 + vectores
- [[Sharding]] — divide el catálogo en particiones antes del filtrado
- [[Namespaces]] — aísla herramientas entre servidores para evitar colisiones
- [[Tool overload]] — el problema que tool gating ataca directamente

## Fuentes

- [[Bases Teoricas]] — bloque 6 (desarrollo completo)
- [[Tang 2025 - RAG-MCP]]
- [[Schick 2023 - Toolformer]]
