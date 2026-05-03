# Prompt caching

## Definición

Mecanismo ofrecido por algunos proveedores de LLM (Anthropic, OpenAI) que permite reutilizar el procesamiento previo de un prefijo de prompt que no cambia entre solicitudes. Si el inicio del contexto (instrucciones del sistema, documentos de referencia, esquemas de herramientas) es idéntico entre llamadas, el proveedor lo "cachea" internamente y cobra un precio reducido por esos tokens en solicitudes subsiguientes.

## Cómo funciona

La inferencia en un Transformer implica calcular los KV-caches para todos los tokens de entrada. Si el prefijo del prompt es el mismo, esos KV-caches pueden reutilizarse. Esto reduce tanto el costo como la latencia ([[TTFT]]) para los tokens del prefijo.

En Anthropic: los tokens de prefijo cacheados cuestan 10% del precio normal en escritura y 0% en lectura (con un mínimo de 1024 tokens para activar el cache).

## Diferencia con caching semántico

- **Prompt caching**: el caching lo hace el proveedor de la API a nivel de KV-cache. Requiere prefijos **idénticos** byte a byte.
- **[[Caching semantico]]**: el caching lo implementa el sistema del agente. Funciona con consultas **similares** (no necesariamente idénticas) y opera sobre los resultados de herramientas, no sobre el procesamiento del prompt.

Son complementarios: prompt caching reduce el costo del prefijo fijo; caching semántico reduce el costo de las llamadas a herramientas repetidas.

## En la tesis

El prompt caching es relevante para la dimensión de [[Eficiencia de tokens]] del [[IQCR]]. Los esquemas de herramientas MCP son un candidato natural para prompt caching: son largos y no cambian entre turnos. Las técnicas como [[Tool gating]] reducen el tamaño de los esquemas, pero si no se aplica gating, prompt caching mitiga su costo.

## Referencias

- [[Caching semantico]]
- [[Eficiencia de tokens]]
- [[TTFT]]
- [[Tool gating]]
- [[Contexto activo]]
