# Tool overload

## Definicion

Mecanismo de [[Context rot]] que ocurre cuando el numero de herramientas expuestas al modelo supera su capacidad efectiva de seleccion y atencion.

## Sintomas

- Seleccion de herramienta incorrecta.
- Invocacion de herramientas inexistentes.
- Parametros invalidos.
- Mayor consumo de tokens.
- Mayor latencia antes de responder.

## Causa principal

En arquitecturas multi-MCP, cada [[Servidor MCP]] aporta su propio catalogo. Si todos los catalogos se exponen al modelo al mismo tiempo, la relacion senal-ruido empeora.

## Evidencia empirica

| Fuente | Escenario | Hallazgo |
|---|---|---|
| Patil et al. (2023) | GPT-4 con herramientas de código | Umbral de degradación ~20 herramientas; más allá, la tasa de selección correcta cae abruptamente |
| Tang et al. (2025) | RAG-MCP con 128 herramientas | +23% alucinación en parámetros al pasar de 10 a 50 herramientas expuestas |
| **Vercel (2025)** | Agente d0 en producción (CI/CD) | Reducción estática de 17-18 herramientas → ops mínimas de filesystem: éxito 80%→100%, −37% tokens, 3.5× más rápido, −42% pasos |

> **Nota sobre Vercel**: el caso d0 demuestra el impacto del tool overload en producción real mediante reducción *estática* (eliminación permanente de herramientas irrelevantes). La tesis propone una solución complementaria y más general: filtrado *dinámico* vía [[RAG-MCP]], adaptable al contexto de cada consulta sin requerir eliminación permanente.

## Mitigacion

- [[Tool gating]]
- [[RAG-MCP]]
- Carga diferida.
- Filtrado semantico top-k.

