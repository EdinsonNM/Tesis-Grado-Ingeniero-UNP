# DOC-08 — Justificación e Importancia

> **Tipo:** Tesis — Capítulo I  
> **Descripción:** Argumentación teórica, práctica y metodológica que sustenta la investigación.

---

Medición del Impacto de Técnicas de Memoria y Gestión de Contexto

sobre la Degradación de Respuestas en Agentes LLM

Conectados a Múltiples Servidores MCP

**DOC-08: Justificación e Importancia**

Edinson Núñez

Tesis de Maestría

2026

**Justificación e Importancia**

La justificación de una investigación expone las razones de orden teórico, práctico, metodológico y social que fundamentan su realización. En el presente capítulo se argumenta la pertinencia del estudio desde cuatro dimensiones complementarias: (a) la justificación teórica, que sustenta la contribución al cuerpo de conocimiento científico existente; (b) la justificación práctica, que evidencia el valor utilitario de los resultados para la industria; (c) la justificación metodológica, que describe el aporte instrumental de la propuesta experimental; y (d) la justificación social, que articula el beneficio para la sociedad y, en particular, para el contexto peruano. Adicionalmente, se expone la importancia del estudio en términos de oportunidad y originalidad.

**Justificación Teórica**

El campo de los agentes LLM ha experimentado un crecimiento exponencial desde la publicación de ReAct ([Yao et al., 2022](https://arxiv.org/abs/2210.03629)) y Toolformer ([Schick et al., 2023](https://arxiv.org/abs/2302.04761)), que demostraron la capacidad de los modelos de lenguaje para razonar sobre acciones y llamadas a herramientas externas. Sin embargo, el estudio sistemático del comportamiento de estos agentes bajo condiciones de contexto extendido —especialmente en arquitecturas multi-servidor— permanece en una etapa incipiente.

La emergencia del Model Context Protocol ([Anthropic, 2024](https://modelcontextprotocol.io/specification)) como estándar abierto para la interoperabilidad entre agentes LLM y herramientas externas plantea preguntas teóricas no resueltas. La literatura disponible sobre degradación de respuestas en contextos largos ([Liu et al., 2023](https://doi.org/10.1162/tacl\_a\_00638); [Shi et al., 2023](https://proceedings.mlr.press/v202/shi23a.html)) se ha desarrollado principalmente en escenarios de lectura de documentos extensos, sin considerar la dinámica acumulativa propia de las arquitecturas multi-MCP: resultados intermedios de herramientas, esquemas de herramientas repetidos, estados de sesión múltiples y tráfico de metadatos de servidor que se acumulan en el contexto de forma estructuralmente diferente a los documentos de texto.

La presente investigación contribuye teóricamente en tres frentes. Primero, propone y operacionaliza el concepto de context rot en arquitecturas multi-MCP, diferenciándolo de la simple degradación por longitud de contexto que ha sido estudiada en la literatura previa. Segundo, sistematiza un marco de clasificación de técnicas de mitigación —memoria externa, compresión de contexto, filtrado de herramientas y caching semántico— aplicado específicamente al escenario MCP, lo que no existe en la literatura actual. Tercero, genera evidencia empírica cuantitativa sobre los umbrales a partir de los cuales el context rot se vuelve estadísticamente significativo, lo que permite avanzar desde la observación cualitativa hacia la modelización predictiva del fenómeno.

Estos aportes teóricos son congruentes con las brechas identificadas en el estado del arte (DOC-03): ninguno de los benchmarks de evaluación disponibles —ToolBH, ToolHaystack, LongMemEval, LoCoMo— ha sido diseñado específicamente para medir la degradación en escenarios MCP multi-servidor, y ningún estudio ha comparado sistemáticamente las técnicas de memoria en dicho contexto.

**Justificación Práctica**

Desde el punto de vista práctico, los resultados de este estudio aportan valor directo a tres categorías de actores: desarrolladores de sistemas agentes, organizaciones que despliegan IA en producción, y proveedores de plataformas MCP.

**Para Desarrolladores de Sistemas Agentes**

Los desarrolladores que construyen agentes LLM sobre infraestructuras MCP carecen actualmente de guías empíricas que les orienten sobre qué técnicas de memoria implementar, en qué orden de prioridad y bajo qué condiciones de carga. La elección actual se basa en intuición técnica o benchmarks de propósito general, lo que resulta en sistemas con rendimiento subóptimo en producción. Los resultados de esta tesis proporcionarán recomendaciones basadas en evidencia: umbrales de longitud de conversación a partir de los cuales el RAG semántico se vuelve indispensable, condiciones bajo las cuales el tool gating supera en beneficio al overhead que introduce, y configuraciones de caching que minimizan la latencia sin comprometer la frescura de los datos.

**Para Organizaciones que Despliegan IA en Producción**

Las organizaciones que implementan agentes LLM en entornos empresariales enfrentan costos operativos directamente relacionados con el consumo de tokens. [Salim et al. (2026)](https://arxiv.org/abs/2601.14470) demostraron empíricamente que en sistemas multi-agente, los tokens de entrada —que representan contexto transmitido y acumulado— constituyen en promedio el 53.9% del consumo total, evidenciando que el costo operativo de inferencia está dominado por la acumulación de contexto, no por la generación de respuestas nuevas. La investigación aportará métricas cuantitativas de reducción de consumo de tokens por técnica, lo que permitirá a los equipos de arquitectura de IA realizar análisis de costo-beneficio informados antes de seleccionar su stack tecnológico de memoria. Para el contexto peruano, donde el 58.4% de las empresas que adoptan IA reportan restricciones de presupuesto como barrera principal ([INEI, 2024](https://www.inei.gob.pe)), esta información tiene un impacto multiplicador en la viabilidad de los proyectos.

**Para Proveedores de Plataformas MCP**

Anthropic y los desarrolladores de servidores MCP de terceros se beneficiarán de datos empíricos que guíen el diseño de mejores prácticas de exposición de herramientas: número óptimo de herramientas por servidor, granularidad de las descripciones de herramientas para minimizar el overhead de tokens, y formatos de respuesta que faciliten la compresión de resultados intermedios. Estos insumos son transferibles a la especificación del protocolo MCP y pueden informar futuras versiones del estándar.

**Justificación Metodológica**

La justificación metodológica del presente estudio se sustenta en la ausencia de un protocolo experimental estandarizado para medir el context rot en arquitecturas multi-MCP. La investigación propone y valida un diseño experimental reproducible que incluye: (a) un conjunto de escenarios de prueba controlados, organizados en niveles de complejidad creciente; (b) un índice compuesto de calidad de respuesta (IQCR) que integra métricas de exactitud, coherencia, tasa de alucinación y eficiencia de tokens; y (c) un procedimiento de ground truth annotation que permite la validación automatizada de respuestas.

Este protocolo es adaptable a otros modelos LLM, otros protocolos de integración de herramientas distintos de MCP, y otros dominios de aplicación. Al publicarse como parte de la tesis, sirve como instrumento reutilizable para investigaciones futuras, lo que amplifica el impacto metodológico más allá del problema específico estudiado.

Adicionalmente, el uso de un diseño factorial 2k reducido para el análisis de técnicas combinadas introduce rigor estadístico que supera el enfoque de comparación uno a uno predominante en estudios previos sobre memoria en LLM. La aplicación de análisis de segmentación de series temporales para la detección de umbrales de degradación constituye también una contribución metodológica aplicable al campo de la evaluación de sistemas de IA.

**Justificación Social**

La dimensión social de la justificación trasciende el ámbito técnico para considerar el impacto del estudio sobre el bienestar de los usuarios finales de sistemas de IA y sobre la capacidad del Perú para participar en la economía digital global.

**Confiabilidad de los Sistemas de IA para Usuarios Finales**

El context rot tiene consecuencias directas sobre la experiencia del usuario: un agente que olvida instrucciones previas, contradice respuestas anteriores o alucina información en conversaciones largas genera desconfianza y abandono del sistema. En sectores críticos como salud, educación y servicios públicos, donde los sistemas de IA asistida están siendo desplegados con creciente frecuencia, la degradación de respuestas no es un problema de rendimiento técnico sino un riesgo de daño real al usuario. Comprender y mitigar el context rot contribuye directamente a sistemas de IA más confiables y seguros para la sociedad.

**Capacitación de Talento Técnico en el Perú**

El Perú ocupa el puesto 60 en el Government AI Readiness Index 2025 ([Oxford Insights, 2025](https://oxfordinsights.com/wp-content/uploads/2025/12/2025-Government-AI-Readiness-Index-2.pdf)) y enfrenta una brecha significativa en talento técnico especializado en IA. Solo el 6% de las empresas peruanas que adoptan IA declaran tener equipos técnicos con capacidades avanzadas, frente al 17–18% de Chile y Colombia ([INEI, 2024](https://www.inei.gob.pe)). La realización de investigación de posgrado en temas de frontera como la arquitectura de agentes LLM y los protocolos MCP contribuye a cerrar esta brecha formando investigadores locales capaces de producir conocimiento relevante para el contexto nacional e internacional.

**Adopción Informada de IA en el Contexto Nacional**

Las instituciones peruanas que han comenzado a adoptar herramientas de IA —incluyendo entidades públicas que operan bajo los lineamientos del Decreto Supremo N° 007-2020-PCM sobre transformación digital— requieren criterios técnicos para evaluar y seleccionar soluciones de agentes inteligentes. Los resultados de esta investigación proveerán criterios de selección basados en evidencia empírica local y alineados con las restricciones de infraestructura del mercado peruano, donde el ancho de banda, el costo por token y la disponibilidad de APIs de embeddings representan restricciones reales que no están capturadas en estudios realizados en entornos de alta disponibilidad.

**Importancia del Estudio**

**Oportunidad Temporal**

El Model Context Protocol fue publicado por Anthropic en noviembre de 2024 y alcanzó adopción masiva en menos de seis meses, con más de 1,000 servidores MCP públicos disponibles para julio de 2025 ([MCP Registry, 2025](https://mcpregistry.dev)). Esta adopción acelerada significa que miles de organizaciones están desplegando arquitecturas multi-MCP en producción sin disponer de guías empíricas sobre los riesgos de degradación de respuestas. La presente investigación llega en el momento preciso en que la comunidad técnica necesita los datos para tomar decisiones informadas de diseño arquitectónico. Un estudio realizado dos años más tarde tendría menor impacto, pues las mejores prácticas habrán emergido de forma empírica y desordenada a través de la práctica industrial.

**Originalidad y Posición en la Literatura**

Una revisión sistemática de la literatura (realizada en la preparación de esta tesis) no encontró ningún estudio que aborde específicamente la medición del context rot en arquitecturas multi-MCP bajo un diseño experimental controlado. Los estudios más próximos —[Liu et al. (2023)](https://doi.org/10.1162/tacl\_a\_00638) sobre pérdida de información en contextos largos, [Chroma Research (2025)](https://www.trychroma.com/blog/context-rot) sobre degradación en sistemas de producción, y [Tang et al. (2025)](https://arxiv.org/abs/2502.03415) sobre RAG-MCP— tratan subconjuntos del problema sin integrarlo en un marco unificado. Esta originalidad posiciona la tesis como un aporte de frontera al campo.

**Escalabilidad de los Resultados**

Los patrones de degradación de contexto y las técnicas de mitigación identificadas en esta investigación son, en principio, transferibles a cualquier protocolo de integración de herramientas basado en estándares abiertos. A medida que el ecosistema de agentes LLM evoluciona hacia arquitecturas más complejas —agentes multi-agente, sistemas de orquestación jerárquica, memoria federada— los hallazgos de este estudio servirán como referencia baseline para investigaciones de mayor escala.

**Síntesis de la Justificación**

La Tabla 1 resume las cuatro dimensiones de justificación, sus argumentos centrales y los beneficiarios directos de cada una:

|                  |                                                                                                                                                                      |                                                                                          |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Dimensión**    | **Argumento Central**                                                                                                                                                | **Beneficiarios Directos**                                                               |
| **Teórica**      | Llena la brecha de conocimiento sobre context rot en arquitecturas multi-MCP; operacionaliza el concepto y genera evidencia cuantitativa de umbrales de degradación. | Comunidad científica de IA, investigadores de evaluación de LLM                          |
| **Práctica**     | Provee recomendaciones basadas en evidencia para la selección de técnicas de memoria; cuantifica la reducción de consumo de tokens por técnica.                      | Desarrolladores de agentes, arquitectos de IA, empresas que despliegan LLM en producción |
| **Metodológica** | Propone un protocolo experimental reproducible y un índice compuesto de calidad de respuesta (IQCR) aplicable a estudios futuros.                                    | Investigadores de benchmarking de LLM, comunidad de evaluación de IA                     |
| **Social**       | Contribuye a sistemas de IA más confiables para usuarios finales y al desarrollo de talento técnico especializado en el Perú.                                        | Usuarios finales de IA, instituciones peruanas, ecosistema TI nacional                   |

> *Nota.* Síntesis de las dimensiones de justificación del estudio y sus beneficiarios directos.

**Referencias**

Anthropic. (2024). Model Context Protocol specification (v1.0). Anthropic. [https://modelcontextprotocol.io/specification](https://modelcontextprotocol.io/specification)

Chroma Research. (2025). Context rot in production LLM systems: A benchmark study. Chroma. [https://www.trychroma.com/blog/context-rot](https://www.trychroma.com/blog/context-rot)

INEI. (2024). Encuesta Nacional de Empresas: Uso de tecnologías de información e inteligencia artificial. Instituto Nacional de Estadística e Informática. [https://www.inei.gob.pe](https://www.inei.gob.pe)

Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2023). Lost in the middle: How language models use long contexts. Transactions of the Association for Computational Linguistics, 12, 157–173. [https://doi.org/10.1162/tacl\_a\_00638](https://doi.org/10.1162/tacl\_a\_00638)

MCP Registry. (2025). Public MCP server catalog. [https://mcpregistry.dev](https://mcpregistry.dev)

Oxford Insights. (2025). Government AI Readiness Index 2025. Oxford Insights. https://oxfordinsights.com/wp-content/uploads/2025/12/2025-Government-AI-Readiness-Index-2.pdf

Packer, C., Wooders, S., Lin, K., Fang, V., Patil, S. G., Stoica, I., & Gonzalez, J. E. (2023). MemGPT: Towards LLMs as operating systems. arXiv. [https://arxiv.org/abs/2310.08560](https://arxiv.org/abs/2310.08560)

Presidencia del Consejo de Ministros. (2020). Decreto Supremo N° 007-2020-PCM: Política Nacional de Transformación Digital al 2030. El Peruano. [https://www.gob.pe/institucion/pcm/normas-legales/659568-007-2020-pcm](https://www.gob.pe/institucion/pcm/normas-legales/659568-007-2020-pcm)

Salim, M., Latendresse, J., Khatoonabadi, S., & Shihab, E. (2026). Tokenomics: Quantifying where tokens are used in agentic software engineering. arXiv. [https://arxiv.org/abs/2601.14470](https://arxiv.org/abs/2601.14470)

Schick, T., Dwivedi-Yu, J., Dessì, R., Raileanu, R., Lomeli, M., Zettlemoyer, L., Cancedda, N., & Scialom, T. (2023). Toolformer: Language models can teach themselves to use tools. Advances in Neural Information Processing Systems, 36. [https://arxiv.org/abs/2302.04761](https://arxiv.org/abs/2302.04761)

Shi, F., Chen, X., Misra, K., Scales, N., Dohan, D., Chi, E., Schärli, N., & Zhou, D. (2023). Large language models can be easily distracted by irrelevant context. Proceedings of the 40th International Conference on Machine Learning, 202, 31210–31227. [https://proceedings.mlr.press/v202/shi23a.html](https://proceedings.mlr.press/v202/shi23a.html)

Tang, R., Jin, Z., Alexandrov, A., Shao, Y., Shi, P., & Pan, L. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. arXiv. [https://arxiv.org/abs/2502.03415](https://arxiv.org/abs/2502.03415)

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. arXiv. [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)
