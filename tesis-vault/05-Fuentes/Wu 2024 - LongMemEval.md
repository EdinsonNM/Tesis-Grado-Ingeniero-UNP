# Wu et al. (2024) — LongMemEval: Benchmarking Chat Assistants on Long-Term Interactive Memory

## Referencia APA

Wu, D., Truong, K., & Ho, J. (2024). LongMemEval: Benchmarking chat assistants on long-term interactive memory. *arXiv preprint*. https://arxiv.org/abs/2410.10813

Dataset: https://huggingface.co/datasets/xiaowu0162/longmemeval-cleaned | Código: https://github.com/xiaowu0162/LongMemEval

## Pregunta que responde

¿Cómo evaluar la capacidad de los asistentes de chat para recordar y razonar sobre información de sesiones pasadas, específicamente en el contexto de memoria a largo plazo multi-sesión?

## Método

LongMemEval: 500 preguntas diseñadas para evaluar 5 capacidades de memoria: extracción de información de turno único, extracción multi-turno, razonamiento temporal, razonamiento de conocimiento y abstención (saber cuándo no se recuerda). Las conversaciones tienen hasta 115K tokens de historial. Se evalúan sistemas con: full context, RAG, y gestores de memoria.

## Métricas reportadas

- Los LLMs de frontera (GPT-4, Claude) degradan en Q&A de memoria a largo plazo con conversaciones largas.
- RAG sobre el historial mejora significativamente vs. truncar contexto.
- La abstención (saber que no se recuerda algo) es el tipo más difícil para todos los modelos.
- Hay trade-off claro entre latencia, costo y precisión de memoria según la estrategia usada.

## Aporte a la tesis

LongMemEval es el benchmark más relevante para la dimensión de [[Exactitud de respuesta]] y [[Coherencia conversacional]] del [[IQCR]] en escenarios de memoria a largo plazo. Sus 5 tipos de preguntas de memoria mapean directamente a los escenarios multi-MCP donde el agente necesita recordar qué herramientas usó, qué resultados obtuvo y qué compromisos adquirió en turnos anteriores.

## Conceptos relacionados

- [[LongMemEval]]
- [[Exactitud de respuesta]]
- [[Coherencia conversacional]]
- [[Dataset de evaluacion]]
- [[MemoryBank]]
- [[Mem0]]
- [[SessionFacts]]
- [[RAG]]
