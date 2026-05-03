# Brown et al. (2020) — Language Models are Few-Shot Learners

## Referencia APA

Brown, T., Mann, B., Ryder, N., Subbiah, M., Kaplan, J. D., Dhariwal, P., Neelakantan, A., Shyam, P., Sastry, G., Askell, A., Agarwal, S., Herbert-Voss, A., Krueger, G., Henighan, T., Child, R., Ramesh, A., Ziegler, D., Wu, J., Winter, C., … Amodei, D. (2020). Language models are few-shot learners. *Advances in Neural Information Processing Systems*, 33, 1877–1901. https://arxiv.org/abs/2005.14165

## Pregunta que responde

¿Pueden los modelos de lenguaje de gran escala realizar tareas diversas con pocos o ningún ejemplo de entrenamiento específico (few-shot / zero-shot)?

## Método

Entrenamiento de GPT-3 (175B parámetros) en texto web a gran escala. Evaluación en 42 benchmarks con prompting in-context (0-shot, 1-shot, few-shot) sin fine-tuning específico por tarea.

## Métricas reportadas

- Estado del arte o near-SOTA en múltiples benchmarks de NLP con few-shot prompting.
- Emergencia de capacidades no vistas en modelos más pequeños.
- La ventana de contexto de GPT-3 es de 2048 tokens.

## Aporte a la tesis

Establece el paradigma de LLMs de gran escala como motores de razonamiento general. La [[Ventana de contexto]] de 2048 tokens de GPT-3 fue el punto de partida; los modelos actuales la han ampliado dramáticamente, lo que hace el problema del [[Context rot]] más relevante, no menos: más contexto disponible incentiva a los desarrolladores a llenarlo.

## Conceptos relacionados

- [[Modelo de lenguaje de gran escala]]
- [[Ventana de contexto]]
- [[Agente LLM]]
- [[Context rot]]
