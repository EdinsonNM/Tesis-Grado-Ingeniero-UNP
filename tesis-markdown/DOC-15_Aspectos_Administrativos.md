# DOC-15 — Aspectos Administrativos

> **Tipo:** Metodológico  
> **Descripción:** Cronograma, recursos humanos y presupuesto del proyecto.

---

Medición del Impacto de Técnicas de Memoria y Gestión de Contexto

sobre la Degradación de Respuestas en Agentes LLM

Conectados a Múltiples Servidores MCP

**DOC-15: Aspectos Administrativos**

Edinson Núñez

Tesis de Maestría

2026

**Aspectos Administrativos**

Los aspectos administrativos de la investigación comprenden la planificación de los recursos necesarios para su ejecución, el presupuesto estimado y el cronograma de actividades. Este capítulo tiene como propósito demostrar la viabilidad operativa del estudio y proveer una hoja de ruta para su gestión durante el período 2025–2026.

**4.1 Recursos Necesarios**

**Recursos Humanos**

El equipo de investigación está conformado por un investigador principal —el tesista— que asume las responsabilidades de diseño experimental, implementación de código, ejecución de experimentos, análisis estadístico y redacción. Se contará con el apoyo de un asesor de tesis con experiencia en sistemas de inteligencia artificial y metodología de investigación, cuya participación se limita a revisión y retroalimentación sobre el avance del estudio. No se requiere personal de campo ni asistentes de investigación dado el carácter computacional del estudio.

**Recursos Tecnológicos**

Los recursos tecnológicos principales son: (a) acceso a la API de Anthropic con créditos suficientes para aproximadamente 1,000,000 de tokens de procesamiento durante la fase experimental; (b) instancias de cómputo en la nube (AWS o GCP) para la ejecución de los experimentos y el almacenamiento de los datasets y resultados; (c) acceso a la API de OpenAI para el modelo de embeddings text-embedding-3-small utilizado en los módulos RAG y tool gating; (d) instancia de Redis Cloud para el módulo de semantic caching (RedisVL); y (e) computadora personal del investigador con al menos 16 GB de RAM para el desarrollo y análisis local.

**Recursos Materiales y de Información**

Los recursos materiales incluyen acceso a los datasets públicos LongMemEval y LoCoMo (disponibles en GitHub sin costo), acceso a bases de datos bibliográficas para la revisión de literatura (Google Scholar, Semantic Scholar, arXiv), y acceso a repositorios de código de los frameworks utilizados (ChromaDB, RedisVL, MLflow). No se requieren materiales físicos especiales dado el carácter íntegramente digital del estudio.

**4.2 Presupuesto**

La Tabla 1 presenta el presupuesto estimado de la investigación, organizado por categorías de gasto. Los valores están expresados en dólares estadounidenses (USD) y soles peruanos (PEN) al tipo de cambio de referencia de S/. 3.75 por dólar.

|                           |                                                                 |              |                          |                       |                       |
| ------------------------- | --------------------------------------------------------------- | ------------ | ------------------------ | --------------------- | --------------------- |
| **Categoría**             | **Ítem**                                                        | **Cantidad** | **Costo Unitario (USD)** | **Costo Total (USD)** | **Costo Total (PEN)** |
| **APIs de IA**            | API Anthropic (Claude Sonnet 4.5) — \~1M tokens                 | 1 paquete    | USD 15.00                | USD 15.00             | S/. 56.25             |
|                           | API OpenAI (embeddings text-embedding-3-small) — \~5M tokens    | 1 paquete    | USD 1.00                 | USD 1.00              | S/. 3.75              |
| **Infraestructura cloud** | AWS EC2 t3.medium (experimentos) — 3 meses                      | 3 meses      | USD 30.00/mes            | USD 90.00             | S/. 337.50            |
|                           | AWS S3 (almacenamiento datasets y resultados) — 50 GB           | 6 meses      | USD 1.15/mes             | USD 6.90              | S/. 25.88             |
|                           | Redis Cloud (semantic caching) — plan Essentials                | 3 meses      | USD 7.00/mes             | USD 21.00             | S/. 78.75             |
| **Licencias y software**  | GitHub Pro (repositorio privado durante desarrollo)             | 12 meses     | USD 4.00/mes             | USD 48.00             | S/. 180.00            |
|                           | MLflow Cloud (tracking de experimentos) — plan gratuito         | —            | USD 0.00                 | USD 0.00              | S/. 0.00              |
| **Bibliografía**          | Acceso a artículos científicos (Sci-Hub / Open Access)          | —            | USD 0.00                 | USD 0.00              | S/. 0.00              |
|                           | Compra de libro Design and Analysis of Experiments (Montgomery) | 1 libro      | USD 80.00                | USD 80.00             | S/. 300.00            |
| **Difusión**              | Impresión y empastado de tesis (3 ejemplares)                   | 3 unidades   | USD 20.00                | USD 60.00             | S/. 225.00            |
|                           | Envío de artículo a conferencia internacional (arXiv preprint)  | 1 preprint   | USD 0.00                 | USD 0.00              | S/. 0.00              |
| **Contingencia (10%)**    | Reserva para costos imprevistos de API o cómputo adicional      | —            | —                        | USD 32.19             | S/. 120.71            |
| **TOTAL**                 |                                                                 |              |                          | **USD 354.09**        | **S/. 1,327.84**      |

> *Nota.* Presupuesto estimado de la investigación. Los costos de API se estiman sobre el uso experimental proyectado; los costos reales pueden variar según el número de reintentos y la variabilidad en la longitud de las respuestas. El presupuesto total es consistente con los límites de financiamiento disponibles para investigaciones de maestría. Tipo de cambio referencial: S/. 3.75 por USD.

**4.3 Cronograma de Actividades**

La Tabla 2 presenta el cronograma de actividades de la investigación en formato de diagrama de Gantt, con resolución mensual para el período julio 2025 – junio 2026. Las actividades están organizadas en cuatro grandes fases: planificación y diseño, desarrollo experimental, análisis y redacción, y difusión y sustentación.

|                                                       |         |         |         |         |         |         |         |         |         |         |         |         |                         |
| ----------------------------------------------------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ----------------------- |
| **Actividad**                                         | **Jul** | **Ago** | **Sep** | **Oct** | **Nov** | **Dic** | **Ene** | **Feb** | **Mar** | **Abr** | **May** | **Jun** | **Responsable**         |
| **FASE 1: Planificación y Diseño**                    |         |         |         |         |         |         |         |         |         |         |         |         |                         |
| 1.1 Revisión sistemática de literatura                | ●       | ●       |         |         |         |         |         |         |         |         |         |         | *Investigador*          |
| 1.2 Redacción del proyecto de tesis (DOC-01 a DOC-13) | ●       | ●       | ●       |         |         |         |         |         |         |         |         |         | *Investigador / Asesor* |
| 1.3 Aprobación del proyecto por comité                |         |         | ●       |         |         |         |         |         |         |         |         |         | *Comité de Tesis*       |
| **FASE 2: Desarrollo Experimental**                   |         |         |         |         |         |         |         |         |         |         |         |         |                         |
| 2.1 Implementación del agente base (baseline)         |         |         | ●       | ●       |         |         |         |         |         |         |         |         | *Investigador*          |
| 2.2 Implementación de técnicas de memoria             |         |         |         | ●       | ●       |         |         |         |         |         |         |         | *Investigador*          |
| 2.3 Construcción del módulo de evaluación             |         |         |         | ●       | ●       |         |         |         |         |         |         |         | *Investigador*          |
| 2.4 Prueba piloto y ajuste del protocolo              |         |         |         |         | ●       |         |         |         |         |         |         |         | *Investigador / Asesor* |
| 2.5 Ejecución experimentos: línea base                |         |         |         |         | ●       | ●       |         |         |         |         |         |         | *Investigador*          |
| 2.6 Ejecución experimentos: técnicas individuales     |         |         |         |         |         | ●       | ●       |         |         |         |         |         | *Investigador*          |
| 2.7 Ejecución experimentos: tool gating               |         |         |         |         |         |         | ●       |         |         |         |         |         | *Investigador*          |
| 2.8 Ejecución diseño factorial 2k                     |         |         |         |         |         |         | ●       | ●       |         |         |         |         | *Investigador*          |
| **FASE 3: Análisis y Redacción**                      |         |         |         |         |         |         |         |         |         |         |         |         |                         |
| 3.1 Análisis estadístico completo                     |         |         |         |         |         |         |         | ●       | ●       |         |         |         | *Investigador*          |
| 3.2 Detección de umbrales (PELT)                      |         |         |         |         |         |         |         |         | ●       |         |         |         | *Investigador*          |
| 3.3 Redacción de resultados y discusión               |         |         |         |         |         |         |         |         | ●       | ●       |         |         | *Investigador / Asesor* |
| 3.4 Revisión y corrección de tesis completa           |         |         |         |         |         |         |         |         |         | ●       | ●       |         | *Investigador / Asesor* |
| **FASE 4: Difusión y Sustentación**                   |         |         |         |         |         |         |         |         |         |         |         |         |                         |
| 4.1 Presentación ante comité para aprobación          |         |         |         |         |         |         |         |         |         |         | ●       |         | *Investigador*          |
| 4.2 Publicación de preprint en arXiv                  |         |         |         |         |         |         |         |         |         |         | ●       | ●       | *Investigador*          |
| 4.3 Sustentación pública de tesis                     |         |         |         |         |         |         |         |         |         |         |         | ●       | *Investigador*          |

> *Nota.* Cronograma de actividades julio 2025 – junio 2026. Los meses están abreviados: Jul = julio 2025 … Jun = junio 2026. El símbolo ● indica que la actividad está planificada para ese mes. Las fases en azul claro son hitos de agrupación sin duración propia. El cronograma tiene un margen de contingencia de dos semanas incorporado en la Fase 4.

Las actividades del cronograma son congruentes con el presupuesto de la Tabla 1: los meses de mayor uso de API (octubre a febrero, correspondientes a las fases de ejecución experimental) coinciden con la mayor acumulación de costos de infraestructura cloud. El cronograma contempla una ventana de corrección y revisión de dos meses (abril y mayo 2026) antes de la sustentación, lo que provee margen para reanálisis si los resultados de las hipótesis requieren ajustes al protocolo experimental.

**Referencias**

<a id="ref-anthropic2024"></a>
Anthropic. (2024). Model Context Protocol specification (v1.0). Anthropic. [https://modelcontextprotocol.io/specification](https://modelcontextprotocol.io/specification)

<a id="ref-hernandez2014"></a>
Hernández Sampieri, R., Fernández Collado, C., & Baptista Lucio, P. (2014). Metodología de la investigación (6.ª ed.). McGraw-Hill Education.

<a id="ref-montgomery2017"></a>
Montgomery, D. C. (2017). Design and analysis of experiments (9.ª ed.). Wiley.

<a id="ref-strubell2019"></a>
Strubell, E., Ganesh, A., & McCallum, A. (2019). Energy and policy considerations for deep learning in NLP. Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics, 3645–3650. [https://doi.org/10.18653/v1/P19-1355](https://doi.org/10.18653/v1/P19-1355)
