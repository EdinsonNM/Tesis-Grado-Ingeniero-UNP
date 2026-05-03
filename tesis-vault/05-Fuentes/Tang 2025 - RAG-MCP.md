# Tang et al. (2025) — RAG-MCP: Mitigating Prompt Bloat in LLM Tool Selection via Retrieval-Augmented Generation

## Referencia APA

Tang, Y., & Gan, Z. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. *arXiv preprint*. https://arxiv.org/abs/2505.03275

## Pregunta que responde

¿Puede RAG aplicarse sobre el espacio de herramientas MCP para reducir el "prompt bloat" causado por incluir todos los esquemas de herramientas en cada solicitud al LLM?

## Método

RAG-MCP: en lugar de pasar todos los esquemas de herramientas al LLM, un retriever selecciona las k herramientas más relevantes para la consulta actual y solo esas se incluyen en el contexto. Evaluado en MCPBench con métricas de éxito de selección de herramientas y reducción de tokens.

## Métricas reportadas

- Reducción significativa del tamaño del contexto activo al filtrar herramientas irrelevantes.
- Mejora en la tasa de selección correcta de herramientas vs. incluir todas las herramientas.
- Reducción de alucinaciones de herramientas en escenarios con muchos servidores MCP.

## Aporte a la tesis

RAG-MCP es el antecedente más directo del [[Tool gating]] como técnica de mitigación del [[Context rot]] en arquitecturas multi-MCP. La tesis extiende este trabajo evaluándolo en el marco del [[IQCR]] y comparándolo sistemáticamente contra otras técnicas de mitigación usando un [[Diseno factorial 2k]].

## Conceptos relacionados

- [[RAG-MCP]]
- [[Tool gating]]
- [[Context rot]]
- [[Servidor MCP]]
- [[Model Context Protocol]]
- [[Hybrid retrieval]]
- [[Tool overload]]
