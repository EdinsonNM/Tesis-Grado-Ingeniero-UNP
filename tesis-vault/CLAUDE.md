# CLAUDE.md — Schema del Wiki de Tesis

Este documento define cómo está estructurado el wiki, qué convenciones usar y qué flujo seguir en cada operación. Está pensado para que cualquier LLM que trabaje en esta bóveda mantenga consistencia entre sesiones.

---

## Contexto del proyecto

Este wiki documenta una tesis de investigación sobre:

> **Medición del impacto de técnicas de memoria y gestión de contexto sobre la degradación de respuestas en agentes LLM conectados a múltiples servidores MCP.**

El problema central es el **Context rot**: la degradación progresiva de la calidad de respuestas de un agente LLM cuando el contexto activo crece en conversaciones multi-turno con múltiples servidores MCP.

Las técnicas de mitigación estudiadas son: Tool gating, SessionFacts, MemoryBank, Caching semántico y Recuperación federada.

La métrica compuesta de evaluación es el **IQCR** (Índice de Calidad de Respuesta en Contexto).

---

## Estructura de carpetas

```
tesis-vault/
├── CLAUDE.md               ← este archivo (schema del wiki)
├── index.md                ← catálogo de todas las páginas del wiki
├── log.md                  ← registro cronológico de actividad
├── Bienvenido.md           ← punto de entrada para el usuario
│
├── 00-Mapa/                ← mapas y árboles de navegación
│   └── Arbol de la tesis.md
│
├── 01-Tesis/               ← estructura formal de la tesis
│   ├── Resumen de la tesis.md
│   ├── Problema de investigacion.md
│   ├── Objetivos de investigacion.md
│   ├── Hipotesis de investigacion.md
│   └── Variables e indicadores.md
│
├── 02-Marco-Teorico/       ← marco teórico y síntesis conceptual
│   └── Mapa del marco teorico.md
│
├── 03-Metodologia/         ← diseño metodológico y matrices
│   ├── Diseno metodologico.md
│   └── Matriz de consistencia.md
│
├── 04-Conceptos/           ← páginas individuales de conceptos y términos
│   └── *.md
│
├── 05-Fuentes/             ← fichas individuales por paper/fuente
│   ├── Catalogo inicial de fuentes.md
│   └── *.md (una ficha por fuente)
│
├── 99-Inbox/               ← bandeja de entrada para términos sin expandir
│   └── Terminos por expandir.md
│
└── rules/                  ← archivos de configuración del LLM
    └── llm-wiki.md
```

**Regla de inmutabilidad:** los documentos fuente en `investigación/` (fuera del vault) son de solo lectura. El LLM lee desde ahí pero nunca modifica esos archivos.

---

## Formato de las páginas de conceptos (`04-Conceptos/`)

Cada concepto es un archivo `.md` con nombre en minúsculas, usando espacios (ej. `Context rot.md`). La estructura estándar es:

```markdown
# Nombre del concepto

## Definición

Texto de 2-4 oraciones. Vincular otros conceptos con [[doble corchete]].

## [Secciones según el tipo de concepto]

...contenido relevante...

## En la tesis

Cómo se usa o referencia este concepto en la investigación.

## Referencias

- [[Fuente 1]]
- [[Fuente 2]]
```

Las secciones internas varían según el tipo:
- **Concepto técnico**: Definición, Cómo funciona, Relación con otros conceptos, En la tesis
- **Métrica/variable**: Definición operacional, Cómo se mide/calcula, Limitaciones, En la tesis
- **Dataset/benchmark**: Descripción, Estructura, Métricas que evalúa, URL, En la tesis
- **Técnica de mitigación**: Descripción, Mecanismo, Ventajas/limitaciones, En la tesis
- **Concepto metodológico**: Definición, Cuándo se usa, Cómo se aplica en la tesis

---

## Formato de las fichas de fuentes (`05-Fuentes/`)

Cada paper o fuente relevante tiene su propia ficha. Nombre del archivo: `Apellido YYYY - Titulo corto.md`.

```markdown
# Apellido et al. (YYYY) — Título corto

## Referencia APA

Apellido, A., & Apellido, B. (YYYY). Título completo. *Revista/Conferencia*, volumen(número), páginas. https://doi.org/...

## Pregunta que responde

¿Qué problema o pregunta de investigación aborda?

## Método

Tipo de estudio, datasets usados, arquitectura experimental.

## Métricas reportadas

Qué métricas usa y qué resultados obtiene.

## Aporte a la tesis

Cómo contribuye específicamente a la investigación actual.

## Conceptos relacionados

- [[Concepto 1]]
- [[Concepto 2]]
```

---

## Convenciones generales

- **Wikilinks**: usar siempre `[[Nombre de la página]]` para vincular páginas. Si el nombre de la página difiere del texto a mostrar: `[[Nombre de la página|texto mostrado]]`.
- **Sin tildes en nombres de archivo**: los nombres de archivo no usan tildes ni caracteres especiales (ej. `Diseno metodologico.md`, no `Diseño metodológico.md`). El contenido interno sí puede usar tildes.
- **Idioma**: todo el wiki está en español. Las definiciones técnicas pueden incluir el término en inglés entre paréntesis.
- **Sin metadatos YAML por defecto**: no agregar frontmatter YAML a menos que sea necesario para Dataview.
- **Estilo de escritura**: conciso y técnico. Priorizar definiciones operacionales claras, no descripciones enciclopédicas extensas.

---

## Operaciones estándar

### Ingest (agregar una nueva fuente)

1. Leer el documento fuente (PDF o MD en `investigación/`).
2. Crear o actualizar la ficha en `05-Fuentes/`.
3. Crear o actualizar páginas de conceptos en `04-Conceptos/` que el paper introduce o amplía.
4. Actualizar `Catalogo inicial de fuentes.md` si es necesario.
5. Actualizar `index.md` con los archivos nuevos o modificados.
6. Agregar entrada al `log.md`: `## [YYYY-MM-DD] ingest | Apellido YYYY — Título corto`.

### Expandir término del inbox

1. Leer `99-Inbox/Terminos por expandir.md`.
2. Crear la página en `04-Conceptos/` con el formato estándar.
3. Vincular la nueva página desde `Arbol de la tesis.md` o `Mapa del marco teorico.md` donde corresponda.
4. Eliminar el término de `Terminos por expandir.md`.
5. Actualizar `index.md`.
6. Agregar entrada al `log.md`: `## [YYYY-MM-DD] expand | Nombre del concepto`.

### Query (responder una pregunta)

1. Leer `index.md` para identificar páginas relevantes.
2. Leer las páginas relevantes.
3. Sintetizar la respuesta con citas `[[página]]`.
4. Si la respuesta es valiosa y reutilizable, crear una nueva página en `04-Conceptos/` o en la carpeta apropiada.
5. Agregar entrada al `log.md`: `## [YYYY-MM-DD] query | Pregunta resumida`.

### Lint (mantenimiento del wiki)

Buscar periódicamente:
- Páginas huérfanas (sin inbound links).
- Conceptos mencionados en el texto pero sin página propia.
- Contradicciones entre páginas.
- Fichas de fuentes incompletas.
- Términos en `Terminos por expandir.md` que han estado pendientes mucho tiempo.

Agregar entrada al `log.md`: `## [YYYY-MM-DD] lint | Resumen de hallazgos`.

---

## Archivos especiales

### `index.md`
Catálogo de todo el wiki, organizado por categoría. El LLM lo lee primero al responder preguntas. Se actualiza en cada ingest o expand. Formato:

```markdown
## Categoría

- [[Nombre de página]] — descripción de una línea
```

### `log.md`
Registro append-only. Cada entrada empieza con `## [YYYY-MM-DD] tipo | descripción` para que sea grep-able. Nunca se borran entradas del log.

---

## Estado actual del wiki

- **Última actualización del schema**: 2026-05-01
- **Páginas de conceptos activas**: ver `index.md`
- **Fichas de fuentes activas**: ver `index.md`
- **Términos pendientes en inbox**: ver `99-Inbox/Terminos por expandir.md`
