# Schick et al. (2023) — Toolformer: Language Models Can Teach Themselves to Use Tools

## Referencia APA

Schick, T., Dwivedi-Yu, J., Dessì, R., Raileanu, R., Lomeli, M., Zettlemoyer, L., Cancedda, N., & Scialom, T. (2023). Toolformer: Language models can teach themselves to use tools. *Advances in Neural Information Processing Systems*, 36. https://arxiv.org/abs/2302.04761

## Pregunta que responde

¿Puede un LLM aprender de forma auto-supervisada cuándo y cómo llamar a herramientas externas, sin supervisión humana explícita?

## Método

Auto-supervisión: el modelo genera candidatos de llamadas a herramientas, ejecuta las herramientas y filtra las llamadas que reducen la perplejidad. El corpus resultante se usa para fine-tuning. Herramientas evaluadas: calculadora, motor de búsqueda, traductor, calendario, QA.

## Métricas reportadas

- GPT-J (6B) con Toolformer supera GPT-3 (175B) en varias tareas de razonamiento aritmético y factual.
- La selección auto-supervisada produce llamadas de herramienta más precisas y menos frecuentes (eficientes) que baselines.

## Aporte a la tesis

Establece que los LLMs pueden aprender a usar herramientas de forma selectiva. La selección selectiva (llamar solo cuando es necesario) es el principio detrás del [[Tool gating]]: no exponer todas las herramientas todo el tiempo, sino activarlas cuando hay señal de relevancia.

## Conceptos relacionados

- [[Tool gating]]
- [[Tool overload]]
- [[Agente LLM]]
- [[Servidor MCP]]
