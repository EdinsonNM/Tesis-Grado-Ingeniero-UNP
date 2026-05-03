# Zhong et al. (2023) — MemoryBank: Enhancing Large Language Models with Long-Term Memory

## Referencia APA

Zhong, W., Guo, L., Gao, Q., Ye, H., & Wang, Y. (2023). MemoryBank: Enhancing large language models with long-term memory. *Proceedings of the AAAI Conference on Artificial Intelligence*, 38. https://arxiv.org/abs/2305.10250

## Pregunta que responde

¿Cómo puede un LLM mantener y actualizar memoria a largo plazo en conversaciones extendidas, priorizando recuerdos más relevantes e imitando el olvido humano adaptativo?

## Método

MemoryBank: banco de memoria externa estructurada donde el LLM almacena y recupera memorias. Incorpora el modelo de olvido de Ebbinghaus: las memorias se debilitan con el tiempo y se refuerzan con el uso. Evaluado con SiliconFriend (chatbot de acompañamiento de larga duración) en conversaciones de semanas.

## Métricas reportadas

- Mejora significativa en consistencia de personalidad y memoria de hechos del usuario a largo plazo vs. LLM sin memoria.
- El mecanismo de Ebbinghaus prioriza memorias relevantes y recientes, mejorando la calidad de recuperación.

## Aporte a la tesis

MemoryBank es una de las técnicas de mitigación del [[Context rot]] evaluadas en la tesis. Representa la familia de soluciones de "memoria externa a largo plazo". La tesis evalúa si [[MemoryBank]] reduce el context rot en escenarios multi-MCP y a qué costo en latencia y tokens.

## Conceptos relacionados

- [[MemoryBank]]
- [[SessionFacts]]
- [[Mem0]]
- [[Context rot]]
- [[Contexto activo]]
- [[Compaction]]
