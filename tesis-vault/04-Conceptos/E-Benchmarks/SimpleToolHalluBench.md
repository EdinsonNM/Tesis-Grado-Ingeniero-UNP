# SimpleToolHalluBench

## Definicion

Benchmark enfocado en alucinaciones durante el uso de herramientas por modelos de lenguaje.

## Donde encontrarlo

- Paper / submission: [The Reasoning Trap: How Enhancing LLM Reasoning Amplifies Tool Hallucination](https://openreview.net/forum?id=xIq7qmyuYF)
- Version previa retirada en ICLR OpenReview: [OpenReview vHKUXkrpVs](https://openreview.net/forum?id=vHKUXkrpVs)
- Implementacion indicada por los autores: [anonymous.4open.science/r/Reasoning_Trap-E5B6](https://anonymous.4open.science/r/Reasoning_Trap-E5B6/)

## Advertencia bibliografica

En algunos documentos de la tesis aparece `arXiv:2501.13395` asociado a SimpleToolHalluBench. Esa referencia no corresponde a este benchmark; actualmente apunta a un paper de quantum machine learning aplicado a QSAR. Conviene corregir esa cita en el catalogo de fuentes.

## Dimensiones evaluadas

- Alucinacion de nombre de herramienta.
- Alucinacion de parametros.
- Valores invalidos o fuera de rango.

## Que aporta al ground truth

SimpleToolHalluBench puede aportar [[Ground truth]] en forma de:

- herramientas disponibles en el catalogo;
- herramientas que no existen y no deben ser invocadas;
- parametros validos para cada herramienta;
- valores esperados o rangos aceptables;
- casos donde el agente debe abstenerse de usar una herramienta.

Esto permite medir si el agente usa herramientas reales y evita inventar tools o argumentos.

## Uso en la tesis

Sirve para evaluar el impacto de [[Tool overload]] y [[Tool gating]] en catalogos de herramientas grandes.

## Relacion con IQCR

Aunque el [[IQCR]] se centra en calidad de respuesta, los errores de tool use pueden alimentar la [[Tasa de alucinacion]] y la exactitud global del agente.

## Conceptos relacionados

- [[Dataset de evaluacion]]
- [[Ground truth]]
- [[Tool overload]]
- [[Tool gating]]
- [[Tasa de alucinacion]]
