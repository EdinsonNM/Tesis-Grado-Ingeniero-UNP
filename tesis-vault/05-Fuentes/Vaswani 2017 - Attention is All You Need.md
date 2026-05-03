# Vaswani et al. (2017) — Attention is All You Need

## Referencia APA

Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is all you need. *Advances in Neural Information Processing Systems*, 30. https://arxiv.org/abs/1706.03762

## Pregunta que responde

¿Es posible construir un modelo de secuencia-a-secuencia de alto rendimiento basado únicamente en mecanismos de atención, eliminando recurrencia y convolución?

## Método

Propuesta de la arquitectura Transformer: encoders y decoders basados en multi-head self-attention y feed-forward. Evaluado en traducción automática (WMT 2014 inglés-alemán e inglés-francés). Entrenamiento en 8 GPUs P100 durante 12 horas (modelo base).

## Métricas reportadas

- BLEU 28.4 en EN-DE (estado del arte en 2017).
- BLEU 41.0 en EN-FR.
- Menor costo de entrenamiento que modelos recurrentes y convolucionales comparables.

## Aporte a la tesis

Define la arquitectura base de los [[Modelo de lenguaje de gran escala|LLMs]] modernos. La [[Ventana de contexto]] y el mecanismo de atención que da origen al efecto [[Lost in the middle]] son propiedades directas de la arquitectura Transformer. Cita fundacional del marco teórico.

## Conceptos relacionados

- [[Modelo de lenguaje de gran escala]]
- [[Ventana de contexto]]
- [[Lost in the middle]]
- [[Agente LLM]]
