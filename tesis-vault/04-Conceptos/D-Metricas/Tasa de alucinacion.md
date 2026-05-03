# Tasa de alucinacion

## Definicion

La tasa de alucinacion mide la proporcion de afirmaciones generadas por un [[Agente LLM]] que son incorrectas, no verificables o no estan sustentadas en el contexto disponible.

## Funcion dentro del IQCR

En el [[IQCR]], la alucinacion se usa como componente invertido:

```text
no_alucinacion = 1 - tasa_de_alucinacion
```

Esto significa que una menor tasa de alucinacion aumenta el puntaje final del indice.

## Tipos relevantes

- Alucinacion factual: informacion incorrecta.
- Alucinacion de herramienta: invocar una tool inexistente.
- Alucinacion de parametros: usar parametros invalidos.
- Alucinacion por atribucion: asociar un dato al servidor o fuente incorrecta.

## Como se mide

Puede medirse mediante:

- Verificacion contra [[Ground truth]].
- Comparacion con outputs esperados de herramientas.
- Evaluacion automatizada con un verificador.
- Revision manual de una muestra para calibrar el verificador.

## Relacion con context rot

Si el contexto crece con informacion irrelevante o contradictoria, la tasa de alucinacion tiende a aumentar. Por eso es un indicador directo del [[Context rot]].

## Conceptos relacionados

- [[IQCR]]
- [[Tool overload]]
- [[SimpleToolHalluBench]]
- [[Ground truth]]

