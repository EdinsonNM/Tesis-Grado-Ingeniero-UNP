# Hybrid retrieval

## Definición

Estrategia de recuperación de información que combina dos paradigmas complementarios:

- **Recuperación léxica (BM25)**: busca coincidencia de términos exactos. Alta precisión cuando el usuario sabe el término exacto.
- **Recuperación semántica (vectores)**: busca similitud de significado mediante embeddings. Alta cobertura para sinónimos y paráfrasis.

Los resultados de ambas se fusionan, típicamente mediante *Reciprocal Rank Fusion* (RRF) u otras estrategias de reranking.

## Ventaja sobre cada paradigma por separado

- BM25 falla con sinónimos y consultas semánticas.
- Recuperación vectorial falla con términos técnicos muy específicos (nombres de funciones, IDs, siglas).
- Hybrid retrieval captura lo mejor de ambos: exactitud léxica + cobertura semántica.

## Implementaciones comunes

- **Elasticsearch / OpenSearch**: BM25 nativo + dense vector search.
- **Weaviate, Qdrant**: hybrid search integrado.
- **LangChain EnsembleRetriever**: combina cualquier par de retrievers.

## En la tesis

Se usa como base para el [[RAG-MCP]] y la [[Recuperacion federada]]. La recuperación de herramientas relevantes de entre los [[Servidor MCP|servidores MCP]] disponibles se beneficia del hybrid retrieval: los nombres de herramientas son léxicamente específicos, pero la intención del usuario es semántica.

## Referencias

- [[RAG]]
- [[RAG-MCP]]
- [[Recuperacion federada]]
- [[Tool gating]]
- [[Caching semantico]]
