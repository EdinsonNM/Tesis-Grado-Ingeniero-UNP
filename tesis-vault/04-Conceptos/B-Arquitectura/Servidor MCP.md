# Servidor MCP

## Definicion

Componente del [[Model Context Protocol]] que expone herramientas, recursos y prompts mediante una interfaz estandarizada para que un agente pueda descubrirlos e invocarlos.

## En la tesis

El numero de servidores MCP activos funciona como variable moderadora. La investigacion evalua escenarios con multiples servidores para observar como cambia el [[Context rot]] cuando crece la escala de herramientas y recursos disponibles.

## Riesgos en multiples servidores

- Catalogos de herramientas demasiado grandes.
- Estados de sesion heterogeneos.
- Resultados intermedios extensos.
- Ambiguedad sobre que servidor produjo que informacion.

## Tecnicas de mitigacion

- [[Tool gating]]
- [[Recuperacion federada]]
- Namespaces por servidor.
- Resumen de resultados mediante [[SessionFacts]].

