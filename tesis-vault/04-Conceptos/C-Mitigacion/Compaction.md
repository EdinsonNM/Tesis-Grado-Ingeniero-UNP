# Compaction

## Definición

Técnica de reducción del [[Contexto activo]] que comprime, resume o poda el contenido acumulado en la conversación para mantenerlo por debajo de un umbral deseado, sin descartar información crítica.

## Estrategias de compaction

1. **Resumen progresivo**: los turnos más antiguos se reemplazan por un resumen generado por el LLM. El resumen ocupa menos tokens que el historial completo.
2. **Eliminación de resultados intermedios**: los resultados de llamadas a herramientas que ya fueron procesados y cuya información fue integrada se eliminan del contexto.
3. **Compresión selectiva**: se identifican los fragmentos de menor relevancia (bajo peso de atención o baja utilidad estimada) y se eliminan o comprimen.
4. **Sliding window**: se mantiene solo una ventana fija de los N turnos más recientes.

## Trade-off

Toda compaction implica pérdida potencial de información. El riesgo es que el resumen no capture un detalle que el modelo necesitará más adelante. Las estrategias más sofisticadas (compresión selectiva) minimizan esta pérdida pero tienen mayor costo computacional.

## Relación con MemGPT

MemGPT (Packer et al., 2023) implementa un sistema de memoria virtual inspirado en sistemas operativos: el contexto en ventana es como RAM, y hay un almacenamiento externo como disco. La compaction es equivalente a "paginar" contenido desde RAM al disco.

## En la tesis

Es una de las técnicas de mitigación del [[Context rot]] consideradas en el marco teórico. Se evalúa en términos de su efecto sobre el [[IQCR]] y los costos de tokens ([[Eficiencia de tokens]]) y latencia ([[TTFT]]).

## Referencias

- [[Contexto activo]]
- [[Context rot]]
- [[MemoryBank]]
- [[SessionFacts]]
- [[Eficiencia de tokens]]
- [[TTFT]]
