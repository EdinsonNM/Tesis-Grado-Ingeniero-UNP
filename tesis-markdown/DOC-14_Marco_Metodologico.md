# DOC-14 — Marco Metodológico

> **Tipo:** Tesis — Capítulo III  
> **Descripción:** Diseño experimental: tipo de estudio, variables, protocolo, diseño factorial 2^k e instrumentos.

---

Medición del Impacto de Técnicas de Memoria y Gestión de Contexto

sobre la Degradación de Respuestas en Agentes LLM

Conectados a Múltiples Servidores MCP

**DOC-14: Marco Metodológico**

Edinson Núñez

Tesis de Maestría

2026

**Marco Metodológico**

El marco metodológico define las decisiones epistemológicas, el diseño experimental y los procedimientos operativos que rigen la ejecución del estudio. En este capítulo se justifican el enfoque, el diseño, el nivel y el tipo de investigación; se caracteriza la unidad de análisis; se detallan los métodos y procedimientos de recolección y análisis de datos; se describen las técnicas e instrumentos utilizados; y se enuncian los principios éticos que guían el trabajo. Cada sección está directamente articulada con los objetivos, las hipótesis y la delimitación establecidos en los documentos anteriores.

**3.1 Enfoque de Investigación**

La investigación adopta un enfoque cuantitativo. Según Hernández Sampieri et al. (2014), el enfoque cuantitativo se caracteriza por la medición numérica de fenómenos, el uso de análisis estadístico y el contraste de hipótesis mediante procedimientos replicables. Este enfoque es el más apropiado para el problema estudiado porque: (a) las variables dependientes del estudio —exactitud de respuesta, tasa de alucinación, consumo de tokens, coherencia conversacional— son inherentemente numéricas y mensurables con instrumentos objetivos; (b) el objetivo central es establecer relaciones causales entre las técnicas de memoria y la calidad de respuesta, lo que requiere control experimental y pruebas de significancia estadística; y (c) los resultados deben ser reproducibles por otros investigadores con las mismas condiciones experimentales.

El enfoque cuantitativo no excluye la interpretación cualitativa de los patrones observados en los datos. En la fase de discusión de resultados se recurrirá a análisis interpretativo para contextualizar los hallazgos numéricos en el marco de la práctica de ingeniería de sistemas agentes. Sin embargo, la recolección de datos y la verificación de hipótesis se realizarán exclusivamente mediante procedimientos cuantitativos.

**3.2 Diseño de la Investigación**

El diseño de la investigación es experimental puro con grupos de control y tratamiento, medición pre y post intervención, y asignación controlada de condiciones experimentales. El diseño experimental es el más adecuado para establecer relaciones causales entre la variable independiente (técnicas de memoria) y la variable dependiente (nivel de context rot), ya que permite controlar las variables confusoras mediante la estandarización de las condiciones de prueba (Shadish et al., 2002).

La estructura experimental contempla seis grupos de tratamiento: un grupo de control sin técnicas de memoria (baseline) y cinco grupos de tratamiento con distintas configuraciones de técnicas. Todos los grupos son expuestos a los mismos escenarios de conversación y al mismo conjunto de datos de prueba, garantizando que las diferencias observadas en las métricas de calidad sean atribuibles exclusivamente a la variable independiente.

Se adopta adicionalmente un diseño de medidas repetidas en la dimensión temporal: las métricas se registran en cada turno de la conversación, lo que permite modelar la trayectoria de degradación y no solo el valor terminal. Este diseño longitudinal dentro de cada sesión experimental es lo que hace posible la detección de puntos de cambio (hipótesis HE5) y el análisis de la velocidad de degradación como variable dependiente secundaria.

Para el análisis de técnicas combinadas (hipótesis HE4) se utiliza un diseño factorial 2k reducido (diseño fraccionado de resolución IV), con k = 4 factores binarios correspondientes a las cuatro técnicas individuales evaluadas en HE2 más la técnica de tool gating evaluada en HE3. La resolución IV garantiza que los efectos principales no están confundidos con interacciones de dos factores, lo que permite estimar las sinergias más relevantes (Montgomery, 2017).

**3.3 Nivel de Investigación**

El nivel de investigación es explicativo-causal. La investigación no se limita a describir el fenómeno de context rot ni a correlacionar variables, sino que busca establecer la relación causal entre la aplicación de técnicas de memoria y la reducción de la degradación de respuestas mediante un diseño experimental con control activo de las condiciones. Este nivel es coherente con el estado del arte del campo: la existencia del fenómeno de context rot ha sido documentada descriptivamente (Liu et al., 2023; Chroma Research, 2025), y el paso necesario es la explicación causal de qué técnicas lo mitigan y en qué magnitud.

Adicionalmente, la investigación tiene una dimensión exploratoria en la detección de umbrales de degradación (hipótesis HE5): dado que no existen estudios previos que hayan caracterizado los puntos de cambio del context rot en arquitecturas multi-MCP, los análisis de segmentación de series temporales producirán hallazgos nuevos cuya interpretación requerirá razonamiento exploratorio. Esta dimensión exploratoria es secundaria respecto al nivel explicativo dominante.

**3.4 Tipo de Investigación**

La investigación es de tipo aplicada. Según Hernández Sampieri et al. (2014), la investigación aplicada busca resolver problemas prácticos utilizando el conocimiento generado por la investigación básica. En este caso, el conocimiento teórico sobre ventanas de contexto de LLM, arquitecturas de agentes y técnicas de memoria se aplica para resolver el problema práctico de la degradación de respuestas en sistemas de producción.

Los resultados de la investigación tienen aplicación directa en el diseño de sistemas agentes LLM en producción: las recomendaciones sobre qué técnicas implementar, bajo qué condiciones y con qué configuraciones serán directamente utilizables por ingenieros de sistemas sin necesidad de adaptación teórica intermedia. Esta orientación práctica no compromete el rigor metodológico del diseño experimental, sino que orienta la selección de los escenarios de prueba y los criterios de relevancia práctica de los hallazgos.

**3.5 Sujetos de la Investigación**

**Unidad de Análisis**

La unidad de análisis es el turno de conversación de un agente LLM conectado a múltiples servidores MCP en una sesión experimental controlada. Cada turno se caracteriza por: (a) un identificador de sesión; (b) el número de turno dentro de la sesión; (c) la consulta del usuario; (d) la respuesta generada por el agente; (e) las métricas de calidad registradas (exactitud, alucinación, coherencia, tokens); y (f) la configuración experimental (técnica de memoria activa, número de servidores MCP, longitud de contexto acumulado).

**Población y Muestra**

La población teórica del estudio es el conjunto de todos los turnos de conversación posibles en agentes LLM multi-MCP bajo las condiciones definidas en la delimitación. Dado que esta población es infinita (depende de las consultas que los usuarios podrían hacer), el estudio opera con una muestra experimental intencional diseñada para ser representativa de los patrones de uso más frecuentes.

La muestra está compuesta por conversaciones sintéticas construidas a partir de tres fuentes: (a) el dataset LongMemEval (Truong & Ho, 2023), del que se seleccionarán 100 conversaciones de referencia adaptadas al contexto multi-MCP; (b) el dataset LoCoMo (Maharana et al., 2024), del que se seleccionarán 50 conversaciones centradas en coherencia conversacional; y (c) escenarios multi-MCP diseñados ad hoc para cubrir tres dominios de herramientas (búsqueda de información, ejecución de código y consulta de datos estructurados), con 50 conversaciones adicionales.

El tamaño muestral total es de 200 conversaciones por grupo de tratamiento, con un mínimo de 30 turnos por conversación (llegando hasta 100 turnos en los escenarios de mayor longitud). El cálculo de potencia estadística (G\*Power 3.1, Faul et al., 2007) con efecto medio d = 0.5, α = 0.05 y potencia 1-β = 0.80 indica un tamaño mínimo de n = 34 por grupo para pruebas t de dos muestras independientes. La muestra de 200 conversaciones por grupo supera ampliamente este mínimo, garantizando potencia suficiente incluso para efectos pequeños (d = 0.2) en análisis secundarios.

**Agente LLM Experimental**

El agente LLM utilizado en todos los grupos experimentales es Claude Sonnet 4.5 (Anthropic, 2024), accedido mediante la API oficial de Anthropic con temperatura = 0.0 para garantizar reproducibilidad. La elección de un único modelo base es una decisión de control experimental: el objetivo es medir el efecto de las técnicas de memoria, no comparar modelos. La temperatura = 0.0 elimina la aleatoriedad en la generación, haciendo que cada experimento sea determinístico y replicable. Los servidores MCP utilizados se seleccionarán del registro público MCP Registry (2025) en los dominios de búsqueda web, ejecución de código Python y consulta de bases de datos SQL.

**3.6 Métodos y Procedimientos**

**Fase 1: Preparación del Entorno Experimental**

La primera fase comprende la construcción de la infraestructura experimental. Las actividades incluyen: (a) implementación del agente base (sin técnicas de memoria) con soporte MCP sobre el SDK oficial de Anthropic; (b) configuración y validación de los tres servidores MCP seleccionados para el experimento; (c) implementación de los módulos de cada técnica de memoria (RAG con ChromaDB, SessionFacts mediante extracción periódica de hechos, MemoryBank con política de olvido Ebbinghaus, semantic caching con RedisVL, filtrado semántico para tool gating); (d) construcción del módulo de evaluación automatizado (exactitud vs. ground truth, verificación de alucinaciones, BERTScore para coherencia, contador de tokens vía API); y (e) validación del conjunto de datos de prueba mediante prueba piloto con 20 conversaciones.

**Fase 2: Establecimiento de la Línea Base**

En la segunda fase se ejecuta el grupo de control (agente sin técnicas de memoria) sobre el conjunto completo de 200 conversaciones de prueba en las tres configuraciones de servidores MCP (2, 3 y 5 servidores activos). Para cada conversación se registran las métricas de calidad en cada turno, generando series temporales de 30, 50 y 100 puntos según la longitud de la conversación. Los resultados de esta fase establecen la línea base de degradación y permiten calcular el tamaño del efecto esperado para el ajuste del plan de potencia estadística.

**Fase 3: Evaluación de Técnicas Individuales**

En la tercera fase se ejecutan los cuatro grupos de tratamiento con técnicas individuales (RAG, SessionFacts, MemoryBank, semantic caching) sobre el mismo conjunto de conversaciones de la línea base. Cada grupo de tratamiento se ejecuta de forma independiente, sin acceso a los resultados de los otros grupos durante la ejecución, para evitar contaminación entre condiciones. El orden de ejecución de los grupos se aleatoriza por bloques para controlar posibles efectos de secuencia en la infraestructura.

**Fase 4: Evaluación de Tool Gating**

La cuarta fase evalúa las estrategias de tool gating de forma aislada sobre conversaciones diseñadas específicamente para estresar el catálogo de herramientas: se utilizan escenarios con 20, 50 y 100 herramientas MCP disponibles simultáneamente, con consultas que requieren herramientas de diferentes dominios. Se miden la tasa de selección correcta de herramientas, la tasa de alucinación de parámetros y el consumo de tokens de descripción de herramientas, antes y después de aplicar el filtrado semántico.

**Fase 5: Diseño Factorial y Optimización**

La quinta fase ejecuta el diseño factorial 2k-1 (fraccionado de resolución IV) con los cinco factores binarios identificados en las fases anteriores. Las 16 combinaciones de tratamiento del diseño fraccionado se ejecutan sobre un subconjunto de 50 conversaciones seleccionadas aleatoriamente del conjunto completo. El análisis factorial identifica los efectos principales y las interacciones de segundo orden, y la función objetivo IQCR se utiliza para seleccionar la combinación óptima.

**Fase 6: Análisis Estadístico y Detección de Umbrales**

La sexta fase realiza el análisis estadístico completo: pruebas de hipótesis para HE1–HE5, cálculo de tamaños del efecto, construcción de intervalos de confianza y aplicación del algoritmo PELT para detección de puntos de cambio en las series temporales de degradación. Los análisis se realizarán en Python utilizando las librerías scipy, statsmodels, ruptures (para PELT) y pingouin (para ANOVA y pruebas de equivalencia). Todos los scripts de análisis se publicarán como material suplementario de la tesis para garantizar la reproducibilidad.

**3.7 Técnicas e Instrumentos**

La Tabla 1 presenta las técnicas e instrumentos utilizados en cada fase del estudio:

|                                            |                                                                                                |                                                                                                                  |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Técnica**                                | **Instrumento / Herramienta**                                                                  | **Propósito**                                                                                                    |
| **Inferencia LLM**                         | API Anthropic Claude Sonnet 4.5 (temperatura 0.0)                                              | Motor de razonamiento del agente experimental en todos los grupos de tratamiento                                 |
| **Recuperación semántica (RAG)**           | ChromaDB + modelo de embeddings text-embedding-3-small (OpenAI)                                | Indexación y recuperación del historial de conversación y catálogo de herramientas para los grupos RAG y RAG-MCP |
| **Compresión de sesión (SessionFacts)**    | Módulo de extracción de hechos implementado sobre el SDK de Anthropic                          | Generación periódica (cada 10 turnos) de resumen estructurado del historial de conversación                      |
| **Memoria a largo plazo (MemoryBank)**     | SQLite + implementación del modelo de olvido Ebbinghaus en Python                              | Almacenamiento y recuperación ponderada por relevancia temporal de memorias de conversación                      |
| **Caching semántico**                      | RedisVL con índice HNSW y umbral de similitud coseno = 0.92                                    | Reutilización de respuestas para consultas semánticamente equivalentes                                           |
| **Filtrado de herramientas (tool gating)** | Módulo Python de filtrado semántico sobre embeddings del catálogo MCP                          | Selección dinámica de las k herramientas más relevantes por turno (k = 5 por defecto)                            |
| **Evaluación de exactitud**                | Comparación automática contra ground truth anotado con scorer de coincidencia exacta y parcial | Medición de la métrica primaria de calidad de respuesta en cada turno                                            |
| **Evaluación de coherencia**               | BERTScore (Zhang et al., 2020) con modelo de referencia deberta-v3-large                       | Medición de la similitud semántica entre respuestas consecutivas y con el historial                              |
| **Detección de alucinaciones**             | Verificador de hechos basado en LLM con prompts de verificación cruzada contra ground truth    | Cuantificación de la tasa de alucinación factual en las respuestas                                               |
| **Conteo de tokens**                       | Contadores nativos de la API de Anthropic (input\_tokens, output\_tokens)                      | Medición del consumo de tokens por turno para calcular eficiencia computacional                                  |
| **Análisis estadístico**                   | Python: scipy, statsmodels, pingouin, ruptures                                                 | Pruebas de hipótesis, ANOVA, TOST, detección de puntos de cambio PELT                                            |
| **Gestión de experimentos**                | MLflow para registro de parámetros, métricas y artefactos de cada corrida experimental         | Trazabilidad, reproducibilidad y comparación de experimentos                                                     |

> *Nota.* Técnicas e instrumentos del diseño experimental. API = Application Programming Interface; RAG = Retrieval-Augmented Generation; MCP = Model Context Protocol; HNSW = Hierarchical Navigable Small World; PELT = Pruned Exact Linear Time; TOST = Two One-Sided Tests.

**3.8 Aspectos Éticos**

**Uso Responsable de APIs de IA**

El estudio utiliza la API comercial de Anthropic para acceder al modelo Claude Sonnet 4.5. El uso se realiza en estricto cumplimiento de los términos de servicio y la política de uso aceptable de Anthropic, que permiten el uso de la API para investigación académica. No se realizarán intentos de extraer información sobre los parámetros internos del modelo, de replicar el modelo mediante destilación, ni de vulnerar las salvaguardas de seguridad del sistema.

**Uso de Datos Sintéticos y de Referencia**

Los datasets utilizados —LongMemEval (Truong & Ho, 2023) y LoCoMo (Maharana et al., 2024)— son de acceso público y están publicados bajo licencias que permiten su uso para investigación académica no comercial. Los escenarios de conversación diseñados ad hoc para el experimento son completamente sintéticos y no contienen información personal identificable ni datos sensibles de ninguna persona.

**Propiedad Intelectual y Reproducibilidad**

Todo el código desarrollado para el experimento —incluyendo los módulos de cada técnica de memoria, el módulo de evaluación y los scripts de análisis estadístico— se publicará bajo licencia MIT como material suplementario de la tesis, garantizando la reproducibilidad de los resultados. Las referencias a trabajos previos se citarán siguiendo el formato APA 7 en todos los documentos de la tesis.

**Impacto Ambiental del Cómputo**

El estudio involucra un número significativo de llamadas a la API de inferencia de LLM, que consume energía eléctrica. Se estima un consumo de aproximadamente 500,000 a 1,000,000 de tokens de entrada y salida durante todo el experimento, lo que equivale a un costo energético estimado comparable al de unas pocas horas de uso intensivo de un computador de escritorio (Strubell et al., 2019). Este impacto es modesto en términos absolutos y es aceptable dado el valor científico y práctico del estudio. Se documentará el consumo de tokens por experimento en los reportes de resultados para facilitar la estimación del impacto ambiental por parte de investigadores que deseen replicar el estudio.

**Transparencia y Ausencia de Conflicto de Intereses**

El investigador declara no tener conflictos de interés económicos ni institucionales con Anthropic, los proveedores de los servidores MCP utilizados, ni con los desarrolladores de las herramientas de análisis. Los resultados se reportarán tal como los produzcan los datos, incluyendo los resultados negativos (hipótesis no confirmadas), en cumplimiento del principio de honestidad científica. El proceso de anotación del ground truth y la verificación de alucinaciones será documentado en detalle para permitir la auditoría metodológica del estudio.

**Referencias**

Anthropic. (2024). Model Context Protocol specification (v1.0). Anthropic. [https://modelcontextprotocol.io/specification](https://modelcontextprotocol.io/specification)

Faul, F., Erdfelder, E., Lang, A.-G., & Buchner, A. (2007). G\*Power 3: A flexible statistical power analysis program for the social, behavioral, and biomedical sciences. Behavior Research Methods, 39(2), 175–191. [https://doi.org/10.3758/BF03193146](https://doi.org/10.3758/BF03193146)

Hernández Sampieri, R., Fernández Collado, C., & Baptista Lucio, P. (2014). Metodología de la investigación (6.ª ed.). McGraw-Hill Education.

Killick, R., Fearnhead, P., & Eckley, I. A. (2012). Optimal detection of changepoints with a linear computational cost. Journal of the American Statistical Association, 107(500), 1590–1598. [https://doi.org/10.1080/01621459.2012.737745](https://doi.org/10.1080/01621459.2012.737745)

Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2023). Lost in the middle: How language models use long contexts. Transactions of the Association for Computational Linguistics, 12, 157–173. [https://doi.org/10.1162/tacl\_a\_00638](https://doi.org/10.1162/tacl\_a\_00638)

Maharana, A., Lee, D.-H., Tulyakov, S., Bansal, M., Barbieri, F., & Fang, Y. (2024). Evaluating very long-term conversational memory of LLM agents. arXiv. [https://arxiv.org/abs/2402.17753](https://arxiv.org/abs/2402.17753)

Montgomery, D. C. (2017). Design and analysis of experiments (9.ª ed.). Wiley.

Shadish, W. R., Cook, T. D., & Campbell, D. T. (2002). Experimental and quasi-experimental designs for generalized causal inference. Houghton Mifflin.

Strubell, E., Ganesh, A., & McCallum, A. (2019). Energy and policy considerations for deep learning in NLP. Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics, 3645–3650. [https://doi.org/10.18653/v1/P19-1355](https://doi.org/10.18653/v1/P19-1355)

Truong, T. H., & Ho, T. B. (2023). LongMemEval: Benchmarking long-context language models on long-term interactive memory. arXiv. [https://arxiv.org/abs/2410.10813](https://arxiv.org/abs/2410.10813)

Zhang, T., Kishore, V., Wu, F., Weinberger, K. Q., & Artzi, Y. (2020). BERTScore: Evaluating text generation with BERT. International Conference on Learning Representations. [https://openreview.net/forum?id=SkeHuCVFDr](https://openreview.net/forum?id=SkeHuCVFDr)
