# Variables e indicadores

## Variable independiente

Tipo y combinacion de tecnicas de memoria y gestion de contexto:

- Baseline sin tecnica.
- [[RAG]]
- [[SessionFacts]]
- [[MemoryBank]]
- [[Caching semantico]]
- [[Tool gating]]
- Combinacion optima.

## Variable dependiente

Nivel de degradacion de respuestas, operacionalizado mediante el [[IQCR]].

## Indicadores primarios

- [[Exactitud de respuesta]].
- [[Tasa de alucinacion]].
- [[Coherencia conversacional]].
- [[Eficiencia de tokens|Consumo de tokens por turno]].
- Latencia p50/p95.

## Variables moderadoras

- Longitud de conversacion.
- Tokens acumulados.
- Numero de [[Servidor MCP|servidores MCP]] activos.
- Tamano del catalogo de herramientas.

## Variables de control

- Modelo LLM base.
- Temperatura.
- Dataset de evaluacion.
- Infraestructura experimental.
- Configuracion de servidores MCP.
