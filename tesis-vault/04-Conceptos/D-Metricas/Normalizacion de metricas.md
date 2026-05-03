# Normalizacion de metricas

## Definicion

La normalizacion de metricas es el proceso de transformar indicadores con escalas distintas a una escala comun, usualmente `[0, 1]`.

## Por que es necesaria

El [[IQCR]] combina metricas heterogeneas:

- Exactitud en porcentaje.
- Tasa de alucinacion en proporcion.
- Coherencia semantica en puntaje.
- Tokens en valores absolutos.

Sin normalizacion, las metricas con valores numericos grandes podrian dominar el indice aunque no sean conceptualmente mas importantes.

## Regla general

Si una metrica es positiva, es decir, mas alto es mejor:

```text
x_norm = (x - min) / (max - min)
```

Si una metrica es negativa, es decir, mas bajo es mejor:

```text
x_norm = 1 - ((x - min) / (max - min))
```

## Ejemplos

Metricas positivas:

- [[Exactitud de respuesta]]
- [[Coherencia conversacional]]

Metricas negativas:

- [[Tasa de alucinacion]]
- Consumo de tokens
- Latencia

## Decision pendiente

La tesis debe definir si los minimos y maximos salen de:

- limites teoricos;
- valores observados en el experimento;
- valores del baseline;
- umbrales definidos por expertos.

## Conceptos relacionados

- [[IQCR]]
- [[Eficiencia de tokens]]
- [[AHP]]

