# Ventana de contexto

## Definición

Límite máximo de tokens que un [[Modelo de lenguaje de gran escala|LLM]] puede procesar en una sola llamada de inferencia. Todo lo que el modelo "ve" en un momento dado debe caber dentro de esta ventana: instrucciones del sistema, historial de conversación, resultados de herramientas y la respuesta generada.

## Tamaños típicos

Los modelos modernos tienen ventanas que van de 8 K tokens (modelos pequeños) hasta 200 K o más (Claude, Gemini). A mayor ventana, mayor costo por token procesado y mayor latencia.

## Relación con el context rot

La ventana de contexto define el límite físico donde opera el [[Context rot]]. El problema no es solo alcanzar el límite, sino que el modelo degrada su rendimiento mucho antes de llenarlo: la atención se distribuye de forma no uniforme y el efecto [[Lost in the middle]] empieza a aparecer a partir del 30–50% de ocupación en conversaciones largas.

## Distinción con contexto activo

La ventana de contexto es el contenedor; el [[Contexto activo]] es lo que hay dentro en un momento dado. Las técnicas de mitigación buscan reducir el contexto activo para mantenerlo muy por debajo del límite de la ventana.

## En la tesis

La ventana de contexto es la variable de capacidad que delimita el problema. El experimento no la modifica (se fija un modelo con ventana determinada), pero el contexto activo crece a medida que avanza la conversación multi-MCP.

## Referencias

- [[Modelo de lenguaje de gran escala]]
- [[Contexto activo]]
- [[Context rot]]
- [[Lost in the middle]]
