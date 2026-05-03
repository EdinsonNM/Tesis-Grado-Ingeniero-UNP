# Packer et al. (2023) — MemGPT: Towards LLMs as Operating Systems

## Referencia APA

Packer, C., Fang, V., Patil, S. G., Lin, K., Wooders, S., & Gonzalez, J. E. (2023). MemGPT: Towards LLMs as operating systems. *arXiv preprint*. https://arxiv.org/abs/2310.08560

## Pregunta que responde

¿Es posible dotar a un LLM de memoria ilimitada y persistente simulando la jerarquía de memoria de un sistema operativo (RAM / disco)?

## Método

MemGPT implementa un sistema donde el LLM tiene acceso a: (1) memoria en contexto (análogo a RAM) y (2) almacenamiento externo (análogo a disco). El propio LLM controla qué información paginar hacia/desde el almacenamiento externo mediante funciones especiales. Evaluado en conversación de documentos extensos y memoria conversacional persistente.

## Métricas reportadas

- Capacidad de mantener conversaciones coherentes que exceden largamente la ventana de contexto.
- El LLM como sistema operativo de su propia memoria: toma decisiones autónomas de paginación.
- Evaluación cualitativa de coherencia en conversaciones de cientos de turnos.

## Aporte a la tesis

Es el antecedente directo del [[MemoryBank]] y arquitecturas similares. Establece el principio de memoria externa administrada por el agente. La distinción RAM/disco es la base conceptual de las técnicas de memoria que se evalúan en la tesis. También introduce el concepto de [[Compaction]] implícito en la gestión del contexto en ventana.

## Conceptos relacionados

- [[MemoryBank]]
- [[SessionFacts]]
- [[Compaction]]
- [[Contexto activo]]
- [[Ventana de contexto]]
- [[Agente LLM]]
