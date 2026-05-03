# DOC-09 — Objetivos General y Específicos

> **Tipo:** Tesis — Capítulo I  
> **Descripción:** Objetivo general y objetivos específicos alineados con el problema e hipótesis.

---

Medición del Impacto de Técnicas de Memoria y Gestión de Contexto

sobre la Degradación de Respuestas en Agentes LLM

Conectados a Múltiples Servidores MCP

**DOC-09: Objetivos General y Específicos**

Edinson Núñez

Tesis de Maestría

2026

**Objetivos de la Investigación**

Los objetivos de investigación constituyen los enunciados precisos de los logros que se pretende alcanzar mediante el estudio. Deben ser formulados en términos observables, medibles y alcanzables dentro del tiempo y los recursos disponibles. En consonancia con la formulación del problema planteada en DOC-07, se establece un objetivo general que responde al problema central, y cinco objetivos específicos que se corresponden biunívocamente con los cinco problemas específicos identificados.

Los objetivos han sido redactados en infinitivo, con un verbo de acción verificable, un objeto de estudio claramente delimitado y una condición de aplicación que especifica el contexto experimental. Esta estructura garantiza que cada objetivo sea operacionalizable en un conjunto de actividades, tareas y entregables concretos durante la ejecución del estudio.

**Objetivo General**

El objetivo general de la investigación se enuncia del siguiente modo:

> **OG:** Medir el impacto de las técnicas de memoria y gestión de contexto sobre la degradación de respuestas (context rot) en agentes LLM conectados a múltiples servidores MCP, identificando qué técnicas o combinaciones de técnicas reducen significativamente dicha degradación y bajo qué condiciones de longitud de contexto y escala de herramientas.

Este objetivo integra las tres dimensiones del problema general: (a) la medición cuantitativa del fenómeno, que requiere la definición y operacionalización de un índice de calidad de respuesta; (b) la comparación sistemática de técnicas de memoria y gestión de contexto, que demanda un diseño experimental controlado con múltiples condiciones de tratamiento; y (c) la caracterización de las condiciones de aplicación, que exige modelar la relación entre la longitud del contexto, el número de servidores MCP activos y la efectividad de cada técnica.

El objetivo general es alcanzable dentro del marco de una investigación de maestría dado que: (i) los modelos LLM de acceso comercial y de código abierto con soporte MCP están disponibles; (ii) los frameworks de evaluación de referencia ---LongMemEval, LoCoMo, SimpleToolHalluBench--- ofrecen datasets reutilizables como punto de partida; y (iii) las técnicas de memoria a evaluar cuentan con implementaciones de referencia publicadas en código abierto.

**Objetivos Específicos**

Los objetivos específicos desagregan el objetivo general en componentes investigables de forma independiente, cuya consecución conjunta garantiza el logro del objetivo principal.

**Objetivo Específico 1: Establecimiento de la Línea Base**

> **OE1:** Establecer la línea base cuantitativa de degradación de respuestas en agentes LLM conectados a múltiples servidores MCP sin aplicación de técnicas de memoria o gestión de contexto, mediante la ejecución de conversaciones de longitud creciente y el registro sistemático de métricas de exactitud, coherencia, tasa de alucinación y consumo de tokens por turno.

Este objetivo es el fundamento del diseño experimental: sin una línea base robusta, ninguna comparación relativa tiene validez. Las actividades asociadas incluyen la selección y configuración de al menos tres servidores MCP representativos de diferentes dominios (recuperación de información, ejecución de código y acceso a datos estructurados), el diseño de un conjunto de conversaciones de prueba de 10, 30, 60 y 100 turnos, y la instrumentación del agente para registrar las métricas seleccionadas en cada turno. El entregable es una curva de degradación baseline y la caracterización estadística descriptiva del fenómeno.

**Objetivo Específico 2: Evaluación de Técnicas Individuales de Memoria**

> **OE2:** Comparar el impacto individual de cuatro técnicas representativas de memoria y gestión de contexto ---RAG semántico, SessionFacts, MemoryBank y semantic caching--- sobre las métricas de calidad de respuesta, determinando el efecto marginal de cada técnica respecto a la línea base establecida en OE1.

Para cada técnica se implementará una variante del agente experimental y se ejecutarán los mismos escenarios de conversación de la línea base. El análisis estadístico incluirá pruebas de diferencia de medias (t de Student o Mann-Whitney U según la distribución de los datos), tamaño del efecto (d de Cohen) y análisis de varianza para determinar si las diferencias observadas son estadísticamente significativas (α = 0.05). El entregable es una tabla comparativa de efectividad con intervalos de confianza al 95%.

**Objetivo Específico 3: Evaluación de Técnicas de Tool Gating**

> **OE3:** Evaluar el impacto de estrategias de tool gating ---incluyendo carga diferida de herramientas y filtrado semántico dinámico--- sobre la sobrecarga de contexto generada por catálogos de herramientas MCP de gran escala (20, 50 y 100 herramientas), midiendo la tasa de selección correcta de herramientas, la tasa de alucinación de parámetros y la reducción porcentual en el consumo de tokens de descripción.

Este objetivo aborda de forma aislada el mecanismo de tool overload, uno de los tres vectores principales del context rot identificados en la literatura. Las actividades incluyen la construcción de catálogos de herramientas MCP sintéticos con 20, 50 y 100 herramientas de diferente relevancia para cada consulta, y la implementación de un módulo de filtrado semántico basado en similitud coseno entre la consulta del usuario y las descripciones de las herramientas. El umbral de selección se optimizará mediante validación cruzada sobre un subconjunto del dataset de prueba.

**Objetivo Específico 4: Identificación de la Combinación Óptima**

> **OE4:** Identificar la combinación de técnicas de memoria y gestión de contexto que maximiza la calidad de respuesta en agentes LLM multi-MCP, minimizando simultáneamente la degradación de respuestas y el overhead computacional, mediante un diseño factorial 2k reducido aplicado a las técnicas evaluadas en OE2 y OE3.

El diseño factorial permitirá estimar los efectos principales e interacciones de segundo orden entre las técnicas, identificando sinergias y efectos de saturación. La función objetivo del proceso de optimización considerará un índice ponderado que integra la mejora en exactitud de respuesta, la reducción en tasa de alucinación y el overhead en latencia y tokens generado por la técnica. La ponderación de los criterios se definirá mediante consulta a expertos del sector utilizando el método AHP (Analytic Hierarchy Process). El entregable es una recomendación de configuración óptima para arquitecturas multi-MCP en producción.

**Objetivo Específico 5: Localización de Umbrales de Degradación**

> **OE5:** Localizar empíricamente los umbrales de longitud de contexto (en tokens acumulados) y número de servidores MCP activos a partir de los cuales la degradación de respuestas se vuelve estadísticamente significativa, con y sin la aplicación de las técnicas de memoria evaluadas, mediante análisis de segmentación de series temporales y modelización de puntos de cambio.

La identificación de umbrales tiene valor tanto teórico ---como caracterización del comportamiento emergente de los LLM bajo carga de contexto--- como práctico, pues permite a los ingenieros de sistemas definir políticas de activación automática de técnicas de memoria en función de indicadores observables (contador de tokens, número de herramientas activas). Se aplicarán algoritmos de detección de puntos de cambio (PELT, Binary Segmentation) sobre las series temporales de métricas de calidad registradas en OE1--OE4. El entregable es un mapa de umbrales con sus intervalos de confianza, expresados en unidades operacionales (tokens y número de servidores).

**Síntesis de Objetivos**

La Tabla 1 presenta la síntesis de todos los objetivos de la investigación, incluyendo el verbo de acción, el objeto de estudio, las métricas de logro y el entregable esperado:

  ---------- ------------- ------------------------------------------------------------------------------ ------------------------------------------------------------------------------ --------------------------------------------------------------------
  **Cód.**   **Verbo**     **Objeto de Estudio**                                                          **Métricas de Logro**                                                          **Entregable**
  **OG**     Medir         Impacto de técnicas de memoria sobre el context rot en agentes LLM multi-MCP   Reducción % en degradación de respuestas; configuración óptima identificada    Informe experimental con recomendaciones de diseño arquitectónico
  **OE1**    Establecer    Línea base de degradación sin técnicas de memoria                              Curva de degradación en 4 longitudes; CI 95% por métrica                       Dataset baseline + curvas de degradación anotadas
  **OE2**    Comparar      Impacto individual de RAG, SessionFacts, MemoryBank y caching                  d de Cohen ≥ 0.5; p \< 0.05 para al menos una técnica                          Tabla comparativa de efectividad por técnica
  **OE3**    Evaluar       Impacto del tool gating con catálogos de 20, 50 y 100 herramientas             Reducción ≥ 40% en tokens de descripción sin pérdida de exactitud              Módulo de filtrado semántico validado + curva precision-recall
  **OE4**    Identificar   Combinación óptima de técnicas en diseño factorial 2k                          Índice compuesto IQCR ≥ 80% vs baseline; overhead \< 15%                       Recomendación de configuración óptima con análisis costo-beneficio
  **OE5**    Localizar     Umbrales de degradación estadísticamente significativos                        Puntos de cambio detectados con CI 95%; expresados en tokens y Nº servidores   Mapa de umbrales de context rot por condición experimental
  ---------- ------------- ------------------------------------------------------------------------------ ------------------------------------------------------------------------------ --------------------------------------------------------------------

> *Nota.* Síntesis de los objetivos de la investigación. OG = Objetivo General; OE = Objetivo Específico; IQCR = Índice de Calidad de Respuesta Compuesto; CI = Intervalo de Confianza.

**Coherencia con el Diseño de la Investigación**

Los objetivos presentados en este documento mantienen coherencia lógica con los demás componentes del diseño de investigación. El objetivo general responde directamente al problema general formulado en DOC-07, y cada objetivo específico responde a su correspondiente problema específico. Los verbos de acción seleccionados ---medir, establecer, comparar, evaluar, identificar, localizar--- son consistentes con una investigación de enfoque cuantitativo y diseño experimental, lo que se articula con la justificación metodológica presentada en DOC-08.

Cada objetivo específico se operacionaliza mediante indicadores cuantificables (métricas de logro en la Tabla 1), lo que permite evaluar el grado de consecución de cada objetivo al finalizar la investigación. Esta operacionalización es el insumo directo para la construcción de la hipótesis general y las hipótesis específicas (DOC-13), así como para la elaboración de la matriz de consistencia (DOC-14 y DOC-15) que vincula formalmente el problema, los objetivos, las hipótesis y los instrumentos de medición.

El logro conjunto de OE1 a OE5 es condición necesaria y suficiente para el logro del OG: (a) OE1 proporciona la referencia comparativa; (b) OE2 y OE3 generan evidencia sobre el efecto de técnicas individuales; (c) OE4 integra los hallazgos en una configuración optimizada; y (d) OE5 caracteriza las condiciones límite del fenómeno, completando así la respuesta a la pregunta central de investigación.

**Referencias**

Hernández Sampieri, R., Fernández Collado, C., & Baptista Lucio, P. (2014). Metodología de la investigación (6.ª ed.). McGraw-Hill Education.

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. Advances in Neural Information Processing Systems, 33, 9459--9474. https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html

Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2023). Lost in the middle: How language models use long contexts. Transactions of the Association for Computational Linguistics, 12, 157--173. https://doi.org/10.1162/tacl\_a\_00638

Packer, C., Wooders, S., Lin, K., Fang, V., Patil, S. G., Stoica, I., & Gonzalez, J. E. (2023). MemGPT: Towards LLMs as operating systems. arXiv. https://arxiv.org/abs/2310.08560

Saaty, T. L. (1980). The analytic hierarchy process. McGraw-Hill.

Tang, R., Jin, Z., Alexandrov, A., Shao, Y., Shi, P., & Pan, L. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. arXiv. https://arxiv.org/abs/2502.03415

Truong, T. H., & Ho, T. B. (2023). LongMemEval: Benchmarking long-context language models on long-term interactive memory. arXiv. https://arxiv.org/abs/2410.10813

Zeng, Z., Liu, M., Lu, R., Wang, B., Liu, X., & Cheng, X. (2025). SimpleToolHalluBench: Towards a comprehensive assessment of tool call hallucination in large language models. arXiv. https://arxiv.org/abs/2501.13395
