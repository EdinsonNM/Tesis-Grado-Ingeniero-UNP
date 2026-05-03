# Contexto activo

## Definición

Porción de la [[Ventana de contexto]] que está efectivamente ocupada en un momento dado durante la ejecución de un [[Agente LLM]]. Incluye: el prompt del sistema, el historial de turnos, los esquemas de herramientas MCP disponibles, los resultados de llamadas a herramientas anteriores y cualquier otro contenido inyectado.

## Componentes en un agente multi-MCP

1. **Prompt del sistema** — instrucciones fijas del agente.
2. **Esquemas de herramientas** — descripciones JSON de todas las herramientas expuestas por los [[Servidor MCP|servidores MCP]] conectados.
3. **Historial de conversación** — todos los turnos usuario-asistente previos.
4. **Resultados de herramientas** — las respuestas de cada llamada a herramienta, que se acumulan turno a turno.
5. **Contexto de sesión** — variables de estado mantenidas entre turnos.

## Crecimiento del contexto activo

En una sesión multi-MCP, el contexto activo crece de forma acumulativa: cada herramienta invocada agrega su resultado, cada turno agrega su intercambio. Este crecimiento sin control es el mecanismo principal del [[Context rot]].

## En la tesis

El contexto activo es la variable de presión experimental. Se mide en tokens y se incrementa sistemáticamente para observar cuándo aparecen umbrales de degradación estadísticamente detectables ([[PELT]]). Las técnicas de mitigación buscan mantener el contexto activo bajo control sin perder información relevante.

## Referencias

- [[Ventana de contexto]]
- [[Context rot]]
- [[Tool overload]]
- [[Agente LLM]]
- [[PELT]]
