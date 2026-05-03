# TOST — Two One-Sided Tests

## Definición

Procedimiento estadístico para demostrar **equivalencia práctica** entre dos condiciones. En lugar de buscar diferencia significativa (hipótesis nula: igual; alternativa: diferente), TOST invierte la lógica: la hipótesis nula es que hay diferencia relevante, y se rechaza si ambos extremos del intervalo de confianza caen dentro del margen de equivalencia predefinido (Δ).

## Por qué TOST y no solo t-test

El t-test clásico no puede "demostrar" que dos condiciones son equivalentes: solo puede fallar en rechazar la igualdad, lo que es distinto a afirmar equivalencia. TOST es el método correcto cuando se quiere sostener que una técnica nueva no degrada significativamente respecto al baseline.

## Mecanismo

Se define un margen de equivalencia Δ (ej. ±5% de diferencia en [[IQCR]] es aceptable). Se lanzan dos pruebas t de una cola:
1. H0: diferencia ≥ +Δ (la nueva condición es peor por más de Δ)
2. H0: diferencia ≤ −Δ (la nueva condición es mejor por más de Δ, lo que también indicaría no equivalencia)

Si ambas H0 se rechazan a nivel α, se concluye equivalencia práctica.

## En la tesis

Se usa para demostrar que las técnicas de mitigación del [[Context rot]] no introducen degradación inaceptable en alguna métrica secundaria mientras mejoran la principal. Por ejemplo: [[Caching semantico]] reduce tokens pero ¿degrada la [[Exactitud de respuesta]] más allá del margen aceptable?

## Referencias

- [[Diseno factorial 2k]]
- [[PELT]]
- [[IQCR]]
- [[Baseline]]
- [[Variable dependiente]]
