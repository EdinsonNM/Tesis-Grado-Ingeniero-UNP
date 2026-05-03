# Eficiencia de tokens

## Definicion

La eficiencia de tokens mide cuanta calidad obtiene el agente en relacion con la cantidad de tokens consumidos durante una respuesta o turno experimental.

## Funcion dentro del IQCR

En el [[IQCR]], la eficiencia de tokens evita que una configuracion reciba un puntaje alto solo por mejorar calidad a costa de inflar demasiado el contexto.

## Por que importa

En agentes multi-MCP, el consumo de tokens crece por:

- Descripciones de herramientas.
- Historial conversacional.
- Resultados intermedios.
- Metadatos de servidores.
- Resumenes o memorias inyectadas.

Si una tecnica reduce [[Context rot]] pero duplica el costo, puede no ser la mejor opcion en produccion.

## Transformacion a escala 0-1

Como menos tokens es mejor, se necesita una funcion inversa. Una opcion simple:

```text
eficiencia_tokens = 1 - ((tokens_turno - tokens_min) / (tokens_max - tokens_min))
```

Otra opcion mas estable es comparar contra el baseline:

```text
eficiencia_tokens = tokens_baseline / tokens_tecnica
```

Luego se recorta o normaliza al rango `[0, 1]`.

## Precaucion

La eficiencia no debe premiar respuestas demasiado cortas si pierden exactitud. Por eso se usa como un componente del [[IQCR]], no como criterio unico.

## Conceptos relacionados

- [[IQCR]]
- [[Normalizacion de metricas]]
- [[Tool gating]]
- [[Caching semantico]]

