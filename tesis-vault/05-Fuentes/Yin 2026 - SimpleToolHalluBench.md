# Yin et al. (2026) — SimpleToolHalluBench: Benchmarking Tool Hallucination in LLM Agents

## Referencia APA

Yin, Z., et al. (2026). SimpleToolHalluBench: Benchmarking tool hallucination in LLM agents via reasoning traps. *OpenReview*. https://openreview.net/forum?id=xIq7qmyuYF

Código: https://anonymous.4open.science/r/Reasoning_Trap-E5B6/

**Nota**: no confundir con arXiv:2501.13395, que corresponde a otro trabajo. La fuente correcta es OpenReview.

## Pregunta que responde

¿En qué condiciones alucinan herramientas los agentes LLM, es decir, llaman a herramientas inexistentes o con parámetros incorrectos? ¿Pueden diseñarse "trampas de razonamiento" para medir este fenómeno sistemáticamente?

## Método

Diseño de un benchmark con escenarios que incluyen "reasoning traps": situaciones que inducen al LLM a llamar herramientas incorrectas o a inventar parámetros. Evaluado en múltiples LLMs de frontera. Métricas: tasa de herramienta correcta, tasa de parámetros correctos, tasa de alucinación total.

## Métricas reportadas

- Los LLMs más capaces tienen tasas de alucinación de herramientas no despreciables, especialmente en escenarios con herramientas similares o parámetros ambiguos.
- Las trampas de razonamiento exponen patrones sistemáticos de error, no solo errores aleatorios.

## Aporte a la tesis

SimpleToolHalluBench es uno de los [[Dataset de evaluacion|datasets de evaluación]] candidatos para medir la dimensión de selección de herramientas en el [[IQCR]]. Proporciona escenarios donde el [[Tool overload]] induce alucinación de herramientas, que es precisamente el fenómeno que el [[Tool gating]] busca mitigar.

## Conceptos relacionados

- [[SimpleToolHalluBench]]
- [[Tasa de alucinacion]]
- [[Tool overload]]
- [[Tool gating]]
- [[Dataset de evaluacion]]
- [[IQCR]]
