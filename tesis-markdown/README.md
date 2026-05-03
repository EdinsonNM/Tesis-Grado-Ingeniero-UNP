# Anteproyecto de Tesis — Versión Markdown

**Medición del impacto de técnicas de memoria y gestión de contexto sobre la degradación de respuestas en agentes LLM conectados a múltiples servidores MCP**

**Investigador:** Edinson Núñez  
**Área:** Inteligencia Artificial Generativa · Modelos de Lenguaje de Gran Escala (LLM) · Model Context Protocol (MCP)  
**Estado:** Anteproyecto en desarrollo

---

## ¿Qué es esta carpeta?

Conversión fiel de los documentos Word del directorio `investigación/` a formato Markdown. El objetivo es facilitar la lectura directa desde GitHub sin necesidad de descargar archivos `.docx`.

> **Nota:** Los archivos fuente `.docx` en `investigación/` son los documentos oficiales del proyecto. Esta carpeta es una vista de solo lectura para navegación en GitHub.

---

## Índice de documentos

### Organizacional

| Doc | Título | Descripción |
|-----|--------|-------------|
| [DOC-01](DOC-01_Indice_Documentos.md) | Índice de Documentos Generados | Mapa de navegación del proyecto con todos los entregables, tipos y estado de avance. |

---

### Bibliográfico y Analítico

| Doc | Título | Descripción |
|-----|--------|-------------|
| [DOC-02](DOC-02_Catalogo_Fuentes.md) | Catálogo de Fuentes | Fichas de papers, datasets y documentación técnica clasificados por categoría. |
| [DOC-04](DOC-04_Indicadores_por_Paper.md) | Indicadores y Métricas por Paper | Tabla comparativa de métricas usadas en cada referencia bibliográfica. |

---

### Capítulo I — Planteamiento del Problema

> Secciones 1.1 a 1.6 del primer capítulo de la tesis.

| Doc | Sección | Título | Descripción |
|-----|---------|--------|-------------|
| [DOC-05](DOC-05_Introduccion_Tesis.md) | 1.0 | Introducción | Contexto general, motivación, alcance y estructura del documento. |
| [DOC-06](DOC-06_Realidad_Problematica.md) | 1.1 | Realidad Problemática | Expansión global de IA generativa, surgimiento de MCP y context rot como problema no resuelto. |
| [DOC-07](DOC-07_Formulacion_Problema.md) | 1.2 | Formulación del Problema | Problema general y problemas específicos de la investigación. |
| [DOC-08](DOC-08_Justificacion_Importancia.md) | 1.3 | Justificación e Importancia | Argumentación teórica, práctica y metodológica. |
| [DOC-09](DOC-09_Objetivos.md) | 1.4 | Objetivos | Objetivo general y tres objetivos específicos. |
| [DOC-10](DOC-10_Delimitacion.md) | 1.5 | Delimitación | Límites espaciales, temporales, temáticos y teóricos. |
| [DOC-13](DOC-13_Hipotesis.md) | 1.6 | Hipótesis | Hipótesis general (HG) y específicas (HE1–HE3) con variables e indicadores. |

---

### Capítulo II — Marco Teórico

| Doc | Sección | Título | Descripción |
|-----|---------|--------|-------------|
| [DOC-11](DOC-11_Bases_Teoricas.md) | 2.1–2.8 | Bases Teóricas | LLMs y transformers, agentes LLM, MCP, context rot, técnicas de memoria, tool gating, benchmarks y harness engineering. |
| [DOC-12](DOC-12_Glosario.md) | 2.2 | Glosario de Términos | Definiciones formales de todos los términos técnicos del dominio. |

---

### Capítulo III — Marco Metodológico

| Doc | Sección | Título | Descripción |
|-----|---------|--------|-------------|
| [DOC-14](DOC-14_Marco_Metodologico.md) | 3.x | Marco Metodológico | Diseño experimental: tipo de estudio, variables, protocolo, diseño factorial 2^k e instrumentos. |

---

### Documentos Metodológicos de Soporte

| Doc | Título | Descripción |
|-----|--------|-------------|
| [DOC-15](DOC-15_Aspectos_Administrativos.md) | Aspectos Administrativos | Cronograma, recursos humanos y presupuesto del proyecto. |
| [DOC-16](DOC-16_Matriz_Consistencia.md) | Matriz de Consistencia | Relación sistemática entre problema, objetivos, hipótesis, variables e indicadores. |
| [DOC-17](DOC-17_Matriz_General_Consistencia.md) | Matriz General de Consistencia | Versión ampliada que integra metodología, instrumentos, técnicas y fuentes. |

---

## Mapa del problema de investigación

```
Expansión de IA generativa + estándar MCP (nov 2024)
    ↓
Agentes LLM conectados a múltiples servidores MCP simultáneamente
    ↓
Tool overload + acumulación de observaciones + mezcla de estados
    ↓
Context rot: degradación progresiva de exactitud, coherencia, tokens y latencia
    (>30% degradación después de 50 turnos — Chroma Research, 2025)
    ↓
Brecha: ningún estudio compara sistemáticamente las técnicas de mitigación
en condiciones multi-MCP controladas
    ↓
[Esta tesis]
Experimento controlado con diseño factorial 2^k:
  RAG-MCP (tool gating) × SessionFacts × MemoryBank/Mem0 × Semantic Caching
Medido mediante IQCR + LongMemEval + LoCoMo + SimpleToolHalluBench
```

---

## Hipótesis central

> **HG:** La aplicación combinada de técnicas de gestión de contexto — RAG-MCP para filtrado dinámico de herramientas, SessionFacts para compresión de historial y MemoryBank para memoria a largo plazo — reduce significativamente el context rot en agentes LLM conectados a múltiples servidores MCP, mejorando en ≥20% el Índice de Calidad de Respuesta Contextual (IQCR) y reduciendo en ≥30% el consumo de tokens respecto a un agente sin técnicas de mitigación.

---

## Fuentes clave

| Fuente | Aporte |
|--------|--------|
| Vaswani et al. (2017) | Arquitectura transformer y ventana de contexto |
| Yao et al. (2022) — ReAct | Ciclo razonamiento-acción-observación del agente |
| Liu et al. (2023) — Lost in the Middle | Evidencia empírica de degradación por posición en el contexto |
| Packer et al. (2023) — MemGPT | Paradigma RAM/disco para memoria de LLMs |
| Zhong et al. (2023) — MemoryBank | Memoria externa con curva de olvido de Ebbinghaus |
| Chhikara et al. (2025) — Mem0 | Memoria adaptativa: −91% tokens, +26% precisión |
| Tang & Gan (2025) — RAG-MCP | Tool gating semántico: −68% tokens en catálogo de 128 herramientas |
| Wu et al. (2024) — LongMemEval | Benchmark de memoria multi-sesión (500 preguntas, 115K tokens) |
| Vercel (2025) — Agente d0 | Caso producción: −37% tokens, +20pp éxito al reducir herramientas |
| Zhou et al. (2026) — Externalization | Marco unificador: pesos → contexto → harness engineering |
| Gartner (2025) | >40% proyectos agénticos cancelados antes de 2027 |
