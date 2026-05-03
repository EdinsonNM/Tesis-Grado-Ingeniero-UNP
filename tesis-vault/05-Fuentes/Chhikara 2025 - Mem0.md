# Chhikara et al. (2025) — Mem0: The Memory Layer for Personalized AI

## Referencia APA

Chhikara, P., Agrawal, K., Khandelwal, T., Singh, P., & Khandelwal, I. (2025). Mem0: The memory layer for personalized AI. *arXiv preprint*. https://arxiv.org/abs/2504.19413

## Pregunta que responde

¿Puede una capa de memoria adaptativa y autogestionada mejorar la personalización y coherencia de agentes de IA en conversaciones largas y multi-sesión, con bajo costo computacional?

## Método

Mem0 implementa una capa de memoria que extrae, indexa y recupera automáticamente recuerdos relevantes del historial de conversación. Usa almacenamiento vectorial para recuperación semántica y un LLM ligero para extracción y resolución de contradicciones en memoria. Evaluado en LOCOMO y comparado con GPT-4, Claude y otros sistemas de memoria.

## Métricas reportadas

- Mejora de ~26% en score de memoria a largo plazo vs. GPT-4 con full context.
- Reducción de ~91% en uso de tokens vs. full context.
- Latencia p50 comparable a sistemas sin memoria externa.

## Aporte a la tesis

Mem0 es la implementación más reciente y eficiente de la familia de memorias externas. Sus métricas de reducción de tokens (~91%) son un benchmark de referencia para comparar las técnicas de la tesis en la dimensión de [[Eficiencia de tokens]]. La tesis evalúa si la reducción de context rot que logra Mem0 en conversaciones personales se replica en escenarios multi-MCP.

## Conceptos relacionados

- [[Mem0]]
- [[MemoryBank]]
- [[Context rot]]
- [[Eficiencia de tokens]]
- [[LoCoMo]]
- [[Agente LLM]]
