# LongMemEval

## Definicion

Benchmark para evaluar memoria a largo plazo en agentes LLM mediante conversaciones extensas y preguntas que requieren recuperar informacion mencionada en turnos anteriores.

## Uso previsto

Fuente de escenarios para evaluar degradacion y memoria conversacional en la tesis.

## Donde encontrarlo

- Paper: [LongMemEval: Benchmarking Chat Assistants on Long-Term Interactive Memory](https://arxiv.org/abs/2410.10813)
- Repositorio oficial: [github.com/xiaowu0162/LongMemEval](https://github.com/xiaowu0162/LongMemEval)
- Dataset actualizado: [xiaowu0162/longmemeval-cleaned en Hugging Face](https://huggingface.co/datasets/xiaowu0162/longmemeval-cleaned)
- Dataset original, marcado como reemplazado: [xiaowu0162/longmemeval en Hugging Face](https://huggingface.co/datasets/xiaowu0162/longmemeval)

## Archivos relevantes

Segun el repositorio oficial, la version actualizada incluye:

- `longmemeval_oracle.json`
- `longmemeval_s_cleaned.json`
- `longmemeval_m_cleaned.json`

La version `cleaned` es preferible porque reemplaza a la version original y elimina sesiones ruidosas que interferian con la correccion de respuestas.

## Que aporta al ground truth

LongMemEval puede aportar [[Ground truth]] en forma de:

- preguntas sobre hechos mencionados previamente;
- respuestas esperadas;
- relaciones temporales entre eventos;
- datos que requieren seguimiento de entidades;
- casos donde el agente debe reconocer ausencia de informacion.

Esto lo vuelve util para medir [[Exactitud de respuesta]] y [[Coherencia conversacional]] en conversaciones largas.

## Capacidades evaluadas

- Recuperacion single-hop.
- Razonamiento multi-hop.
- Seguimiento de entidades.
- Razonamiento temporal.
- Deteccion de ausencia de informacion.

## Relacion con IQCR

Sus respuestas esperadas pueden alimentar los componentes de [[IQCR]] relacionados con exactitud, coherencia y memoria longitudinal.

## Conceptos relacionados

- [[Dataset de evaluacion]]
- [[Ground truth]]
- [[Context rot]]
- [[MemoryBank]]
- [[SessionFacts]]
