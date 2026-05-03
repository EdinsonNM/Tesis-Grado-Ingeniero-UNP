# Lewis et al. (2020) — Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks

## Referencia APA

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. *Advances in Neural Information Processing Systems*, 33, 9459–9474. https://arxiv.org/abs/2005.11401

## Pregunta que responde

¿Puede un modelo generativo mejorar su precisión factual combinando generación con recuperación de documentos relevantes, sin re-entrenar para cada tarea?

## Método

Arquitectura RAG: un retriever denso (DPR) recupera documentos de Wikipedia y los pasa como contexto a un generador seq2seq (BART). Dos variantes: RAG-Sequence (mismo documento para toda la respuesta) y RAG-Token (documento por token). Evaluado en NQ, TriviaQA, WebQ, CuratedTrec, MS-MARCO, Jeopardy, FEVER.

## Métricas reportadas

- Estado del arte en NQ, TriviaQA, WebQ.
- Superior a modelos paramétricos en tareas de conocimiento abierto.
- Generaciones más específicas, diversas y factuales que seq2seq sin retrieval.

## Aporte a la tesis

Es la base conceptual de [[RAG]] y [[RAG-MCP]]. El principio de recuperar solo lo relevante en lugar de tenerlo todo en contexto es análogo al [[Tool gating]]: en lugar de tener todos los documentos en la ventana de contexto, se recuperan los pertinentes. Este principio se extiende a herramientas MCP en la tesis.

## Conceptos relacionados

- [[RAG]]
- [[RAG-MCP]]
- [[Tool gating]]
- [[Recuperacion federada]]
- [[Hybrid retrieval]]
- [[Context rot]]
