# LoCoMo

## Definicion

Benchmark de conversaciones largas y multi-sesion orientado a evaluar coherencia, consistencia y actualizacion de creencias en agentes LLM.

## Uso previsto

Medir coherencia conversacional y efectos de memoria longitudinal en la tesis.

## Donde encontrarlo

- Paper: [Evaluating Very Long-Term Conversational Memory of LLM Agents](https://arxiv.org/abs/2402.17753)
- Repositorio oficial: [github.com/snap-research/locomo](https://github.com/snap-research/locomo)
- Pagina del proyecto: [snap-research.github.io/locomo](https://snap-research.github.io/locomo/)

## Archivo relevante

El repositorio oficial indica que el dataset esta en:

- `data/locomo10.json`

Cada muestra contiene una conversacion con sesiones, timestamps, dialogos, anotaciones de QA y resumenes/eventos.

## Que aporta al ground truth

LoCoMo puede aportar [[Ground truth]] sobre:

- hechos mencionados en sesiones anteriores;
- preferencias o datos personales persistentes dentro de una conversacion;
- contradicciones que el agente debe evitar;
- cambios de informacion que el agente debe actualizar;
- preguntas que requieren memoria multi-sesion.

Su valor principal no esta solo en una respuesta exacta, sino en evaluar si el agente conserva continuidad.

## Relacion con IQCR

LoCoMo es especialmente relevante para el componente de [[Coherencia conversacional]] del [[IQCR]].

## Relacion con conceptos

- [[Context rot]]
- [[MemoryBank]]
- [[IQCR]]
- [[Dataset de evaluacion]]
- [[Ground truth]]
