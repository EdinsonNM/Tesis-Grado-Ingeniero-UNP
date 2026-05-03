# PELT — Pruned Exact Linear Time

## Definición

Algoritmo de detección de puntos de cambio (*changepoint detection*) en series temporales que opera en tiempo O(n) mediante poda dinámica de búsqueda. Dado una serie de observaciones, identifica los puntos donde la distribución estadística de la serie cambia de forma significativa.

## Fuente

Killick, R., Fearnhead, P., & Eckley, I. A. (2012). Optimal detection of changepoints with a linear computational cost. *Journal of the American Statistical Association*, 107(500), 1590–1598.

Implementación en R: paquete `changepoint`. En Python: paquete `ruptures`.

## Cómo funciona

Minimiza una función de costo penalizada:

`∑ C(y_{t_i+1:t_{i+1}}) + β * m`

Donde C es la función de costo (ej. suma de cuadrados residuales), β es la penalización por añadir un punto de cambio y m es el número de puntos. La poda elimina candidatos que no pueden ser óptimos, logrando complejidad lineal.

## En la tesis

Se aplica sobre las series de métricas de calidad ([[IQCR]], [[Exactitud de respuesta]], [[Tasa de alucinacion]]) en función del [[Contexto activo]] creciente. El objetivo es detectar **umbrales estadísticos**: en qué punto (medido en tokens de contexto activo) la degradación se vuelve estadísticamente detectable. Responde la pregunta: "¿en qué punto aparecen umbrales estadísticamente detectables?"

## Relación con TOST

[[TOST]] determina si dos condiciones son prácticamente equivalentes. PELT determina cuándo una serie deja de ser estacionaria. Son complementarios: PELT detecta el umbral, TOST confirma si la magnitud de cambio es prácticamente relevante.

## Referencias

- [[Diseno factorial 2k]]
- [[TOST]]
- [[Contexto activo]]
- [[IQCR]]
- [[Diseno metodologico]]
