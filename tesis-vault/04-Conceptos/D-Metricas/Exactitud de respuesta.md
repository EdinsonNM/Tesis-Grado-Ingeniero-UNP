# Exactitud de respuesta

## Definicion

La exactitud de respuesta mide que proporcion de la respuesta generada por un [[Agente LLM]] coincide con una respuesta esperada, evidencia verificable o [[Ground truth]].

## Funcion dentro del IQCR

Es uno de los componentes mas importantes del [[IQCR]] porque captura si el agente responde correctamente. Una tecnica de memoria solo es util si mantiene o mejora la exactitud.

## Como se mide

Puede medirse de varias formas, segun el tipo de tarea:

- Coincidencia exacta cuando la respuesta esperada es cerrada.
- Coincidencia parcial cuando existen varias formulaciones correctas.
- Evaluacion semantica cuando la respuesta admite redaccion flexible.
- Verificacion contra ground truth anotado.

## Escala

Debe expresarse en el rango `[0, 1]`.

```text
exactitud = respuestas_correctas / total_de_respuestas
```

En evaluacion por turno, cada respuesta puede recibir un puntaje continuo entre 0 y 1.

## Riesgo metodologico

Una respuesta puede ser parcialmente correcta pero incompleta. Por eso conviene definir rubricas por tipo de pregunta y no depender solo de coincidencia textual exacta.

## Relacion con otros conceptos

- [[IQCR]]
- [[Ground truth]]
- [[Context rot]]
- [[Tasa de alucinacion]]

