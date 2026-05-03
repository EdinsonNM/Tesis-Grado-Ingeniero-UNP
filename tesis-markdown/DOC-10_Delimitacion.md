# DOC-10 — Delimitación

> **Tipo:** Tesis — Capítulo I  
> **Descripción:** Delimitación espacial, temporal, temática y teórica del estudio.

---

Medición del Impacto de Técnicas de Memoria y Gestión de Contexto

sobre la Degradación de Respuestas en Agentes LLM

Conectados a Múltiples Servidores MCP

**DOC-10: Delimitación**

Edinson Núñez

Tesis de Maestría

2026

**Delimitación de la Investigación**

La delimitación define con precisión los límites dentro de los cuales se desarrolla la investigación. Establece el alcance en dimensiones temáticas, espaciales, temporales y poblacionales, diferenciando lo que el estudio abarca de lo que queda expresamente fuera de su alcance. Una delimitación bien fundamentada es condición necesaria para la validez interna del diseño experimental y para la correcta interpretación y transferencia de los resultados.

La presente investigación está acotada en cuatro dimensiones principales: (a) temática, que define los conceptos, fenómenos y técnicas que serán estudiados; (b) tecnológica, que especifica los modelos, protocolos e infraestructura que formarán parte del experimento; (c) espacial y poblacional, que delimita el contexto geográfico e institucional del estudio; y (d) temporal, que fija el horizonte cronológico de la investigación. Adicionalmente, se identifican explícitamente las áreas excluidas, con el fin de prevenir malinterpretaciones del alcance y facilitar comparaciones con estudios futuros.

**Delimitación Temática**

La investigación se circunscribe al estudio del fenómeno de degradación de respuestas (context rot) en agentes basados en modelos de lenguaje de gran escala (LLM) que operan bajo el Model Context Protocol (MCP). El foco temático se articula en torno a tres ejes conceptuales interdependientes:

**Eje 1: Context Rot en Arquitecturas Multi-MCP**

El primer eje comprende el estudio de los mecanismos por los cuales la calidad de las respuestas de un agente LLM se deteriora progresivamente a medida que el contexto de conversación crece. El estudio se limita a los tres mecanismos identificados en la literatura como propios de las arquitecturas multi-MCP: (a) tool overload, originado por la exposición simultánea de un gran número de herramientas al modelo; (b) acumulación de resultados intermedios, derivada de la retención de outputs de herramientas previas en el contexto activo; y (c) mezcla de estados de sesión, generada por la coexistencia de metadatos de múltiples servidores MCP en el mismo contexto.

Quedan fuera de este eje los fenómenos de degradación originados por: (a) limitaciones de capacidad de atención (attention sink) en el modelo base, que constituyen un problema de arquitectura de red neuronal y no de gestión de contexto; (b) sesgos de posición en secuencias largas, que aunque relacionados con el problema son un fenómeno de nivel de modelo y no de nivel de agente; y (c) degradación por deriva de distribución (distribution shift) en los datos de entrada del modelo.

**Eje 2: Técnicas de Memoria y Gestión de Contexto**

El segundo eje abarca las técnicas de software implementables a nivel de agente para mitigar el context rot. Las técnicas incluidas en el estudio son: (a) RAG semántico, en sus variantes de recuperación densa (dense retrieval) con modelos de embeddings de acceso comercial o de código abierto; (b) SessionFacts, como mecanismo de compresión del estado de sesión en estructuras clave-valor serializables; (c) MemoryBank, como sistema de memoria externa con acceso indexado y política de olvido basada en relevancia; y (d) semantic caching basado en similitud vectorial (RedisVL o equivalente), como mecanismo de reutilización de respuestas para consultas semánticamente equivalentes.

Adicionalmente, se incluyen estrategias de tool gating: carga diferida de herramientas y filtrado semántico por relevancia de consulta. Estas estrategias no son técnicas de memoria en sentido estricto, pero son parte integral del problema de gestión de contexto en arquitecturas MCP y han sido identificadas como uno de los mecanismos de mitigación con mayor potencial práctico.

Se excluyen del estudio: (a) técnicas de fine-tuning o ajuste de parámetros del modelo para mejorar la retención de información, ya que implican modificación del modelo base y no son aplicables en entornos de uso de APIs comerciales; (b) mecanismos de atención modificada (sparse attention, sliding window attention), que operan a nivel de arquitectura de red y requieren acceso al código fuente del modelo; (c) técnicas de compresión de contexto basadas en destilación (prompt distillation), cuya efectividad depende en gran medida del dominio específico de aplicación y no es generalizable en el alcance de este estudio.

**Eje 3: Evaluación y Métricas**

El tercer eje delimita el conjunto de métricas y benchmarks que se utilizarán para medir el fenómeno. El estudio se limita a cuatro métricas primarias: exactitud de respuesta (comparación contra ground truth anotado), tasa de alucinación (verificación automatizada de afirmaciones factuales), coherencia conversacional (similitud semántica entre turnos consecutivos) y consumo de tokens por turno (como proxy de eficiencia computacional). Estas métricas son mensurables de forma objetiva y reproducible, sin requerir evaluación humana en tiempo real.

Quedan fuera del alcance métrico: (a) la evaluación subjetiva de la calidad de respuesta mediante jueces humanos, aunque se reconoce su valor complementario; (b) métricas de equidad algorítmica (fairness) y sesgo, que corresponden a una dimensión ética distinta del problema de degradación; y (c) indicadores de seguridad y privacidad de los datos procesados por los servidores MCP.

**Delimitación Tecnológica**

El estudio se circunscribe al uso de modelos LLM con soporte nativo al Model Context Protocol en su versión 1.0 (Anthropic, 2024). El modelo base seleccionado para todos los experimentos es Claude Sonnet 4.5, utilizado a través de la API comercial de Anthropic con temperatura fija en 0.0 para garantizar la reproducibilidad de los resultados. La elección de un único modelo base es una decisión deliberada de control experimental: el objetivo del estudio es medir el efecto de las técnicas de memoria, no comparar modelos.

Los servidores MCP utilizados en el experimento serán seleccionados del registro público de servidores MCP (MCP Registry, 2025), priorizando aquellos que cubren tres dominios representativos: recuperación de información (search), ejecución de código y acceso a datos estructurados (bases de datos). Se utilizarán entre dos y cinco servidores MCP de forma simultánea por escenario de prueba, lo que cubre el rango de complejidad típico de los despliegues en producción reportados por la literatura.

La infraestructura de cómputo se limitará a instancias de cómputo en la nube disponibles con presupuesto de investigación de maestría. No se incluirán experimentos que requieran GPUs de alta gama para inferencia local de modelos, ni despliegues en clústeres de alta disponibilidad. Esta restricción es coherente con el enfoque de la investigación, centrado en técnicas de nivel de agente aplicables en entornos de uso de APIs de inferencia comerciales.

**Delimitación Espacial y Poblacional**

Dado que la investigación es de naturaleza experimental y los experimentos se ejecutan sobre infraestructura de cómputo en la nube, no existe una delimitación geográfica física en sentido estricto. Sin embargo, el estudio se desarrolla en el marco de una tesis de maestría de una institución peruana, y sus resultados tienen aplicación directa en el ecosistema de adopción de IA en el Perú.

La población de interés está constituida por los sistemas de agentes LLM conectados a múltiples servidores MCP en entornos de producción. Dado que no es posible acceder a los sistemas de producción de terceros para su instrumentación y medición, el estudio trabaja con una muestra experimental controlada: agentes implementados por el investigador, ejecutados sobre conjuntos de datos de prueba diseñados para simular conversaciones representativas de los casos de uso reales más frecuentes.

Los conjuntos de datos de prueba se construirán combinando datasets de referencia de la literatura ---LongMemEval (Truong & Ho, 2023), LoCoMo (Maharana et al., 2024) y SimpleToolHalluBench (Zeng et al., 2025)--- con escenarios adicionales diseñados específicamente para el contexto multi-MCP, lo que garantiza tanto la comparabilidad con estudios previos como la relevancia para el problema específico estudiado.

**Delimitación Temporal**

La investigación se enmarca en el período 2025--2026, correspondiente al ciclo de maestría del investigador. La revisión de literatura cubre publicaciones hasta abril de 2025, incluyendo preprints de relevancia directa disponibles en arXiv. No se incluirán publicaciones posteriores a esta fecha de corte, aunque podrán ser referenciadas en la discusión de resultados como contexto comparativo si su relevancia lo justifica.

El diseño experimental se ejecutará entre el tercer y cuarto trimestre de 2025, y el análisis de resultados y redacción de conclusiones se completará en el primer trimestre de 2026. Esta delimitación temporal es consistente con el estado actual de la especificación MCP (v1.0) y con la disponibilidad de los modelos y herramientas seleccionados para el experimento.

Cabe señalar que el campo de los agentes LLM y el protocolo MCP se encuentran en evolución acelerada: versiones futuras del estándar MCP, nuevos modelos de lenguaje o nuevas técnicas de memoria publicadas después del corte de literatura podrían alterar las condiciones del problema. La delimitación temporal es, por tanto, no solo una restricción operativa sino una condición de estabilidad del contexto tecnológico que garantiza la reproducibilidad del experimento.

**Síntesis de la Delimitación**

La Tabla 1 presenta una síntesis de las dimensiones de delimitación, especificando para cada una lo que está incluido y lo que queda expresamente excluido del alcance del estudio:

  ---------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------------------------------------------------
  **Dimensión**                **Incluido en el Estudio**                                                                                                                                   **Excluido Expresamente**
  **Temática**                 Context rot en multi-MCP; RAG semántico, SessionFacts, MemoryBank, semantic caching y tool gating; métricas de exactitud, alucinación, coherencia y tokens   Fine-tuning del modelo; atención modificada; compresión por destilación; equidad algorítmica; seguridad de datos
  **Tecnológica**              Claude Sonnet 4.5 vía API; MCP v1.0; 2--5 servidores MCP públicos en 3 dominios; infraestructura cloud de bajo costo                                         Modelos con inferencia local en GPU; arquitecturas multi-agente jerárquicas; versiones MCP posteriores a v1.0; APIs propietarias sin soporte MCP
  **Espacial / Poblacional**   Agentes LLM multi-MCP implementados experimentalmente; datasets LongMemEval, LoCoMo, SimpleToolHalluBench + escenarios multi-MCP diseñados ad hoc            Sistemas de producción de terceros; usuarios humanos reales; evaluación en entornos regulados (salud, finanzas, gobierno)
  **Temporal**                 Período 2025--2026; literatura hasta abril 2025; MCP v1.0 como versión de referencia                                                                         Publicaciones posteriores a abril 2025 (excepto referencia comparativa en discusión); versiones futuras del estándar MCP
  ---------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------------------------------------------------

> *Nota.* Síntesis de las cuatro dimensiones de delimitación del estudio. MCP = Model Context Protocol; RAG = Retrieval-Augmented Generation.

**Implicaciones de la Delimitación**

La delimitación establecida tiene implicaciones directas sobre la generalización de los resultados. Los hallazgos del estudio serán directamente aplicables a: (a) agentes LLM que utilizan APIs de inferencia comerciales con soporte MCP, que constituyen el caso de uso predominante en la industria; (b) arquitecturas de agentes con dos a cinco servidores MCP activos, que representan el rango de complejidad más frecuente en los despliegues documentados; y (c) conversaciones multi-turno de hasta 100 turnos, que cubren la mayoría de los casos de uso empresariales.

Los resultados deben interpretarse con cautela en contextos que involucren: (a) modelos LLM distintos de Claude Sonnet 4.5, ya que diferentes arquitecturas de transformer pueden exhibir patrones de degradación diferentes; (b) catálogos de herramientas de más de 100 herramientas MCP, que están fuera del rango experimental evaluado; y (c) dominios altamente especializados (medicina, derecho, finanzas) donde la exactitud de la información tiene consecuencias críticas y puede requerir métricas de evaluación específicas del dominio.

Esta delimitación es coherente con el principio de parsimonia científica: un estudio acotado con resultados sólidos y reproducibles aporta más valor al campo que un estudio de alcance amplio con evidencia débil. Los límites establecidos representan además oportunidades de extensión natural para investigaciones futuras, tal como se desarrolla en las limitaciones y trabajos futuros de la tesis.

**Referencias**

Anthropic. (2024). Model Context Protocol specification (v1.0). Anthropic. https://modelcontextprotocol.io/specification

Hernández Sampieri, R., Fernández Collado, C., & Baptista Lucio, P. (2014). Metodología de la investigación (6.ª ed.). McGraw-Hill Education.

Maharana, A., Lee, D.-H., Tulyakov, S., Bansal, M., Barbieri, F., & Fang, Y. (2024). Evaluating very long-term conversational memory of LLM agents. arXiv. https://arxiv.org/abs/2402.17753

MCP Registry. (2025). Public MCP server catalog. https://mcpregistry.dev

Tang, R., Jin, Z., Alexandrov, A., Shao, Y., Shi, P., & Pan, L. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. arXiv. https://arxiv.org/abs/2502.03415

Truong, T. H., & Ho, T. B. (2023). LongMemEval: Benchmarking long-context language models on long-term interactive memory. arXiv. https://arxiv.org/abs/2410.10813

Zeng, Z., Liu, M., Lu, R., Wang, B., Liu, X., & Cheng, X. (2025). SimpleToolHalluBench: Towards a comprehensive assessment of tool call hallucination in large language models. arXiv. https://arxiv.org/abs/2501.13395
