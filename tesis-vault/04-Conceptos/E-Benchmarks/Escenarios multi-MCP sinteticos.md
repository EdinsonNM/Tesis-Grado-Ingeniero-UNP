# Escenarios multi-MCP sinteticos

## Definicion

Casos de evaluacion creados especificamente para la tesis con el objetivo de simular agentes LLM conectados a multiples [[Servidor MCP|servidores MCP]].

## Por que son necesarios

Los benchmarks existentes cubren partes del problema, como memoria larga o alucinacion de herramientas, pero no necesariamente reproducen una arquitectura multi-MCP completa.

Los escenarios sinteticos permiten controlar:

- numero de servidores MCP activos;
- tamano del catalogo de herramientas;
- presencia de herramientas distractoras;
- respuestas esperadas;
- servidor correcto para cada consulta;
- parametros correctos de tool calls;
- longitud de conversacion;
- acumulacion de resultados intermedios.

## Que aportan al ground truth

Estos escenarios permiten construir [[Ground truth]] de forma controlada:

| Elemento del escenario | Ground truth definido |
|---|---|
| Consulta del usuario | Respuesta esperada |
| Servidores disponibles | Servidor relevante |
| Catalogo de tools | Herramienta correcta |
| Esquema de parametros | Parametros validos |
| Datos consultables | Hechos verificables |
| Conversacion previa | Memoria que debe recuperarse |

## Ejemplo

```text
Escenario:
- Servidores: calendario, notas, base de datos
- Pregunta: "Que reunion tengo despues de la demo de Neo?"
- Servidor correcto: calendario
- Tool correcta: find_events
- Ground truth: "Reunion de seguimiento, 16:00"
```

Si el agente consulta notas en vez de calendario, o inventa una reunion, se registra error de seleccion o alucinacion.

## Relacion con la tesis

Son utiles para probar [[Tool gating]], [[Recuperacion federada]], [[SessionFacts]] y deteccion de umbrales de [[Context rot]] bajo condiciones controladas.

## Conceptos relacionados

- [[Dataset de evaluacion]]
- [[Ground truth]]
- [[Tool overload]]
- [[Tool gating]]
- [[IQCR]]
