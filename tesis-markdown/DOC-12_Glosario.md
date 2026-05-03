# DOC-12 — Glosario de Términos

> **Tipo:** Tesis — Capítulo II  
> **Descripción:** Definiciones formales de todos los términos técnicos del dominio.

---

Medición del Impacto de Técnicas de Memoria y Gestión de Contexto

sobre la Degradación de Respuestas en Agentes LLM

Conectados a Múltiples Servidores MCP

**DOC-12: Glosario de Términos**

Edinson Núñez

Tesis de Maestría

2026

**Glosario de Términos**

El presente glosario reúne las definiciones operacionales de los términos técnicos, siglas y conceptos especializados utilizados en el desarrollo de la tesis. Las definiciones son específicas al contexto del estudio —agentes LLM, Model Context Protocol y técnicas de memoria— y se han construido a partir de las fuentes primarias citadas en el marco teórico (DOC-11). Para cada término se indica la referencia de la fuente cuando la definición deriva directamente de un trabajo publicado; en caso contrario, la definición es original y consistente con el uso establecido en la literatura del campo.

Los términos están ordenados alfabéticamente. Las siglas en español e inglés se incluyen como entradas propias con remisión al término completo correspondiente. El glosario cubre 45 términos distribuidos en 13 letras del alfabeto.

**A**

**Agente LLM**. Sistema de software que utiliza un modelo de lenguaje de gran escala como motor de razonamiento y lo combina con la capacidad de ejecutar acciones en el entorno —llamadas a herramientas, búsquedas, ejecución de código— mediante ciclos iterativos de razonamiento, acción y observación, con el objetivo de completar tareas que van más allá de la generación de texto estático. *([Wang et al., 2024](#ref-wang2024))*

**Alucinación de herramienta**. Error de un agente LLM que consiste en invocar una herramienta inexistente en el catálogo disponible, especificar parámetros incorrectos para una herramienta existente, o proporcionar valores de parámetros inválidos o fuera del rango aceptado. Es una manifestación específica del fenómeno general de alucinación de los LLM en el contexto del uso de herramientas. *([Zeng et al., 2025](#ref-zeng2025))*

**Atención multi-cabezal *(MHA)***. Mecanismo central de la arquitectura transformer que calcula, para cada token en la secuencia de entrada, un vector de contexto ponderado por la relevancia de todos los demás tokens mediante múltiples cabezales de atención paralelos. Permite al modelo capturar relaciones sintácticas y semánticas a diferentes niveles de abstracción simultáneamente. *([Vaswani et al., 2017](#ref-vaswani2017))*

**B**

**Benchmark de evaluación**. Conjunto estandarizado de tareas, datos de prueba y métricas de evaluación diseñado para medir y comparar el rendimiento de sistemas de inteligencia artificial de forma reproducible y comparable entre estudios. En el contexto de esta tesis, los benchmarks de referencia son LongMemEval, LoCoMo y SimpleToolHalluBench.

**BERTScore**. Métrica de evaluación de generación de texto que mide la similitud semántica entre dos enunciados utilizando representaciones contextuales de embeddings generadas por modelos BERT. Calcula la similitud coseno entre los embeddings de los tokens de la hipótesis y los de la referencia, produciendo puntuaciones de precisión, cobertura y F1 semánticas. *([Zhang et al., 2020](#ref-zhang2020))*

**C**

**Caching semántico**. Técnica de optimización que almacena pares (consulta, respuesta) y los recupera cuando una nueva consulta es semánticamente equivalente a una almacenada, determinando la equivalencia mediante similitud coseno entre vectores de embeddings en lugar de coincidencia textual exacta. Reduce el número de invocaciones de inferencia del modelo para consultas similares. *(Redis Labs, 2025)*

**Coherencia conversacional**. Propiedad de un agente LLM que denota la consistencia interna de sus respuestas a lo largo de una conversación extendida, incluyendo la consistencia de afirmaciones factuales entre turnos, la continuidad lógica del razonamiento y la ausencia de contradicciones con información proporcionada o generada anteriormente en la sesión.

**Context rot**. Proceso de degradación progresiva y acumulativa de la calidad de las respuestas de un agente LLM, medida a través de métricas cuantificables, como consecuencia del crecimiento del contexto activo en conversaciones multi-turno. En arquitecturas multi-MCP, el context rot es exacerbado por los mecanismos de tool overload, acumulación de resultados intermedios y mezcla de estados de sesión. Término adoptado de la práctica industrial. *(Chroma Research, 2025)*

**Contexto activo**. Conjunto de tokens que el modelo de lenguaje procesa en una inferencia determinada, incluyendo el prompt del sistema, el historial de conversación, los resultados de herramientas previas y las descripciones de las herramientas disponibles. El tamaño del contexto activo está limitado por la ventana de contexto del modelo.

**D**

**Degradación de respuestas**. Reducción cuantificable en uno o más indicadores de calidad de las respuestas de un agente LLM a medida que avanza una conversación, incluyendo disminución de la exactitud factual, incremento de la tasa de alucinación, reducción de la coherencia conversacional o aumento del consumo de tokens por turno. Sinónimo operacional de context rot en el contexto de esta tesis.

**Diseño factorial 2k**. Diseño experimental estadístico que evalúa los efectos de k factores binarios (presencia/ausencia de cada técnica) y sus interacciones sobre una variable de respuesta. Permite estimar con eficiencia los efectos principales e interacciones de segundo orden usando 2k combinaciones de tratamiento. En esta tesis se aplica en forma reducida (diseño fraccionado) para evaluar combinaciones de técnicas de memoria. *([Montgomery, 2017](#ref-montgomery2017))*

**E**

**Embeddings**. Representaciones vectoriales densas de elementos discretos —palabras, tokens, documentos, herramientas— en un espacio continuo de alta dimensión, generadas mediante redes neuronales entrenadas para capturar relaciones semánticas. Dos elementos con significados similares tienen embeddings con alta similitud coseno. Fundamentales para la recuperación semántica en sistemas RAG y semantic caching.

**Exactitud de respuesta**. Proporción de afirmaciones verificables en las respuestas de un agente LLM que son correctas respecto a un conjunto de ground truth anotado. Métrica primaria de calidad en los experimentos de esta tesis, medida mediante comparación automatizada contra respuestas de referencia validadas.

**F**

**Filtrado semántico**. Estrategia de selección de herramientas MCP que compara la representación vectorial de la consulta del usuario con los embeddings de las descripciones de las herramientas disponibles y expone al modelo solo aquellas cuya similitud coseno supera un umbral configurable. Componente central de las estrategias de tool gating. *([Tang et al., 2025](#ref-tang2025))*

**Fine-tuning**. Proceso de ajuste de los parámetros de un modelo de lenguaje pre-entrenado mediante entrenamiento adicional sobre un conjunto de datos específico del dominio o tarea objetivo. Permite especializar las capacidades del modelo sin entrenarlo desde cero. Excluido del alcance de esta tesis por requerir acceso a los pesos del modelo.

**G**

**Ground truth**. Conjunto de respuestas correctas validadas manualmente o mediante procedimientos automáticos verificables, utilizado como referencia para medir la exactitud de las respuestas generadas por el agente LLM. En esta tesis, el ground truth se construye a partir de los datasets de benchmarks de referencia complementados con escenarios multi-MCP diseñados ad hoc.

**H**

**Historial de conversación**. Secuencia ordenada de turnos de interacción entre el usuario y el agente LLM, incluyendo las entradas del usuario, los pensamientos del agente, las llamadas a herramientas, los resultados de herramientas y las respuestas generadas. En la implementación estándar sin técnicas de memoria, el historial completo se concatena al contexto activo en cada turno, siendo la principal fuente de crecimiento del contexto.

**I**

**Inferencia**. Proceso mediante el cual un modelo de lenguaje genera una respuesta a partir de un prompt de entrada. En el contexto de APIs comerciales, la inferencia se realiza en los servidores del proveedor del modelo y su costo se mide en tokens procesados. El tiempo desde el envío del prompt hasta la recepción del primer token de respuesta se denomina latencia de primer token (TTFT).

**L**

**Latencia de primer token *(TTFT)***. Tiempo transcurrido entre el envío de la solicitud de inferencia y la recepción del primer token de la respuesta generada por el modelo. Métrica de eficiencia computacional relevante para sistemas de agentes en producción, ya que determina la percepción de velocidad del sistema por parte del usuario.

**LLM**. Véase Modelo de Lenguaje de Gran Escala.

**LoCoMo**. Benchmark de evaluación de agentes LLM en conversaciones largas y multi-sesión que evalúa la coherencia, consistencia y capacidad de actualización de creencias del agente ante nueva información. Utilizado en esta tesis para medir el impacto de las técnicas de memoria sobre la coherencia conversacional. *([Maharana et al., 2024](#ref-maharana2024))*

**LongMemEval**. Benchmark de evaluación de la memoria a largo plazo de agentes LLM en conversaciones de hasta 500 turnos. Evalúa cinco capacidades de memoria: recuperación de información única, razonamiento multi-hop, seguimiento de entidades, razonamiento temporal y detección de ausencia de información. Utilizado en esta tesis como dataset base para los experimentos de degradación. *([Truong & Ho, 2023](#ref-truong2023))*

**M**

**Marco ReAct**. Framework de operación de agentes LLM que intercala la generación de pensamientos de razonamiento con la ejecución de acciones sobre herramientas externas, siguiendo el ciclo: razonar → actuar → observar → razonar. Cada ciclo acumula tokens en el contexto del agente, siendo la arquitectura subyacente estándar en los sistemas de agentes LLM modernos. *([Yao et al., 2022](#ref-yao2022))*

**MCP**. Véase Model Context Protocol.

**Mecanismo de atención**. Componente central de la arquitectura transformer que calcula, para cada token en una secuencia, un vector de representación ponderado por la relevancia de todos los demás tokens. Permite al modelo modelar dependencias a larga distancia sin la degradación de gradiente de las redes recurrentes. La calidad de la atención decrece para tokens ubicados en el centro de contextos muy largos. *([Vaswani et al., 2017](#ref-vaswani2017))*

**Mem0**. Sistema de memoria adaptativa para agentes LLM que combina recuperación vectorial con grafos de conocimiento para gestionar memorias de usuario, agente y sesión de forma diferenciada. Diseñado para entornos de producción con múltiples usuarios y sesiones concurrentes. *([Chhikara et al., 2025](#ref-chhikara2025))*

**MemGPT / Letta**. Sistema de gestión de memoria para agentes LLM que simula el comportamiento de un sistema operativo, con memoria principal (contexto activo) y memoria secundaria (almacenamiento externo). Implementa técnicas de paginación de memoria para superar la limitación de la ventana de contexto y fue el precursor del concepto de SessionFacts. *([Packer et al., 2023](#ref-packer2023))*

**MemoryBank**. Sistema de memoria a largo plazo para agentes LLM que combina almacenamiento externo indexado con una política de olvido inspirada en la curva de Ebbinghaus de la psicología cognitiva. Las memorias almacenadas decaen en relevancia con el tiempo transcurrido desde su última recuperación, evitando la acumulación de información obsoleta. *([Hu et al., 2023](#ref-hu2023))*

**Model Context Protocol *(MCP)***. Estándar abierto publicado por Anthropic en noviembre de 2024 para la integración de agentes LLM con herramientas y fuentes de datos externas mediante una interfaz cliente-servidor estandarizada. Define los mecanismos de inicialización de sesión, descubrimiento de herramientas, invocación y notificación de cambios en el catálogo, siendo el protocolo de integración de herramientas de referencia para la investigación. *([Anthropic, 2024](#ref-anthropic2024))*

**Modelo de lenguaje de gran escala *(LLM)***. Sistema de inteligencia artificial basado en la arquitectura transformer, entrenado sobre vastos corpus de texto mediante el objetivo de predicción del siguiente token. Opera dentro de una ventana de contexto limitada que define el número máximo de tokens que puede procesar en una inferencia. Los LLM modernos exhiben capacidades emergentes de razonamiento, uso de herramientas y seguimiento de instrucciones complejas. *([Brown et al., 2020](#ref-brown2020))*

**N**

**Next-token prediction**. Objetivo de entrenamiento de los modelos de lenguaje autoregresivos que consiste en predecir el token siguiente en una secuencia dado el contexto de todos los tokens anteriores. Es la tarea de pre-entrenamiento de los LLM como GPT, Llama, Gemini y Claude. La capacidad de razonamiento y las capacidades emergentes de los LLM son consecuencias del escalado de este objetivo simple.

**O**

**Overhead de contexto**. Tokens del contexto activo del agente que no contienen información directamente útil para la tarea actual, pero que son transmitidos al modelo en cada inferencia porque forman parte del historial o del catálogo de herramientas. El overhead incluye las descripciones de herramientas no relevantes, resultados de herramientas de turnos pasados y metadatos de servidores MCP.

**P**

**Puntos de cambio**. Ubicaciones en una serie temporal donde las propiedades estadísticas de la serie —media, varianza, tendencia— cambian de forma abrupta. En esta tesis, los puntos de cambio en las métricas de calidad de respuesta identifican los umbrales de longitud de contexto a partir de los cuales el context rot se vuelve estadísticamente significativo. Se detectan mediante algoritmos PELT y Binary Segmentation.

**R**

**RAG**. Véase Retrieval-Augmented Generation.

**RAG-MCP**. Extensión de RAG aplicada específicamente al catálogo de herramientas MCP, que utiliza recuperación semántica para exponer al modelo solo las herramientas más relevantes para cada consulta, en lugar de el catálogo completo. Reduce el overhead de tokens de descripción de herramientas sin sacrificar significativamente la exactitud de selección. *([Tang et al., 2025](#ref-tang2025))*

**Retrieval-Augmented Generation *(RAG)***. Técnica de gestión de memoria externa que combina un modelo de recuperación densa —que busca documentos o fragmentos relevantes en una base de datos vectorial mediante similitud coseno entre embeddings— con el modelo de generación, que utiliza los elementos recuperados como contexto adicional para producir la respuesta. Mitiga el context rot al sustituir el historial completo de conversación por los fragmentos más relevantes recuperados dinámicamente. *([Lewis et al., 2020](#ref-lewis2020))*

**S**

**Semantic caching**. Véase Caching semántico.

**Servidor MCP**. Componente del protocolo MCP que expone un catálogo de herramientas, recursos y prompts mediante una interfaz estandarizada JSON accesible por cualquier cliente MCP compatible. En las arquitecturas estudiadas en esta tesis, múltiples servidores MCP de diferentes dominios se conectan simultáneamente al mismo agente LLM, creando el contexto multi-servidor que es el objeto de estudio. *([Anthropic, 2024](#ref-anthropic2024))*

**SessionFacts**. Mecanismo de compresión del estado de sesión de un agente LLM que extrae y almacena los hechos, entidades y restricciones más relevantes del historial de conversación en una estructura compacta de pares clave-valor, sustituyendo el historial completo por este resumen en el contexto activo del agente. Reduce significativamente el consumo de tokens de historial en conversaciones largas. *([Packer et al., 2023](#ref-packer2023))*

**Similitud coseno**. Medida de similitud entre dos vectores que calcula el coseno del ángulo entre ellos, con valores en el rango \[-1, 1\] donde 1 indica vectores idénticos en dirección y -1 indica vectores opuestos. Utilizada como función de distancia en los sistemas de recuperación vectorial y filtrado semántico de esta tesis por su robustez ante diferencias de magnitud entre vectores.

**SimpleToolHalluBench**. Benchmark de evaluación de alucinaciones en el uso de herramientas que mide la tasa de alucinación de nombres de herramientas, parámetros y valores en catálogos de diferentes tamaños. Diseñado para evaluar específicamente el impacto del tool overload sobre la precisión del agente en la invocación de herramientas. *([Zeng et al., 2025](#ref-zeng2025))*

**T**

**Tasa de alucinación**. Proporción de afirmaciones verificables en las respuestas de un agente LLM que son incorrectas o no fundamentadas en la información disponible en el contexto. Métrica primaria de confiabilidad del sistema, cuyo incremento es uno de los indicadores más claros del fenómeno de context rot. Se mide mediante verificación cruzada automatizada contra el ground truth.

**Token**. Unidad mínima de procesamiento de los modelos de lenguaje, obtenida mediante un algoritmo de tokenización (comúnmente BPE o WordPiece) que divide el texto en subpalabras. En inglés, un token corresponde aproximadamente a 0.75 palabras; en español, la relación es ligeramente inferior debido a la mayor longitud media de las palabras. El costo de inferencia de las APIs de LLM se factura en función del número de tokens procesados.

**Tool gating**. Conjunto de estrategias que controlan qué herramientas del catálogo MCP se exponen al modelo en cada turno de la conversación, en lugar de exponer el catálogo completo de forma estática. Incluye el filtrado semántico por relevancia y la carga diferida de herramientas. Mitiga el mecanismo de tool overload del context rot.

**Tool overload**. Mecanismo de context rot que ocurre cuando el número de herramientas expuestas al modelo supera su capacidad de atención efectiva, resultando en degradación de la tasa de selección correcta de herramientas e incremento de la tasa de alucinación de parámetros. Se intensifica en arquitecturas multi-MCP donde cada servidor contribuye con su propio catálogo al contexto compartido. *([Tang et al., 2025](#ref-tang2025))*

**Transformer**. Arquitectura de red neuronal introducida por [Vaswani et al. (2017)](#ref-vaswani2017) basada en el mecanismo de atención multi-cabezal, que reemplazó a las redes recurrentes para el procesamiento de secuencias de texto. Es la arquitectura subyacente de todos los LLM modernos y determina las propiedades de la ventana de contexto y el mecanismo de atención que condicionan el fenómeno de context rot. *([Vaswani et al., 2017](#ref-vaswani2017))*

**V**

**Variable dependiente**. En el diseño experimental de esta tesis, el nivel de degradación de respuestas (context rot) medido a través del Índice de Calidad de Respuesta Compuesto (IQCR), que integra exactitud de respuesta, tasa de alucinación, coherencia conversacional y consumo de tokens por turno.

**Variable independiente**. En el diseño experimental de esta tesis, el tipo y combinación de técnicas de memoria y gestión de contexto aplicadas al agente LLM, operacionalizada en cinco niveles de tratamiento: sin técnica (baseline), RAG semántico, SessionFacts, tool gating y combinación óptima.

**Ventana de contexto**. Número máximo de tokens que un modelo de lenguaje puede procesar en una sola inferencia, definido por la arquitectura del modelo. Incluye todos los tokens del prompt de entrada y de la respuesta generada. Los LLM modernos tienen ventanas de contexto de 128,000 a 1,000,000 de tokens, aunque la calidad de la atención sobre tokens en posiciones centrales decrece con el tamaño del contexto.

**Í**

**Índice de calidad de respuesta compuesto *(IQCR)***. Métrica agregada diseñada para esta tesis que integra las cuatro dimensiones primarias de evaluación —exactitud de respuesta, tasa de alucinación, coherencia conversacional y consumo de tokens— mediante una ponderación definida por el método AHP. El IQCR permite comparar el desempeño global de diferentes técnicas de memoria en una única dimensión cuantitativa normalizada.

**Referencias**

<a id="ref-anthropic2024"></a>
Anthropic. (2024). Model Context Protocol specification (v1.0). Anthropic. [https://modelcontextprotocol.io/specification](https://modelcontextprotocol.io/specification)

<a id="ref-brown2020"></a>
Brown, T. B., Mann, B., Ryder, N., Subbiah, M., Kaplan, J., Dhariwal, P., Neelakantan, A., Shyam, P., Sastry, G., Askell, A., Agarwal, S., Herbert-Voss, A., Krueger, G., Henighan, T., Child, R., Ramesh, A., Ziegler, D. M., Wu, J., Winter, C., … Amodei, D. (2020). Language models are few-shot learners. Advances in Neural Information Processing Systems, 33, 1877–1901. [https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html](https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html)

<a id="ref-chhikara2025"></a>
Chhikara, P., Singh, D., Gupta, T., Goyal, A., & Tiwari, A. (2025). Mem0: Building production-ready AI agents with scalable long-term memory. arXiv. [https://arxiv.org/abs/2504.19413](https://arxiv.org/abs/2504.19413)

<a id="ref-chroma2025"></a>
Chroma Research. (2025). Context rot in production LLM systems: A benchmark study. Chroma. [https://www.trychroma.com/blog/context-rot](https://www.trychroma.com/blog/context-rot)

<a id="ref-hu2023"></a>
Hu, J., Huang, S., Luo, Y., Wu, F., & Lam, W. (2023). MemoryBank: Enhancing large language models with long-term memory. arXiv. [https://arxiv.org/abs/2305.10250](https://arxiv.org/abs/2305.10250)

<a id="ref-lewis2020"></a>
Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. Advances in Neural Information Processing Systems, 33, 9459–9474. [https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html](https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html)

<a id="ref-maharana2024"></a>
Maharana, A., Lee, D.-H., Tulyakov, S., Bansal, M., Barbieri, F., & Fang, Y. (2024). Evaluating very long-term conversational memory of LLM agents. arXiv. [https://arxiv.org/abs/2402.17753](https://arxiv.org/abs/2402.17753)

<a id="ref-montgomery2017"></a>
Montgomery, D. C. (2017). Design and analysis of experiments (9.ª ed.). Wiley.

<a id="ref-packer2023"></a>
Packer, C., Wooders, S., Lin, K., Fang, V., Patil, S. G., Stoica, I., & Gonzalez, J. E. (2023). MemGPT: Towards LLMs as operating systems. arXiv. [https://arxiv.org/abs/2310.08560](https://arxiv.org/abs/2310.08560)

<a id="ref-redis2025"></a>
Redis Labs. (2025). Enterprise AI deployment patterns: Token consumption and memory management. Redis. [https://redis.io/blog/enterprise-ai-memory-2025](https://redis.io/blog/enterprise-ai-memory-2025)

<a id="ref-tang2025"></a>
Tang, R., Jin, Z., Alexandrov, A., Shao, Y., Shi, P., & Pan, L. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. arXiv. [https://arxiv.org/abs/2502.03415](https://arxiv.org/abs/2502.03415)

<a id="ref-truong2023"></a>
Truong, T. H., & Ho, T. B. (2023). LongMemEval: Benchmarking long-context language models on long-term interactive memory. arXiv. [https://arxiv.org/abs/2410.10813](https://arxiv.org/abs/2410.10813)

<a id="ref-vaswani2017"></a>
Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is all you need. Advances in Neural Information Processing Systems, 30. [https://proceedings.neurips.cc/paper\_files/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html](https://proceedings.neurips.cc/paper\_files/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html)

<a id="ref-wang2024"></a>
Wang, L., Ma, C., Feng, X., Zhang, Z., Yang, H., Zhang, J., Chen, Z., Tang, J., Chen, X., Lin, Y., Zhao, W. X., Wei, Z., & Wen, J.-R. (2024). A survey on large language model based autonomous agents. Frontiers of Computer Science, 18(6), 186345. [https://doi.org/10.1007/s11704-024-40231-1](https://doi.org/10.1007/s11704-024-40231-1)

<a id="ref-yao2022"></a>
Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. arXiv. [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)

<a id="ref-zeng2025"></a>
Zeng, Z., Liu, M., Lu, R., Wang, B., Liu, X., & Cheng, X. (2025). SimpleToolHalluBench: Towards a comprehensive assessment of tool call hallucination in large language models. arXiv. [https://arxiv.org/abs/2501.13395](https://arxiv.org/abs/2501.13395)

<a id="ref-zhang2020"></a>
Zhang, T., Kishore, V., Wu, F., Weinberger, K. Q., & Artzi, Y. (2020). BERTScore: Evaluating text generation with BERT. International Conference on Learning Representations. [https://openreview.net/forum?id=SkeHuCVFDr](https://openreview.net/forum?id=SkeHuCVFDr)
