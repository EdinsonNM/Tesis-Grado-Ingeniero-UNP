# Diseño factorial 2k

## Definición

Diseño experimental en el que se estudian k factores, cada uno con exactamente 2 niveles (bajo/alto, presente/ausente, configuración A/configuración B). El número total de combinaciones de tratamiento es 2^k. Permite estimar efectos principales e interacciones con eficiencia estadística.

## Ventajas

- Detecta no solo el efecto de cada factor individualmente, sino también si los factores interactúan entre sí.
- Eficiente: requiere menos corridas que diseños con más niveles.
- Análisis por regresión múltiple o ANOVA factorial.

## Notación

Las condiciones se codifican como ±1 (bajo = −1, alto = +1). Un diseño 2^3 con factores A, B, C produce 8 condiciones: (−−−), (+−−), (−+−), (++−), (−−+), (+−+), (−++), (+++).

## En la tesis

Se aplica para comparar técnicas de mitigación del [[Context rot]]. Por ejemplo, k=3 factores: [[Tool gating]] (sí/no), [[SessionFacts]] (sí/no), [[Caching semantico]] (sí/no). Esto genera 8 combinaciones de tratamiento para comparar contra el [[Baseline]]. Permite detectar si combinar dos técnicas produce mejoras mayores que cada una por separado (interacciones).

## Relación con PELT

El [[PELT]] se aplica sobre las series de métricas generadas por cada condición del diseño factorial para detectar en qué punto del crecimiento del contexto activo aparecen umbrales de degradación.

## Referencias

- [[TOST]]
- [[PELT]]
- [[Baseline]]
- [[Diseno metodologico]]
- [[Variable dependiente]]
