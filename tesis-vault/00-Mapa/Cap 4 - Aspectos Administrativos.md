# Cap 4 — Aspectos Administrativos

> Cuarto capítulo. Define los recursos necesarios, el presupuesto estimado y el cronograma de actividades para ejecutar la investigación.

← [[Cap 3 - Marco Metodologico]] | → [[Cap 5 - Referencias]]

Ver página detallada: [[Aspectos Administrativos]]

---

## 4.1 Recursos Necesarios

**Computacionales**:
- Acceso a API de modelo LLM de frontera (ej. Claude Sonnet o GPT-4o).
- Servidor o máquina local con GPU para ChromaDB y RedisVL.
- Almacenamiento para datasets: LongMemEval (~2 GB), LoCoMo (~500 MB), benchmarks adicionales.

**Software** (todos open-source o con tier gratuito):
- Python 3.11+, MCP SDK, LangChain/LangGraph.
- ChromaDB, RedisVL, SQLite.
- scipy, statsmodels, pingouin, ruptures, BERTScore.
- Obsidian (este vault).

**Humanos**:
- Investigador principal (tiempo completo durante fase experimental).
- Asesor metodológico (revisión de diseño estadístico).

---

## 4.2 Presupuesto

> Pendiente de actualización con valores exactos.

| Ítem | Estimado |
|---|---|
| Costo de API LLM (tokens de experimento) | Por definir según proveedor |
| Infraestructura cloud (si aplica) | Por definir |
| Materiales bibliográficos | Acceso institucional / gratuito |
| **Total estimado** | **Por definir** |

---

## 4.3 Cronograma de Actividades

> Cronograma tentativo. Actualizar con fechas absolutas una vez aprobado el proyecto.

| Fase | Actividad | Duración estimada |
|---|---|---|
| 1 | Revisión de literatura y marco teórico | 4 semanas |
| 2 | Diseño del experimento y preparación del entorno | 3 semanas |
| 3 | Experimento: línea base | 2 semanas |
| 4 | Experimento: técnicas individuales | 3 semanas |
| 5 | Experimento: tool gating y diseño factorial | 3 semanas |
| 6 | Análisis estadístico y detección de umbrales | 2 semanas |
| 7 | Redacción de resultados y conclusiones | 3 semanas |
| 8 | Revisión y correcciones | 2 semanas |
| **Total** | | **~22 semanas** |
