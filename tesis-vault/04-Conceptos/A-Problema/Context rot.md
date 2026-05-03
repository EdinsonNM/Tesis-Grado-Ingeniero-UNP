# Context rot

## Definición operacional

Proceso de degradación progresiva y acumulativa de la calidad de respuestas de un [[Agente LLM]], producido por el crecimiento del [[Contexto activo]] en conversaciones multi-turno con acceso a múltiples [[Servidor MCP|servidores MCP]]. El término proviene de la práctica industrial (Chroma Research, 2025) y captura la analogía con el deterioro de datos en sistemas de almacenamiento: así como los datos se corrompen por acumulación de errores, el contexto se degrada por acumulación de información irrelevante, redundante o contradictoria.

## Tres mecanismos en arquitecturas multi-MCP

**1. [[Tool overload]]**
El catálogo de herramientas de múltiples servidores se expone completo al modelo en cada turno.
- Patil et al. (2023): degradación en selección de herramientas cuando el catálogo supera **20 herramientas**.
- Tang et al. (2025): la tasa de alucinación en parámetros de herramientas **aumenta 23%** al pasar de 10 a 50 herramientas disponibles.

**2. Acumulación de resultados intermedios**
Los resultados de cada llamada a herramienta se concatenan al historial, ocupando la región central del contexto.
- Liu et al. (2023): **reducción de hasta 40%** en la utilización efectiva de información en el centro del contexto vs. los extremos → efecto [[Lost in the middle]].

**3. Mezcla de estados de sesión**
Los metadatos de múltiples servidores (errores, autenticación, paginación) coexisten sin separación semántica.
- Chroma Research (2025): la tasa de error en atribución de resultados a servidores crece del **3% (1 servidor) al 18% (5 servidores)**.

## Evidencia empírica

| Fuente | Hallazgo clave |
|---|---|
| Liu et al. (2023) | -40% atención efectiva en posiciones centrales del contexto |
| Shi et al. (2023) | Información irrelevante reduce exactitud de razonamiento hasta **-65%** |
| **Chroma Research (2025)** | **>30% degradación en exactitud** después de 50 turnos en producción |
| Redis Labs (2025) | **67% del costo de inferencia** atribuible a acumulación de contexto |
| Tang et al. (2025) | +23% alucinación de parámetros al pasar de 10 a 50 herramientas |

> El 30% de degradación de Chroma Research (2025) es el **umbral de referencia** para la hipótesis general de la tesis (HG): se espera que al menos una configuración de técnicas revierta esta degradación completamente.

## Cómo se mide

Se mide mediante el [[IQCR]] y sus componentes:
- [[Exactitud de respuesta]] — comparación contra [[Ground truth]]
- [[Tasa de alucinacion]] — afirmaciones incorrectas
- [[Coherencia conversacional]] — consistencia a lo largo de la conversación
- [[Eficiencia de tokens]] — tokens consumidos por turno
- [[Latencia p50 p95]] + [[TTFT]] — distribución de tiempos de respuesta

El algoritmo [[PELT]] detecta los **umbrales estadísticos** — el punto exacto de la curva donde el context rot se vuelve estadísticamente significativo.

## Técnicas de mitigación estudiadas

- [[Tool gating]] — reduce el overhead del catálogo de herramientas
- [[SessionFacts]] — comprime el estado de sesión
- [[MemoryBank]] · [[Mem0]] — memoria externa a largo plazo
- [[Caching semantico]] — reduce llamadas redundantes a herramientas
- [[Recuperacion federada]] — recuperación selectiva desde múltiples fuentes
- [[Compaction]] — compresión directa del contexto activo

## Fuentes

- [[Bases Teoricas]] — bloque 4 (desarrollo completo)
- [[Liu 2023 - Lost in the Middle]]
- [[Realidad Problematica]]
