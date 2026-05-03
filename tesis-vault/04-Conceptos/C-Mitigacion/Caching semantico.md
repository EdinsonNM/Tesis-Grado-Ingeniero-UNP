# Caching semantico

## Definicion

Tecnica que almacena consultas y respuestas previas para reutilizarlas cuando una nueva consulta es semanticamente equivalente, usando embeddings y similitud coseno.

## Objetivo

Reducir llamadas repetidas al modelo y a herramientas, disminuyendo costo de tokens y latencia.

## En la tesis

Se evalua como tecnica individual de mitigacion. No elimina el [[Context rot]] directamente, pero puede reducir la cantidad de inferencias y observaciones acumuladas.

## Indicadores

- Tasa de acierto de cache.
- Reduccion de tokens.
- Reduccion de latencia.
- Riesgo de respuestas obsoletas.

