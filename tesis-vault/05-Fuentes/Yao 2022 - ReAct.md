# Yao et al. (2022) — ReAct: Synergizing Reasoning and Acting in Language Models

## Referencia APA

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. *International Conference on Learning Representations (ICLR 2023)*. https://arxiv.org/abs/2210.03629

## Pregunta que responde

¿Puede un LLM intercalar razonamiento verbal explícito (pensamiento) y acciones externas (herramientas) en un ciclo iterativo para resolver tareas complejas de manera más efectiva?

## Método

Prompting de pocos ejemplos en LLMs (PaLM, GPT-3) que interleava pensamientos y acciones. Evaluado en: HotpotQA, FEVER (búsqueda web), ALFWorld, WebShop (tareas de decisión secuencial).

## Métricas reportadas

- Mejora de 34% sobre ActOnly y ThinkOnly en HotpotQA.
- Reducción de alucinaciones respecto a Chain-of-Thought puro (sin acceso a herramientas).
- Mejor interpretabilidad al exponer el razonamiento intermedio.

## Aporte a la tesis

Define el ciclo operativo del [[Agente LLM]] que es la unidad experimental de la tesis: razonamiento → acción (llamada a herramienta) → observación (resultado) → razonamiento. Cada observación se acumula en el [[Contexto activo]], lo que establece el mecanismo de crecimiento que produce el [[Context rot]].

## Conceptos relacionados

- [[Agente LLM]]
- [[Contexto activo]]
- [[Context rot]]
- [[Tool overload]]
- [[Servidor MCP]]
