# Agente LLM

## Definicion

Sistema de software que usa un modelo de lenguaje como motor de razonamiento y lo conecta con herramientas externas para ejecutar acciones, consultar datos o interactuar con APIs.

## Ciclo operativo

1. Recibe una tarea.
2. Razona sobre el estado actual.
3. Selecciona una herramienta cuando la necesita.
4. Observa el resultado.
5. Actualiza su contexto.
6. Responde o continua actuando.

## Relacion con ReAct

El patron ReAct organiza el ciclo razonamiento-accion-observacion. En conversaciones largas, cada observacion puede aumentar el contexto activo y contribuir al [[Context rot]].

## En la tesis

La unidad experimental es un agente LLM conectado a multiples [[Servidor MCP|servidores MCP]], evaluado bajo distintas tecnicas de memoria y gestion de contexto.

