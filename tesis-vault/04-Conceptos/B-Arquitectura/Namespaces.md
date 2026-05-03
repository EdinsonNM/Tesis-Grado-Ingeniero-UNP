# Namespaces

## Definición

Mecanismo de particionamiento lógico que agrupa herramientas de distintos [[Servidor MCP|servidores MCP]] bajo identificadores de espacio de nombres separados, evitando colisiones de nombres y permitiendo que el [[Agente LLM]] distinga el origen de cada herramienta.

## Problema que resuelve

En una arquitectura multi-MCP, distintos servidores pueden exponer herramientas con el mismo nombre genérico (ej. `search`, `get_data`, `create_item`). Sin namespaces, el agente no puede distinguir entre `calendar.search` y `email.search`. La ambigüedad contribuye al [[Tool overload]] y aumenta la tasa de selección incorrecta de herramientas.

## Convención de nombres

El formato típico es `servidor.herramienta` o `servidor/herramienta`. Por ejemplo:
- `github.create_issue`
- `calendar.list_events`
- `docs.search_files`

## En la tesis

Los namespaces son parte de la arquitectura experimental. Cada servidor MCP en los [[Escenarios multi-MCP sinteticos]] opera bajo su propio namespace. El [[Tool gating]] opera sobre el espacio con namespaces para filtrar herramientas relevantes sin que el agente confunda herramientas homónimas de distintos servidores.

## Relación con sharding

Los namespaces organizan herramientas lógicamente; el [[Sharding]] las particiona físicamente para escalar la recuperación. Son complementarios.

## Referencias

- [[Servidor MCP]]
- [[Tool gating]]
- [[Tool overload]]
- [[Sharding]]
- [[Model Context Protocol]]
