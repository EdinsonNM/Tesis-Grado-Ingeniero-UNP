# Recuperacion federada

## Definicion

Estrategia de recuperacion donde cada servidor, dominio o indice busca sus propios candidatos relevantes y un componente central fusiona y rerankea los resultados.

## Por que importa en multi-MCP

Permite mantener separadas las fuentes de informacion por [[Servidor MCP]], reduciendo mezcla de estados y ruido entre dominios.

## Flujo

1. El router identifica servidores relevantes.
2. Cada servidor recupera sus top-k resultados.
3. Un reranker global fusiona resultados.
4. Solo se inyecta al contexto la informacion seleccionada.

## Relacion con la tesis

Es una tecnica de mitigacion orientada a arquitecturas multi-servidor, especialmente util cuando los datos estan distribuidos en silos.

