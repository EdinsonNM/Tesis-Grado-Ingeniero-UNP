# Baseline

## Definicion

Condicion experimental de referencia contra la cual se comparan las tecnicas de memoria y gestion de contexto.

## En la tesis

El baseline es un [[Agente LLM]] conectado a multiples [[Servidor MCP|servidores MCP]] sin aplicar tecnicas de mitigacion como [[Tool gating]], [[SessionFacts]], [[MemoryBank]] o [[Caching semantico]].

## Funcion

Permite medir la degradacion natural del sistema y calcular la mejora atribuible a cada tecnica.

## Ejemplo de comparacion

```text
mejora_IQCR = (IQCR_tecnica - IQCR_baseline) / IQCR_baseline
```

## Conceptos relacionados

- [[IQCR]]
- [[Context rot]]
- [[Diseno metodologico]]

