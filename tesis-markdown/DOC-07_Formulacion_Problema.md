# DOC-07 — Formulación del Problema

> **Tipo:** Tesis — Capítulo I  
> **Descripción:** Enunciado formal del problema general y los problemas específicos de investigación.

---

Medición del Impacto de Técnicas de Memoria y Gestión de Contexto

sobre la Degradación de Respuestas en Agentes LLM

Conectados a Múltiples Servidores MCP

DOC-07: Formulación del Problema

Edinson Núñez

Tesis de Maestría

2026

**Formulación del Problema**

La formulación del problema constituye el núcleo lógico de toda investigación científica. A partir del diagnóstico presentado en la realidad problemática, este capítulo organiza y precisa la pregunta central que orienta la tesis, junto con las preguntas derivadas que delimitan sus componentes específicos. La correcta formulación garantiza que la investigación sea medible, reproducible y acotada dentro del alcance disponible.

El presente trabajo aborda un fenómeno emergente en la ingeniería de sistemas de inteligencia artificial: la degradación progresiva de la calidad de respuestas en agentes basados en modelos de lenguaje de gran escala (LLM) cuando estos se conectan simultáneamente a múltiples servidores bajo el Model Context Protocol (MCP). Dicha degradación, denominada context rot en la literatura técnica, tiene consecuencias directas sobre la confiabilidad, precisión y coherencia de los sistemas agentes en entornos de producción.

Si bien existe literatura sobre técnicas individuales de gestión de memoria y contexto —como RAG, tool gating, SessionFacts y semantic caching— no se ha documentado empíricamente en qué medida cada técnica, ni combinaciones de ellas, mitigan el context rot en arquitecturas multi-MCP. Esta brecha justifica la necesidad de un estudio experimental controlado y cuantificable.

**Problema General**

La pregunta general de investigación se formula del siguiente modo:

> *¿En qué medida la aplicación de técnicas de memoria y gestión de contexto reduce la degradación de respuestas (context rot) en agentes LLM conectados a múltiples servidores MCP, en comparación con una arquitectura base sin dichas técnicas?*

Esta pregunta encapsula el problema central en sus tres dimensiones: (a) la variable independiente, constituida por las técnicas de memoria y gestión de contexto; (b) la variable dependiente, representada por la degradación de respuestas medida mediante indicadores cuantitativos; y (c) el contexto de aplicación, definido por la arquitectura multi-MCP en la que operan los agentes LLM.

La pregunta general es verificable mediante un diseño experimental que exponga agentes con y sin técnicas de memoria a conversaciones de duración creciente sobre múltiples servidores MCP, midiendo la evolución de métricas de calidad de respuesta a lo largo del tiempo.

**Problemas Específicos**

A fin de descomponer el problema general en dimensiones investigables y acotadas, se plantean los siguientes problemas específicos:

**Problema Específico 1: Cuantificación de la Degradación Base**

> *¿Cómo y en qué magnitud se manifiesta la degradación de respuestas (context rot) en agentes LLM conectados a múltiples servidores MCP cuando no se aplica ninguna técnica de memoria o gestión de contexto?*

Este problema establece la línea base (baseline) del experimento. Para responderlo, se ejecutarán agentes LLM en configuración sin memoria sobre sesiones de conversación de longitud creciente (10, 30, 60 y 100 turnos), registrando la evolución de métricas como exactitud de respuesta, tasa de alucinación, latencia media y uso de tokens. Los resultados de este problema alimentarán el denominador de todas las comparaciones relativas realizadas en los problemas subsecuentes.

**Problema Específico 2: Efectividad de Técnicas de Memoria Individuales**

> *¿En qué medida cada técnica individual de memoria —RAG semántico, SessionFacts, MemoryBank y semantic caching— reduce la degradación de respuestas en agentes LLM multi-MCP, medida en términos de exactitud, coherencia y consumo de tokens?*

Este problema examina el efecto aislado de cuatro técnicas representativas identificadas en la revisión de literatura. Para cada técnica se implementará una variante del agente experimental y se ejecutarán los mismos escenarios de conversación que en el baseline. La comparación permitirá estimar el efecto marginal de cada técnica sobre las métricas seleccionadas, identificando cuál ofrece la mejor relación entre mejora en calidad y overhead computacional.

**Problema Específico 3: Efectividad de Técnicas de Tool Gating**

> *¿En qué medida las estrategias de tool gating —incluyendo carga diferida de herramientas y filtrado semántico por relevancia— reducen la sobrecarga de contexto y la degradación de respuestas en agentes LLM conectados a catálogos de herramientas MCP de gran escala?*

El tool overload constituye uno de los tres mecanismos principales de context rot identificados en la literatura. Este problema específico aísla el impacto de exponer un gran número de herramientas MCP al modelo (20, 50 y 100 herramientas disponibles) versus aplicar filtrado semántico dinámico que reduzca las herramientas visibles al contexto inmediato. Las métricas de interés incluyen la tasa de selección correcta de herramientas, la tasa de alucinación de parámetros y el número de tokens consumidos por la descripción de herramientas.

**Problema Específico 4: Sinergia de Técnicas Combinadas**

> *¿Qué combinación de técnicas de memoria y gestión de contexto produce el mayor impacto positivo sobre la calidad de respuestas en agentes LLM multi-MCP, considerando conjuntamente la exactitud, la coherencia, la latencia y el consumo de recursos computacionales?*

Este problema aborda el efecto de sinergia o interferencia entre técnicas. Una vez caracterizado el efecto individual de cada técnica (PE1–PE3), se evaluarán configuraciones combinadas seleccionadas mediante diseño factorial 2k reducido. El objetivo es determinar si la combinación de, por ejemplo, RAG semántico con tool gating y SessionFacts supera el desempeño de cualquiera de las técnicas aplicadas de forma independiente, y en qué condiciones se produce efecto de saturación o redundancia.

**Problema Específico 5: Umbrales de Degradación y Puntos Críticos**

> *¿Existen umbrales de longitud de contexto o número de servidores MCP a partir de los cuales la degradación de respuestas se vuelve estadísticamente significativa e irreversible, con y sin técnicas de memoria aplicadas?*

La literatura sugiere que el context rot no es lineal: investigaciones previas han identificado puntos de inflexión a partir de los cuales la calidad cae abruptamente. Este problema busca localizar empíricamente esos umbrales para la arquitectura multi-MCP, lo que tiene implicaciones directas para el diseño de sistemas en producción. Se modelarán las curvas de degradación en función de la longitud de contexto (en tokens) y el número de servidores MCP activos, identificando los puntos de quiebre mediante análisis de segmentación de series temporales.

**Variables Derivadas de la Formulación**

La formulación de los problemas anterior permite identificar con precisión las variables del estudio:

**Variable Independiente**

Tipo y combinación de técnicas de memoria y gestión de contexto aplicadas al agente LLM. Esta variable se operacionaliza mediante cinco niveles de tratamiento: (a) sin técnica (baseline), (b) RAG semántico únicamente, (c) SessionFacts únicamente, (d) tool gating únicamente y (e) combinación óptima de técnicas.

**Variable Dependiente**

Nivel de degradación de respuestas (context rot), medido a través de un índice compuesto que integra cuatro dimensiones: (a) exactitud de respuesta, medida contra ground truth anotado; (b) tasa de alucinación, determinada mediante verificación cruzada automatizada; (c) coherencia conversacional, evaluada con métricas de similitud semántica entre turnos; y (d) consumo de tokens por turno, como indicador de eficiencia computacional.

**Variables de Control**

Con el fin de garantizar la validez interna del experimento, se mantendrán constantes las siguientes variables: (a) modelo LLM base (Claude Sonnet 4.5); (b) temperatura de generación (0.0 para reproducibilidad); (c) conjunto de datos de evaluación; (d) número y tipo de servidores MCP en los escenarios de prueba; y (e) infraestructura de cómputo utilizada para la ejecución de los experimentos.

**Variables Moderadoras**

Se identifican dos variables moderadoras que podrían influir en la relación entre la variable independiente y la dependiente: (a) longitud de la conversación, expresada en número de turnos y total de tokens acumulados; y (b) número de servidores MCP activos en la sesión, que determina el volumen de herramientas disponibles para el agente.

**Alcance y Delimitación de la Formulación**

La formulación presentada se circunscribe a las siguientes condiciones: (a) agentes LLM basados en arquitecturas transformer de acceso comercial o de código abierto con soporte nativo al protocolo MCP; (b) conversaciones estructuradas en formato multi-turno de pregunta-respuesta, sin considerar interacciones multimodales; (c) servidores MCP que exponen herramientas de consulta de información, ejecución de código y acceso a datos estructurados; y (d) medición del impacto en términos de calidad de respuesta y eficiencia computacional, sin incluir análisis de seguridad ni evaluaciones de equidad algorítmica.

Quedan fuera del alcance de esta formulación los aspectos relacionados con el ajuste fino (fine-tuning) de modelos, el entrenamiento continuo, la personalización de embeddings propietarios, y los escenarios de despliegue en infraestructuras reguladas o con requisitos de privacidad especiales. Estas limitaciones son consistentes con el alcance declarado en DOC-05 (Introducción de la Tesis) y permiten que el estudio sea ejecutable dentro de los recursos disponibles para una investigación de maestría.

**Coherencia con Hipótesis y Objetivos**

Cada problema específico formulado en esta sección se corresponde biunívocamente con un objetivo específico de la investigación (documentado en DOC-09) y con una hipótesis específica (documentada en DOC-13). Esta correspondencia garantiza la coherencia interna del diseño de investigación y facilita la elaboración posterior de la matriz de consistencia (DOC-14 y DOC-15).

La Tabla 1 muestra la correspondencia entre problemas específicos, objetivos e hipótesis:

|         |                                                                                          |                                                                                                                             |                                                                                                                           |
| ------- | ---------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **N°**  | **Problema Específico**                                                                  | **Objetivo Específico**                                                                                                     | **Hipótesis Específica**                                                                                                  |
| **PE1** | Cuantificación de degradación base (sin técnicas aplicadas)                              | OE1: Establecer la línea base de degradación en arquitectura multi-MCP sin memoria                                          | HE1: La arquitectura sin memoria presenta \>25% de degradación a partir del turno 30                                      |
| **PE2** | Efectividad de técnicas de memoria individuales (RAG, SessionFacts, MemoryBank, caching) | OE2: Comparar el impacto de cada técnica de memoria sobre las métricas de calidad de respuesta                              | HE2: Al menos una técnica individual reduce la degradación en \>40% respecto al baseline                                  |
| **PE3** | Efectividad de técnicas de tool gating y carga diferida de herramientas                  | OE3: Evaluar el impacto del tool gating sobre la sobrecarga de contexto y la tasa de selección correcta                     | HE3: El tool gating reduce el consumo de tokens de herramientas en \>50% sin sacrificar exactitud                         |
| **PE4** | Sinergia de técnicas combinadas en arquitecturas multi-MCP                               | OE4: Identificar la combinación de técnicas que maximiza la calidad de respuesta y minimiza el context rot                  | HE4: La combinación óptima supera a cualquier técnica individual en al menos dos métricas de calidad                      |
| **PE5** | Umbrales de degradación y puntos críticos de context rot                                 | OE5: Localizar los umbrales de longitud de contexto a partir de los cuales el context rot es estadísticamente significativo | HE5: Existen umbrales discretos de longitud de contexto y número de servidores MCP que predicen el inicio del context rot |

> *Nota.* Correspondencia entre problemas, objetivos e hipótesis del estudio. Los documentos DOC-09 y DOC-13 desarrollan en extenso cada objetivo e hipótesis respectivamente.

**Referencias**

<a id="ref-anthropic2024"></a>
Anthropic. (2024). Model Context Protocol specification (v1.0). Anthropic. [https://modelcontextprotocol.io/specification](https://modelcontextprotocol.io/specification)

<a id="ref-brown2020"></a>
Brown, T. B., Mann, B., Ryder, N., Subbiah, M., Kaplan, J., Dhariwal, P., Neelakantan, A., Shyam, P., Sastry, G., Askell, A., Agarwal, S., Herbert-Voss, A., Krueger, G., Henighan, T., Child, R., Ramesh, A., Ziegler, D. M., Wu, J., Winter, C., … Amodei, D. (2020). Language models are few-shot learners. Advances in Neural Information Processing Systems, 33, 1877–1901. [https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html](https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html)

<a id="ref-chroma2025"></a>
Chroma Research. (2025). Context rot in production LLM systems: A benchmark study. Chroma. [https://www.trychroma.com/blog/context-rot](https://www.trychroma.com/blog/context-rot)

<a id="ref-hu2023"></a>
Hu, J., Huang, S., Luo, Y., Wu, F., & Lam, W. (2023). MemoryBank: Enhancing large language models with long-term memory. arXiv. [https://arxiv.org/abs/2305.10250](https://arxiv.org/abs/2305.10250)

<a id="ref-lewis2020"></a>
Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. Advances in Neural Information Processing Systems, 33, 9459–9474. [https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html](https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html)

<a id="ref-liu2023"></a>
Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2023). Lost in the middle: How language models use long contexts. Transactions of the Association for Computational Linguistics, 12, 157–173. [https://doi.org/10.1162/tacl\_a\_00638](https://doi.org/10.1162/tacl\_a\_00638)

<a id="ref-packer2023"></a>
Packer, C., Wooders, S., Lin, K., Fang, V., Patil, S. G., Stoica, I., & Gonzalez, J. E. (2023). MemGPT: Towards LLMs as operating systems. arXiv. [https://arxiv.org/abs/2310.08560](https://arxiv.org/abs/2310.08560)

<a id="ref-patil2023"></a>
Patil, S. G., Zhang, T., Wang, X., & Gonzalez, J. E. (2023). Gorilla: Large language model connected with massive APIs. arXiv. [https://arxiv.org/abs/2305.15334](https://arxiv.org/abs/2305.15334)

<a id="ref-redis2025"></a>
Redis Labs. (2025). Enterprise AI deployment patterns: Token consumption and memory management. Redis. [https://redis.io/blog/enterprise-ai-memory-2025](https://redis.io/blog/enterprise-ai-memory-2025)

<a id="ref-tang2025"></a>
Tang, R., Jin, Z., Alexandrov, A., Shao, Y., Shi, P., & Pan, L. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. arXiv. [https://arxiv.org/abs/2502.03415](https://arxiv.org/abs/2502.03415)

<a id="ref-yao2022"></a>
Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. arXiv. [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)

<a id="ref-zeng2025"></a>
Zeng, Z., Liu, M., Lu, R., Wang, B., Liu, X., & Cheng, X. (2025). SimpleToolHalluBench: Towards a comprehensive assessment of tool call hallucination in large language models. arXiv. [https://arxiv.org/abs/2501.13395](https://arxiv.org/abs/2501.13395)
