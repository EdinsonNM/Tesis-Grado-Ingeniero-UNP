# Liu et al. (2023) — Lost in the Middle: How Language Models Use Long Contexts

## Referencia APA

Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2023). Lost in the middle: How language models use long contexts. *Transactions of the Association for Computational Linguistics*, 12, 157–173. https://arxiv.org/abs/2307.03172

## Pregunta que responde

¿Cómo utilizan los LLMs la información distribuida a lo largo de contextos largos? ¿Es uniforme el acceso a la información independientemente de su posición?

## Método

Experimentos controlados con multi-document QA y key-value retrieval. Se coloca el documento relevante en distintas posiciones del contexto (inicio, medio, final) y se mide la precisión de respuesta. Evaluado en GPT-3.5, Claude, y otros modelos.

## Métricas reportadas

- Precisión significativamente más alta cuando el documento relevante está al inicio o al final del contexto.
- Degradación pronunciada cuando el documento relevante está en posiciones centrales.
- El efecto es consistente en todos los modelos evaluados y empeora con contextos más largos.

## Aporte a la tesis

Proporciona evidencia empírica del mecanismo de [[Lost in the middle]], uno de los componentes del [[Context rot]]. Justifica por qué la acumulación de resultados intermedios de herramientas en posiciones centrales del contexto activo es problemática: el modelo "olvida" efectivamente información enterrada en el medio. Cita central para la motivación del problema.

## Conceptos relacionados

- [[Lost in the middle]]
- [[Context rot]]
- [[Contexto activo]]
- [[Ventana de contexto]]
- [[Compaction]]
