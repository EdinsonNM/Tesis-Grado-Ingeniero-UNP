# Dataset de evaluacion

## Definicion

Un dataset de evaluacion es un conjunto organizado de casos de prueba usado para medir el desempeno de un sistema.

En esta tesis, un dataset puede incluir:

- conversaciones largas;
- preguntas por turno;
- respuestas esperadas;
- catalogos de herramientas;
- herramientas distractoras;
- resultados esperados de herramientas;
- metadatos de sesion;
- etiquetas de coherencia o alucinacion.

## Diferencia con ground truth

El dataset es el paquete completo de evaluacion. El [[Ground truth]] es la verdad de referencia contenida o derivada de ese paquete.

```text
Dataset de evaluacion = caso completo
Ground truth = respuesta, etiqueta, tool o parametro correcto
```

## Datasets mencionados en la tesis

- [[LongMemEval]]
- [[LoCoMo]]
- [[SimpleToolHalluBench]]
- [[ToolHaystack]]
- [[Escenarios multi-MCP sinteticos]]

## URLs de acceso

| Dataset / benchmark | Paper | Codigo / datos |
|---|---|---|
| [[LongMemEval]] | [arXiv:2410.10813](https://arxiv.org/abs/2410.10813) | [GitHub](https://github.com/xiaowu0162/LongMemEval), [Hugging Face cleaned](https://huggingface.co/datasets/xiaowu0162/longmemeval-cleaned) |
| [[LoCoMo]] | [arXiv:2402.17753](https://arxiv.org/abs/2402.17753) | [GitHub](https://github.com/snap-research/locomo), [Project page](https://snap-research.github.io/locomo/) |
| [[SimpleToolHalluBench]] | [OpenReview ACL ARR 2026](https://openreview.net/forum?id=xIq7qmyuYF) | [Implementacion anonima indicada por los autores](https://anonymous.4open.science/r/Reasoning_Trap-E5B6/) |
| [[ToolHaystack]] | [arXiv:2505.23662](https://arxiv.org/abs/2505.23662), [ACL Anthology](https://aclanthology.org/2025.findings-emnlp.1344/) | [GitHub indicado por arXiv](https://github.com/bwookwak/toolhaystack) |
| [[Escenarios multi-MCP sinteticos]] | No aplica | Se construyen dentro de la tesis |

## Nota de verificacion

La referencia `arXiv:2501.13395` no corresponde a SimpleToolHalluBench. Si aparece en algun documento de la tesis, debe corregirse antes de cerrar el catalogo bibliografico.

## Uso metodologico

Los datasets sirven para:

- establecer el [[Baseline]];
- comparar tecnicas individuales;
- medir degradacion en conversaciones largas;
- evaluar [[Tool gating]];
- calcular componentes del [[IQCR]];
- contrastar hipotesis.

## Riesgo metodologico

Un dataset puede no representar bien el escenario real multi-MCP. Por eso la tesis combina benchmarks existentes con [[Escenarios multi-MCP sinteticos]] disenados especificamente para el problema investigado.

## Conceptos relacionados

- [[Ground truth]]
- [[IQCR]]
- [[Diseno metodologico]]
- [[Context rot]]
