# ToolHaystack

## Definicion

Benchmark orientado a evaluar si un modelo puede encontrar y utilizar la herramienta correcta dentro de catalogos grandes de herramientas.

## Donde encontrarlo

- Paper: [arXiv:2505.23662](https://arxiv.org/abs/2505.23662)
- Version publicada: [ACL Anthology - Findings of EMNLP 2025](https://aclanthology.org/2025.findings-emnlp.1344/)
- Repositorio indicado por arXiv: [github.com/bwookwak/toolhaystack](https://github.com/bwookwak/toolhaystack)

## Nota de acceso

El paper en arXiv indica que el codigo y los datos estan disponibles en GitHub. Si el repositorio no carga en algun momento, usar como respaldo la pagina de arXiv o ACL Anthology para confirmar el enlace oficial.

## Relacion con la tesis

Es relevante para escenarios donde el agente esta conectado a multiples [[Servidor MCP|servidores MCP]] y enfrenta un catalogo amplio y ruidoso.

## Que aporta al ground truth

ToolHaystack puede aportar [[Ground truth]] sobre:

- cual es la herramienta correcta para una consulta;
- cuales herramientas son distractoras;
- cuando una herramienta parece relevante pero no debe usarse;
- como cambia la seleccion correcta a medida que crece el catalogo.

Este tipo de ground truth es clave para evaluar [[Tool gating]] y [[RAG-MCP]].

## Conceptos conectados

- [[Tool overload]]
- [[Tool gating]]
- [[RAG-MCP]]
- [[Dataset de evaluacion]]
- [[Ground truth]]
