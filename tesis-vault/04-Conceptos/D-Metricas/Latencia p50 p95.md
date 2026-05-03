# Latencia p50 / p95

## Definición

Percentiles de la distribución de tiempos de respuesta de un [[Agente LLM]]. En lugar de un promedio, describen puntos específicos de la cola de latencias ordenadas de menor a mayor.

## Cómo leerlos

Imagina 100 solicitudes al agente, con sus tiempos medidos y ordenados:

```
[120ms, 145ms, 180ms, ... , 620ms, 890ms, 1.2s, 3.8s]
                               ↑                  ↑
                              p50                p95
```

- **p50** (mediana) — el turno número 50 de la cola. La mitad de las solicitudes tardó menos que esto, la otra mitad tardó más. Representa la **experiencia típica** del usuario. Es más honesto que el promedio porque los outliers no lo distorsionan.

- **p95** — el turno número 95. Solo el 5% más lento queda por encima. Representa la **peor experiencia frecuente**: lo que le ocurre a un usuario real de vez en cuando, no un caso extremo aislado.

## Por qué importan los dos juntos

Mirar solo p50 puede ocultar degradación en los casos difíciles. Mirar solo p95 puede alarmar sin contexto. Juntos cuentan la historia completa:

| Escenario | p50 | p95 | Interpretación |
|---|---|---|---|
| Técnica ayuda en casos pesados | igual | baja | Corta picos cuando el contexto está muy inflado |
| Técnica mejora todo | baja | baja | Mejora generalizada |
| Técnica introduce overhead fijo | sube levemente | sube poco | Costo constante, sin picos adicionales |
| Sin técnica, contexto creciendo | estable | sube | El context rot empieza a golpear los turnos largos primero |

El tercer escenario es clave para evaluar [[Tool gating]]: el filtrado semántico agrega un paso extra (el retrieval), lo que puede subir levemente el p50, pero debería reducir el p95 porque evita que el modelo procese contextos enormes con cientos de herramientas.

## Relación con el context rot

El [[Context rot]] impacta primero el p95, no el p50. Las primeras solicitudes de una sesión todavía tienen contexto liviano, pero conforme el [[Contexto activo]] crece, los turnos tardíos se vuelven progresivamente más lentos. El p95 sube antes de que el p50 se mueva — es una señal temprana de degradación.

## Relación con TTFT

El [[TTFT]] mide cuánto tarda en aparecer el **primer token** (latencia percibida en interfaces de streaming). La latencia p50/p95 mide el tiempo hasta la **respuesta completa**. En sesiones con herramientas, la diferencia entre ambos incluye el tiempo de ejecución de las llamadas a tools.

## En la tesis

Son métricas de evaluación secundarias del experimento, reportadas junto al [[IQCR]]. Se espera una correlación positiva entre tamaño del [[Contexto activo]] y p95 que las técnicas de mitigación deberían romper — especialmente [[Tool gating]], [[Compaction]] y [[Caching semantico]].

## Referencias

- [[TTFT]]
- [[IQCR]]
- [[Context rot]]
- [[Contexto activo]]
- [[Eficiencia de tokens]]
