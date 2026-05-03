# Tesis de Grado — Ingeniería Informática

**Universidad Nacional de Piura**
Facultad de Ingeniería Informática

## Medición del impacto de técnicas de memoria y gestión de contexto sobre la degradación de respuestas en agentes LLM conectados a múltiples servidores MCP

Este repositorio contiene toda la documentación, investigación y notas de trabajo desarrolladas para obtener el título de **Ingeniero Informático** en la Universidad Nacional de Piura. La investigación estudia el fenómeno de *context rot* en agentes LLM conectados a múltiples servidores MCP, y evalúa técnicas de memoria y gestión de contexto para mitigarlo.

---

## Equipo

| Rol | Nombre |
|-----|--------|
| Asesor Principal | Pedro Criollo Gonzales |
| Asesora Secundaria | Dra. Carmen Infante |
| Asesor Secundario | Ing. Moisés Savedra |

---

## Pregunta de investigación

> ¿En qué medida la aplicación de técnicas de memoria y gestión de contexto reduce la degradación de respuestas (*context rot*) en agentes LLM conectados a múltiples servidores MCP, en comparación con una arquitectura base sin dichas técnicas?

---

## Estructura del repositorio

```
Tesis/
├── investigación/          # Documentos Word de la tesis formal
│   ├── DOC-01_Indice_Documentos.docx
│   ├── DOC-02_Catalogo_Fuentes.docx
│   ├── DOC-04_Indicadores_por_Paper.docx
│   ├── DOC-05_Introduccion_Tesis.docx
│   ├── DOC-06_Realidad_Problematica.docx
│   ├── DOC-07_Formulacion_Problema.docx
│   ├── DOC-08_Justificacion_Importancia.docx
│   ├── DOC-09_Objetivos.docx
│   ├── DOC-10_Delimitacion.docx
│   ├── DOC-11_Bases_Teoricas.docx
│   ├── DOC-12_Glosario.docx
│   ├── DOC-13_Hipotesis.docx
│   ├── DOC-14_Marco_Metodologico.docx
│   ├── DOC-15_Aspectos_Administrativos.docx
│   ├── DOC-16_Matriz_Consistencia.docx
│   └── DOC-17_Matriz_General_Consistencia.docx
│
└── tesis-vault/            # Vault de Obsidian (base de conocimiento interconectada)
    ├── 00-Mapa/            # Mapas de contenido por capítulo (MOC)
    ├── 01-Tesis/           # Núcleo de la tesis: problema, objetivos, hipótesis, variables
    ├── 02-Marco-Teorico/   # Antecedentes, bases teóricas, glosario, marco referencial
    ├── 03-Metodologia/     # Diseño metodológico y matrices de consistencia
    ├── 04-Conceptos/       # Notas atómicas organizadas por dominio
    │   ├── A-Problema/     # Context rot, tool overload, lost in the middle
    │   ├── B-Arquitectura/ # Agentes LLM, servidores MCP, ReAct
    │   ├── C-Mitigacion/   # RAG, SessionFacts, MemoryBank, tool gating, caching
    │   ├── D-Metricas/     # IQCR, BERTScore, exactitud, coherencia
    │   ├── E-Benchmarks/   # LoCoMo, LongMemEval, SimpleToolHalluBench
    │   └── F-Metodologia/  # Diseño factorial 2^k, PELT, TOST, AHP
    ├── 05-Fuentes/         # Notas de papers académicos (formato estándar)
    └── 99-Inbox/           # Términos y conceptos pendientes de expandir
```

### Carpeta `investigación/`

Contiene los documentos Word que corresponden a las secciones formales de la tesis, numerados con el prefijo `DOC-XX` para facilitar el seguimiento. Cada archivo representa una sección específica del documento final (introducción, realidad problemática, objetivos, hipótesis, metodología, etc.).

### Carpeta `tesis-vault/`

Vault de [Obsidian](https://obsidian.md/) que funciona como base de conocimiento interconectada. Las notas se organizan en capas:

- **00-Mapa** — mapas de contenido (MOC) que enlazan las notas de cada capítulo, ofreciendo una vista de alto nivel del árbol de la tesis.
- **01-Tesis** — las notas centrales: problema de investigación, objetivos, hipótesis, variables e indicadores, justificación y alcance.
- **02-Marco-Teorico** — antecedentes, bases teóricas y glosario de términos técnicos.
- **03-Metodologia** — diseño metodológico y matrices de consistencia.
- **04-Conceptos** — notas atómicas organizadas en sub-dominios temáticos (problema, arquitectura, técnicas de mitigación, métricas, benchmarks y métodos estadísticos).
- **05-Fuentes** — notas de los papers académicos revisados, cada una vinculada a los conceptos relevantes del vault.
- **99-Inbox** — área de entrada para términos y conceptos aún por desarrollar.

---

## Resumen del trabajo de investigación

La tesis estudia el **context rot** — degradación progresiva de la calidad de respuestas — en agentes LLM conectados simultáneamente a múltiples servidores MCP. El fenómeno surge por tres mecanismos que se potencian mutuamente: *tool overload* (sobrecarga de descripciones de herramientas), acumulación de resultados intermedios en el contexto activo, y mezcla de estados de sesión entre servidores.

El aporte es un **protocolo experimental reproducible** que compara cinco técnicas de mitigación — RAG semántico, SessionFacts, MemoryBank, semantic caching y tool gating — mediante el índice compuesto IQCR (exactitud, tasa de alucinación, coherencia BERTScore y consumo de tokens). El diseño experimental incluye línea base sin técnica, comparación de técnicas individuales, combinación óptima mediante diseño factorial 2^k y localización de umbrales de degradación con el algoritmo PELT.

---

## Fuentes clave consultadas

- Vaswani et al. (2017) — *Attention Is All You Need*
- Brown et al. (2020) — *Language Models are Few-Shot Learners* (GPT-3)
- Lewis et al. (2020) — *Retrieval-Augmented Generation (RAG)*
- Yao et al. (2022) — *ReAct: Synergizing Reasoning and Acting*
- Liu et al. (2023) — *Lost in the Middle*
- Packer et al. (2023) — *MemGPT*
- Schick et al. (2023) — *Toolformer*
- Zhong et al. (2023) — *MemoryBank*
- Maharana et al. (2024) — *LoCoMo*
- Wu et al. (2024) — *LongMemEval*
- Chhikara et al. (2025) — *Mem0*
- Tang et al. (2025) — *RAG-MCP*
- Yin et al. (2026) — *SimpleToolHalluBench*
- Zhou et al. (2026) — *Externalization in LLM Agents*
