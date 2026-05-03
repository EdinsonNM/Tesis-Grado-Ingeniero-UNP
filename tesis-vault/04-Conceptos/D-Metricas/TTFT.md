# TTFT — Time to First Token

## Definición

Tiempo transcurrido entre el momento en que se envía una solicitud al [[Modelo de lenguaje de gran escala|LLM]] y el momento en que el modelo emite el primer token de respuesta. Se mide en milisegundos.

## Por qué importa

En interfaces de streaming, el TTFT determina cuánto tiempo espera el usuario antes de ver cualquier texto. Es la métrica más directa de latencia percibida. Un TTFT alto hace que la interfaz parezca "congelada".

## Factores que afectan el TTFT

1. **Tamaño del contexto activo**: el modelo debe procesar todos los tokens de entrada antes de generar el primero de salida. Más contexto = mayor TTFT.
2. **Carga del servidor**: cola de solicitudes en la infraestructura del proveedor.
3. **Tipo de operación**: si hay llamadas a herramientas previas al prefill, el TTFT incluye ese tiempo también.

## Relación con el context rot

El [[Context rot]] aumenta el TTFT porque el [[Contexto activo]] crece con cada turno. Las técnicas de mitigación que reducen el contexto activo (como [[Compaction]] o [[Tool gating]]) tienen efecto directo sobre el TTFT.

## En la tesis

Se mide como métrica de latencia junto con [[Latencia p50 p95]]. Se espera una correlación positiva entre tamaño del contexto activo y TTFT que las técnicas de mitigación deberían romper.

## Referencias

- [[Latencia p50 p95]]
- [[Contexto activo]]
- [[Context rot]]
- [[Agente LLM]]
