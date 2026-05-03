# Model Context Protocol

## Definicion

Estandar abierto para conectar asistentes y agentes de IA con herramientas, recursos y prompts externos mediante una arquitectura cliente-servidor.

## Componentes

- Host: coordina la experiencia del usuario y las sesiones.
- Cliente MCP: mantiene la conexion con un servidor.
- [[Servidor MCP]]: expone tools, resources y prompts.

## Flujo basico

1. Inicializacion.
2. Negociacion de capacidades.
3. Listado de herramientas.
4. Invocacion de herramientas.
5. Notificacion de cambios de catalogo.

## Relevancia para la tesis

El MCP permite conectar muchos servidores al mismo agente, pero tambien aumenta la superficie contextual: mas herramientas, mas resultados y mas estados de sesion.

## Conceptos relacionados

- [[Servidor MCP]]
- [[Tool gating]]
- [[Tool overload]]
- [[Context rot]]

