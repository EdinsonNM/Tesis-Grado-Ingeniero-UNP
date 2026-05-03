# DOC-05 — Introducción de la Tesis

> **Tipo:** Tesis — Capítulo I  
> **Descripción:** Introducción formal: contexto, motivación, alcance y estructura del documento.

---

**Medición del Impacto de Técnicas de Memoria y Gestión de Contexto sobre la Degradación de Respuestas en Agentes LLM Conectados a Múltiples Servidores MCP**

Edinson Núñez

\[Nombre de la Facultad / Escuela Profesional\]

\[Nombre de la Universidad\]

\[Nombre del Asesor / Director de Tesis\]

Abril 2026

**Resumen**

Los modelos de lenguaje de gran escala (LLM) conectados a herramientas externas a través del Model Context Protocol (MCP) enfrentan un fenómeno progresivo de degradación de la calidad de sus respuestas conocido como context rot, que se manifiesta como pérdida de precisión, incremento de alucinaciones y aumento del costo computacional conforme crece el número de herramientas y servidores conectados. La presente investigación tiene como objetivo medir empíricamente el impacto de distintas técnicas de memoria y control de contexto sobre esta degradación en agentes LLM bajo configuraciones de uno, tres y cinco o más servidores MCP. Se adopta un diseño cuantitativo experimental con tres fases progresivas, empleando como variables dependientes el costo de tokens de entrada y salida, la latencia de respuesta en percentiles p50 y p95, y la tasa de precisión de respuesta. Se contrastan cinco técnicas de mitigación documentadas en la literatura: tool gating, memoria de sesión compacta (SessionFacts), memoria longitudinal categorizada, recuperación federada por servidor y caching semántico. Los resultados permitirán generar un mapa empírico de la relación rendimiento-costo de cada técnica bajo condiciones controladas y replicables, aportando evidencia cuantitativa para el diseño de agentes LLM en producción.

***Palabras clave:** modelos de lenguaje de gran escala, Model Context Protocol, context rot, memoria en LLM, tool gating, degradación de contexto, recuperación aumentada*

**Abstract**

Large language models (LLMs) connected to external tools through the Model Context Protocol (MCP) experience a progressive phenomenon of response quality degradation known as context rot, which manifests as a loss of precision, increased hallucinations, and higher computational cost as the number of connected tools and servers grows. This research aims to empirically measure the impact of different memory and context management techniques on this degradation in LLM agents configured with one, three, and five or more MCP servers. A quantitative experimental design with three progressive phases is adopted, using as dependent variables the input and output token cost, response latency at p50 and p95 percentiles, and response accuracy rate. Five mitigation techniques documented in the literature are contrasted: tool gating, compact session memory (SessionFacts), categorized long-term memory, federated retrieval by server, and semantic caching. The results will generate an empirical performance-cost map for each technique under controlled and replicable conditions, providing quantitative evidence for the design of production-grade LLM agents.

***Keywords:** large language models, Model Context Protocol, context rot, LLM memory, tool gating, context degradation, retrieval-augmented generation*

**Introducción**

La inteligencia artificial generativa ha experimentado una transformación estructural en los últimos años: los modelos de lenguaje de gran escala (LLM) han dejado de operar como sistemas de respuesta autónoma para convertirse en el núcleo de agentes capaces de planificar, razonar y actuar sobre herramientas externas ([Yao et al., 2022](https://arxiv.org/abs/2210.03629)). Este cambio de paradigma amplía enormemente la utilidad práctica de los LLM, pero introduce simultáneamente un conjunto de desafíos técnicos que la investigación actual apenas comienza a caracterizar de forma sistemática.

El Model Context Protocol (MCP), publicado por Anthropic en noviembre de 2024, estandariza la forma en que los agentes LLM se conectan a fuentes de datos y herramientas externas a través de una arquitectura host-cliente-servidor ([Anthropic, 2024](https://modelcontextprotocol.io/specification/2025-11-25)). Su adopción ha sido rápida: en pocos meses, ecosistemas de desarrollo en todo el mundo comenzaron a publicar servidores MCP para calendarios, bases de datos, sistemas de gestión de proyectos, repositorios de código y docenas de servicios adicionales. Como resultado, es común encontrar agentes LLM conectados simultáneamente a cinco, diez o más servidores MCP, cada uno con su propio catálogo de herramientas y recursos.

Esta proliferación expone un problema técnico de creciente relevancia: la degradación progresiva de la calidad de las respuestas del agente conforme crece el número de herramientas y servidores en su contexto. [Gan y Sun (2025)](https://arxiv.org/abs/2505.03275) documentaron que los LLM fallan en seleccionar la herramienta correcta en el 86.4% de los casos cuando el catálogo supera cierto umbral, mientras que [Anthropic (2024)](https://modelcontextprotocol.io/specification/2025-11-25) reporta que las definiciones de herramientas pueden consumir decenas de miles de tokens antes de que el agente procese la consulta real. Este fenómeno, que en la literatura emergente se denomina context rot, constituye el objeto de estudio central de la presente investigación.

**El Problema de la Degradación Contextual**

El context rot no es un fenómeno de todo o nada: se manifiesta de forma gradual y a lo largo de tres dimensiones interdependientes. La primera es la sobrecarga de herramientas (tool overload): al exponer al modelo un catálogo completo de decenas o cientos de herramientas, la probabilidad de selección incorrecta, de invocación de herramientas inexistentes (alucinación de tools) o de bloqueo del plan de acción se incrementa de forma proporcional al tamaño del catálogo ([Zhang et al., 2024](https://arxiv.org/abs/2406.20015)). La segunda dimensión es la inflación del contexto por resultados intermedios: cada llamada a una herramienta devuelve datos que se acumulan en el contexto del modelo, incrementando el costo de procesamiento y diluyendo la señal relevante para la consulta actual ([LangChain, 2024](https://langchain-ai.github.io/langgraph/)). La tercera dimensión es la mezcla no estructurada de memorias: preferencias del usuario, hechos operacionales, resultados de herramientas y estado emocional se almacenan en la misma bolsa sin estructura, generando contradicciones y respuestas incoherentes entre sesiones ([Kirmayr et al., 2025](https://arxiv.org/abs/2501.09645); [Zhong et al., 2023](https://arxiv.org/abs/2305.10250)).

La literatura reciente ha comenzado a proponer soluciones para cada una de estas dimensiones de forma individual. [Gan y Sun (2025)](https://arxiv.org/abs/2505.03275) proponen aplicar recuperación semántica sobre el catálogo de herramientas antes de construir el prompt (RAG-MCP), logrando reducir el número de tokens del prompt en más del 50% y triplicar la precisión de selección de herramientas. [Chhikara et al. (2025)](https://arxiv.org/abs/2504.19413) presentan Mem0, una capa de memoria longitudinal que reduce la latencia en el percentil 95 en un 91% y el costo de tokens en más del 90% frente al baseline de contexto completo. [Kirmayr et al. (2025)](https://arxiv.org/abs/2501.09645) demuestran que acotar la memoria por categorías predefinidas reduce significativamente las contradicciones y redundancias en sistemas de asistencia personalizada. Sin embargo, ninguno de estos trabajos mide el impacto combinado de múltiples técnicas de forma integrada sobre un agente conectado a múltiples servidores MCP, ni lo hace con métricas económicas —costo de tokens y latencia— como variables primarias de medición.

**Justificación de la Investigación**

La justificación de esta investigación opera en tres niveles. A nivel teórico, el campo carece de un marco de referencia integrado que relacione el número de servidores MCP conectados con la magnitud de la degradación de respuestas y con la efectividad de las técnicas de mitigación disponibles. Los benchmarks existentes —LongMemEval ([Wu et al., 2024](https://arxiv.org/abs/2410.10813)), LoCoMo ([Maharana et al., 2024](https://arxiv.org/abs/2402.17753)) y ToolHaystack (2025)— miden aspectos específicos del problema pero no lo abordan en su dimensión multi-MCP completa ni incorporan métricas de costo como variables dependientes.

A nivel práctico, la degradación de respuestas en agentes LLM tiene consecuencias directas en la calidad de los sistemas de software que los incorporan: mayor latencia para el usuario final, mayor costo operativo para las organizaciones que los despliegan, y mayor riesgo de errores o información incorrecta en los resultados. En el contexto peruano y latinoamericano, donde la adopción de inteligencia artificial generativa en empresas y organismos del Estado se encuentra en una fase temprana pero de crecimiento acelerado, contar con evidencia empírica sobre el comportamiento de estas arquitecturas bajo condiciones controladas resulta de alto valor para la toma de decisiones de diseño e implementación.

A nivel metodológico, la investigación contribuye con un protocolo experimental reproducible que puede servir como referencia para futuras investigaciones sobre el tema, al definir de forma explícita las condiciones de prueba, los benchmarks utilizados, las métricas medidas y los procedimientos de análisis estadístico aplicados.

**Objetivos de la Investigación**

***Objetivo General***

Medir el impacto de distintas técnicas de memoria y gestión de contexto sobre la degradación de respuestas —expresada en costo de tokens, latencia de respuesta y precisión— en agentes LLM conectados a múltiples servidores MCP bajo condiciones experimentales controladas.

***Objetivos Específicos***

1.  Establecer una línea base de rendimiento (costo de tokens, latencia p50/p95 y precisión de respuesta) para un agente LLM sin conexión a servidores MCP.

2.  Medir la degradación progresiva de las métricas de rendimiento conforme se incrementa el número de servidores MCP conectados al agente (de uno a cinco o más servidores).

3.  Evaluar el impacto individual de cinco técnicas de mitigación —tool gating, memoria de sesión compacta, memoria longitudinal categorizada, recuperación federada y caching semántico— sobre las métricas de degradación medidas.

4.  Comparar la relación rendimiento-costo de cada técnica de mitigación para identificar cuáles ofrecen la mayor recuperación de precisión con el menor incremento de latencia y costo de tokens.

5.  Generar un protocolo experimental documentado y reproducible que permita a investigadores futuros extender o replicar los experimentos en distintos modelos LLM y configuraciones MCP.

**Hipótesis General**

La aplicación de técnicas de memoria estructurada y control de contexto —en particular el tool gating, la memoria de sesión compacta y la memoria longitudinal categorizada— reduce significativamente la degradación de respuestas (context rot) en agentes LLM conectados a múltiples servidores MCP, manifestada como una reducción estadísticamente significativa del costo de tokens, la latencia de respuesta y la tasa de error, en comparación con un agente LLM sin técnicas de mitigación aplicadas.

**Alcance y Delimitación**

La investigación se delimita al estudio experimental de agentes LLM basados en modelos con capacidad de function calling o tool use y soporte nativo o vía SDK al protocolo MCP. No se evalúan modelos de lenguaje especializados en dominios específicos (médico, legal o financiero) ni arquitecturas multimodales. El ámbito temático se circunscribe a las siguientes técnicas: tool gating con filtros semánticos (inspirado en RAG-MCP), memoria de sesión compacta (SessionFacts), memoria longitudinal categorizada (inspirada en CarMem y Mem0), recuperación federada por servidor (inspirada en FedRAG) y caching semántico (RedisVL). El período de experimentación comprende el año 2025 y el primer semestre de 2026.

Desde el punto de vista geográfico, los experimentos se ejecutan sobre infraestructura en la nube accesible desde el Perú, utilizando APIs de proveedores disponibles en la región. La investigación no se orienta a la construcción de un nuevo modelo LLM ni a la modificación de pesos neuronales; su foco es la arquitectura del sistema de agente que envuelve al modelo.

**Estructura del Documento**

La presente tesis se organiza en cinco capítulos. El Capítulo I presenta el planteamiento del problema, la formulación de las preguntas de investigación, la justificación, los objetivos, las hipótesis y la delimitación del estudio. El Capítulo II desarrolla el marco teórico, incluyendo los fundamentos de los LLM y la arquitectura transformer, el protocolo MCP, las técnicas de memoria para agentes, el fenómeno de degradación contextual y los frameworks de evaluación existentes. El Capítulo III describe la metodología: tipo y diseño de investigación, operacionalización de variables, protocolo experimental, instrumentos de medición y procedimientos estadísticos de análisis. El Capítulo IV presenta los resultados obtenidos, organizados por fase experimental. El Capítulo V discute los hallazgos, los contrasta con la literatura revisada, presenta las conclusiones y propone líneas de investigación futura.

**Referencias**

Anthropic. (2024). Model Context Protocol specification. Anthropic. [https://modelcontextprotocol.io/specification/2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25)

Chhikara, P., Singh, T., Yadav, D., Nie, N., & Doerr, T. (2025). Mem0: Building production-ready AI agents with scalable long-term memory. arXiv. [https://arxiv.org/abs/2504.19413](https://arxiv.org/abs/2504.19413)

Gan, T., & Sun, Q. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. arXiv. [https://arxiv.org/abs/2505.03275](https://arxiv.org/abs/2505.03275)

Kirmayr, J., Stappen, L., Schneider, P., Matthes, F., & André, E. (2025). CarMem: Enhancing long-term memory in LLM voice assistants through category-bounding. En Proceedings of the 31st International Conference on Computational Linguistics: Industry Track (pp. 350–365). Association for Computational Linguistics. [https://arxiv.org/abs/2501.09645](https://arxiv.org/abs/2501.09645)

LangChain. (2024). LangGraph: State management and agent orchestration \[Documentación técnica\]. LangChain Inc. [https://langchain-ai.github.io/langgraph/](https://langchain-ai.github.io/langgraph/)

Maharana, A., Lee, D.-H., Tulyakov, S., Bansal, M., Barbieri, F., & Fang, Y. (2024). Evaluating very long-term conversational memory of LLM agents. En Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics (pp. 13851–13870). ACL. [https://arxiv.org/abs/2402.17753](https://arxiv.org/abs/2402.17753)

Packer, C., Fang, V., Patil, S. G., Lin, K., Wooders, S., & Gonzalez, J. (2023). MemGPT: Towards LLMs as operating systems. arXiv. [https://arxiv.org/abs/2310.08560](https://arxiv.org/abs/2310.08560)

Wu, D., Wang, H., Yu, W., Zhang, Y., Chang, K.-W., & Yu, D. (2024). LongMemEval: Benchmarking chat assistants on long-term interactive memory. arXiv. [https://arxiv.org/abs/2410.10813](https://arxiv.org/abs/2410.10813)

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. arXiv. [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)

Zhang, Y., et al. (2024). ToolBeHonest: A multi-level hallucination diagnostic benchmark for tool-augmented large language models. arXiv. [https://arxiv.org/abs/2406.20015](https://arxiv.org/abs/2406.20015)

Zhong, W., Guo, L., Gao, Q., Ye, H., & Wang, Y. (2023). MemoryBank: Enhancing large language models with long-term memory. arXiv. [https://arxiv.org/abs/2305.10250](https://arxiv.org/abs/2305.10250)
