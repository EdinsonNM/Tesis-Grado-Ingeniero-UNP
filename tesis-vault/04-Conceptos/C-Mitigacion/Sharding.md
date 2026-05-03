# Sharding

## Definición

Técnica de particionamiento que divide un espacio grande de herramientas, documentos o datos en subconjuntos más pequeños (shards), permitiendo que las operaciones de búsqueda y recuperación operen sobre un subconjunto relevante en lugar del espacio completo.

## Motivación en agentes multi-MCP

Cuando un [[Agente LLM]] tiene acceso a decenas o cientos de servidores MCP con miles de herramientas, buscar la herramienta correcta en el espacio completo es costoso (en tokens y latencia). El sharding divide ese espacio por dominio, servidor o tipo de herramienta, reduciendo el espacio de búsqueda efectivo.

## Tipos de sharding relevantes

- **Por servidor MCP**: cada servidor es su propio shard. El agente primero determina a qué servidor dirigirse y luego busca dentro de ese shard.
- **Por dominio funcional**: agrupa herramientas por tipo de operación (lectura, escritura, búsqueda) independientemente del servidor.
- **Por frecuencia de uso**: herramientas más frecuentes en un shard "caliente", las raras en shards secundarios.

## En la tesis

El sharding es una estrategia complementaria al [[Tool gating]]. En los [[Escenarios multi-MCP sinteticos]] con alta dimensionalidad (benchmark [[ToolHaystack]]), el sharding reduce el espacio de búsqueda antes de aplicar filtrado semántico. La combinación sharding + tool gating es una de las configuraciones experimentales.

## Relación con namespaces

Los [[Namespaces]] organizan herramientas por identidad lógica; el sharding las organiza por partición de recuperación. Un namespace puede corresponder a un shard, pero no necesariamente.

## Referencias

- [[Namespaces]]
- [[Tool gating]]
- [[RAG-MCP]]
- [[ToolHaystack]]
- [[Recuperacion federada]]
