# Coherencia conversacional

## Definicion

La coherencia conversacional mide si las respuestas de un [[Agente LLM]] mantienen continuidad, consistencia y ausencia de contradicciones a lo largo de una conversacion.

## Funcion dentro del IQCR

Dentro del [[IQCR]], la coherencia permite capturar degradaciones que no siempre aparecen como errores factuales directos. Un agente puede responder datos correctos, pero perder continuidad respecto a preferencias, restricciones o decisiones previas.

## Dimensiones

- Consistencia factual entre turnos.
- Continuidad del objetivo de la conversacion.
- Respeto de restricciones previas.
- Seguimiento de entidades.
- Actualizacion correcta de informacion nueva.

## Como se mide

Puede medirse con:

- [[BERTScore]] u otra metrica semantica entre respuesta y referencia.
- Deteccion de contradicciones entre turnos.
- Preguntas de memoria conversacional.
- Benchmarks como [[LoCoMo]] y [[LongMemEval]].

## Riesgo metodologico

La similitud semantica no siempre equivale a coherencia. Dos respuestas pueden ser semanticamente cercanas y aun asi contradecir un detalle importante. Por eso conviene combinar metricas automaticas con rubricas.

## Conceptos relacionados

- [[IQCR]]
- [[MemoryBank]]
- [[SessionFacts]]
- [[LoCoMo]]

