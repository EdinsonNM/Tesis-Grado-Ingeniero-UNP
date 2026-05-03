# DOC-11 — Bases Teóricas

> **Tipo:** Tesis — Capítulo II  
> **Descripción:** Marco teórico: LLMs, MCP, técnicas de memoria, context rot, RAG y evaluación.

---

Medición del Impacto de Técnicas de Memoria y Gestión de Contexto

sobre la Degradación de Respuestas en Agentes LLM

Conectados a Múltiples Servidores MCP

**DOC-11: Bases Teóricas**

Edinson Núñez

Tesis de Maestría

2026

**Bases Teóricas**

Las bases teóricas constituyen el fundamento conceptual que sustenta el diseño, la ejecución y la interpretación de la investigación. En este capítulo se desarrollan los constructos teóricos centrales organizados en siete bloques temáticos: (a) modelos de lenguaje de gran escala y su arquitectura; (b) agentes LLM y marcos de razonamiento-acción; (c) el Model Context Protocol como infraestructura de integración; (d) degradación de contexto y el fenómeno de context rot; (e) técnicas de memoria y gestión de contexto; (f) estrategias de tool gating; y (g) evaluación y benchmarks para agentes LLM.

Cada bloque establece las definiciones operacionales que se utilizarán en el estudio, sintetiza el estado del conocimiento en ese eje y articula la conexión con el problema de investigación. El desarrollo sigue el orden lógico de construcción de la problemática: desde los fundamentos del modelo hasta las técnicas de mitigación y los instrumentos de medición.

**Modelos de Lenguaje de Gran Escala**

**Definición y Características Fundamentales**

Los modelos de lenguaje de gran escala (Large Language Models, LLM) son sistemas de inteligencia artificial entrenados sobre vastos corpus de texto mediante el objetivo de predicción de la siguiente palabra (next-token prediction). Su arquitectura subyacente es el transformer ([Vaswani et al., 2017](#ref-vaswani2017)), que introdujo el mecanismo de atención multi-cabezal (multi-head self-attention) como alternativa a las redes recurrentes para el modelado de dependencias a larga distancia en secuencias de texto.

La arquitectura transformer opera sobre representaciones vectoriales densas denominadas embeddings, que codifican el significado semántico de los tokens. El mecanismo de atención calcula, para cada token en la secuencia de entrada, un vector de contexto ponderado por la relevancia de todos los demás tokens, lo que permite al modelo capturar relaciones sintácticas y semánticas complejas independientemente de la distancia entre los elementos en la secuencia ([Vaswani et al., 2017](#ref-vaswani2017)).

Los LLM modernos como la familia GPT ([Brown et al., 2020](#ref-brown2020)), Llama ([Touvron et al., 2023](#ref-touvron2023)), Gemini ([Anil et al., 2023](#ref-anil2023)) y Claude ([Anthropic, 2024](#ref-anthropic2024)) escalan esta arquitectura a miles de millones de parámetros y emplean técnicas de ajuste fino con retroalimentación humana (Reinforcement Learning from Human Feedback, RLHF) para alinear el comportamiento del modelo con las preferencias del usuario ([Ouyang et al., 2022](#ref-ouyang2022)).

**La Ventana de Contexto**

Un concepto central para la comprensión del problema estudiado es la ventana de contexto (context window), que define el número máximo de tokens que el modelo puede procesar en una sola inferencia. La ventana de contexto incluye tanto la entrada del usuario como el historial de conversación y las respuestas del modelo, lo que significa que en conversaciones largas el contexto disponible se llena progresivamente.

Los LLM de generación actual cuentan con ventanas de contexto que van desde los 128,000 tokens (Claude Sonnet 4.5, Anthropic, 2024) hasta el millón de tokens (Gemini 1.5 Pro, Anil et al., 2023). Sin embargo, la capacidad nominal de la ventana de contexto no equivale a una capacidad de atención uniforme sobre todos los tokens presentes: [Liu et al. (2023)](#ref-liu2023) demostraron que los LLM exhiben un sesgo de posición que reduce la atención efectiva sobre los tokens ubicados en el centro de contextos largos —el denominado efecto lost-in-the-middle—, con consecuencias directas sobre la calidad de las respuestas en conversaciones extensas.

**Capacidades de Razonamiento y Limitaciones**

Los LLM han demostrado capacidades emergentes de razonamiento en cadena (chain-of-thought reasoning; Wei et al., 2022) que les permiten resolver problemas complejos descomponiéndolos en pasos intermedios. Estas capacidades son la base del uso de LLM como motores de razonamiento en sistemas agentes. Sin embargo, los LLM presentan limitaciones estructurales que son relevantes para el problema estudiado: (a) su conocimiento está congelado en la fecha de corte del entrenamiento; (b) no tienen acceso nativo a información externa ni a herramientas computacionales; y (c) su comportamiento en contextos muy largos se degrada, como se documenta ampliamente en la sección sobre context rot.

**Agentes LLM y Marcos de Razonamiento-Acción**

**Definición de Agente LLM**

Un agente LLM es un sistema de software que utiliza un modelo de lenguaje como motor de razonamiento y lo combina con la capacidad de ejecutar acciones en el entorno —ya sean llamadas a herramientas externas, búsquedas en bases de datos, ejecución de código o interacciones con APIs— con el objetivo de completar tareas que van más allá de la generación de texto estático ([Wang et al., 2024](#ref-wang2024)). A diferencia del uso conversacional de un LLM, los agentes operan en ciclos de razonamiento-acción-observación que pueden extenderse a lo largo de múltiples turnos y herramientas.

**El Marco ReAct**

El marco ReAct (Reasoning and Acting; [Yao et al., 2022](#ref-yao2022)) formalizó el ciclo de operación de los agentes LLM mediante la interleaved generation de pensamientos (razonamiento) y acciones (llamadas a herramientas). En el marco ReAct, el agente genera alternativamente: (a) un pensamiento que razona sobre el estado actual de la tarea; (b) una acción que especifica la herramienta a invocar y sus parámetros; y (c) una observación que incorpora el resultado de la herramienta al contexto. Este ciclo se repite hasta que el agente determina que dispone de suficiente información para producir la respuesta final.

La importancia del marco ReAct para el problema estudiado radica en que cada ciclo de razonamiento-acción-observación acumula tokens en el contexto: los pensamientos intermedios, las llamadas a herramientas y sus resultados se concatenan al historial, lo que contribuye directamente al fenómeno de context rot en conversaciones largas.

**Toolformer y Uso Autónomo de Herramientas**

Toolformer ([Schick et al., 2023](#ref-schick2023)) demostró que los LLM podían aprender a usar herramientas de forma autónoma mediante autoentrenamiento sobre ejemplos generados sintéticamente. El modelo aprende a insertar llamadas a APIs en el texto de generación en los momentos en que la herramienta añade valor a la respuesta. Este trabajo estableció el precedente técnico para el uso de herramientas como capacidad nativa de los LLM, que posteriormente se generalizó en los sistemas de function calling de [OpenAI (2023)](#ref-openai2023) y en el Model Context Protocol de [Anthropic (2024)](#ref-anthropic2024).

**Arquitecturas Multi-Agente**

Las arquitecturas multi-agente extienden el paradigma del agente individual mediante la coordinación de múltiples LLM especializados que colaboran para resolver tareas complejas ([Hong et al., 2023](#ref-hong2023)). En estas arquitecturas, los agentes pueden actuar como orquestadores —que delegan subtareas— o como ejecutores especializados. Aunque el presente estudio se centra en agentes individuales conectados a múltiples servidores MCP y no en sistemas multi-agente propiamente dichos, los principios de gestión de contexto y memoria son transferibles a ambas arquitecturas.

**Model Context Protocol**

**Origen y Motivación**

El Model Context Protocol (MCP) fue publicado por Anthropic en noviembre de 2024 como un estándar abierto para la integración de agentes LLM con herramientas y fuentes de datos externas ([Anthropic, 2024](#ref-anthropic2024)). La motivación principal del protocolo fue resolver el problema de la fragmentación de integraciones: cada herramienta o API requería una integración ad hoc con el agente, lo que generaba costos de mantenimiento elevados y limitaba la interoperabilidad entre sistemas. MCP define una interfaz estandarizada que permite a cualquier servidor exponer herramientas que cualquier cliente MCP compatible puede invocar sin código de integración específico.

**Arquitectura del Protocolo**

La arquitectura MCP sigue el patrón cliente-servidor. El servidor MCP expone un catálogo de herramientas (tools), recursos (resources) y prompts mediante un esquema JSON estandarizado. El cliente MCP —que en el contexto de esta tesis es el agente LLM— negocia las capacidades con el servidor durante la inicialización de la sesión y recibe el listado completo de herramientas disponibles, incluyendo sus nombres, descripciones y esquemas de parámetros en formato JSON Schema.

El flujo de comunicación MCP estándar incluye cuatro fases: (a) inicialización (initialize), en la que el cliente declara sus capacidades y el servidor responde con las suyas; (b) listado de herramientas (tools/list), en la que el cliente obtiene el catálogo completo de herramientas disponibles; (c) invocación (tools/call), en la que el cliente ejecuta una herramienta específica con los parámetros requeridos; y (d) notificación de cambios (notifications/tools/list\_changed), mediante la que el servidor comunica actualizaciones en el catálogo de herramientas ([Anthropic, 2024](#ref-anthropic2024)).

**Impacto sobre el Contexto del Agente**

El aspecto del protocolo MCP más relevante para el problema estudiado es el mecanismo de exposición de herramientas. En la implementación estándar de MCP, el cliente recibe y mantiene en el contexto del modelo las descripciones completas de todas las herramientas disponibles en todos los servidores conectados. Para un servidor típico con 20 herramientas cuyas descripciones ocupan un promedio de 200 tokens cada una, la sola exposición del catálogo consume 4,000 tokens del contexto disponible ([Tang et al., 2025](#ref-tang2025)). En arquitecturas multi-servidor con 3 a 5 servidores MCP activos, este overhead puede alcanzar los 12,000–20,000 tokens, lo que representa entre el 9% y el 16% de la ventana de contexto de un modelo de 128,000 tokens, antes de que el agente haya procesado una sola consulta del usuario.

**Degradación de Contexto y Context Rot**

**Definición Operacional de Context Rot**

Para los efectos de esta investigación, se define context rot como el proceso de degradación progresiva y acumulativa de la calidad de las respuestas de un agente LLM, medida a través de métricas cuantificables, como consecuencia del crecimiento del contexto activo en conversaciones multi-turno con acceso a múltiples servidores MCP. El término, adoptado de la práctica industrial (Chroma Research, 2025), captura la analogía con el deterioro de datos en sistemas de almacenamiento: así como los datos se corrompen por acumulación de errores, el contexto de un agente LLM se degrada por acumulación de información irrelevante, redundante o contradictoria.

**Mecanismos de Context Rot en Arquitecturas Multi-MCP**

La literatura y la práctica industrial identifican tres mecanismos principales a través de los cuales el context rot se manifiesta en arquitecturas multi-MCP:

***Tool Overload***

El tool overload ocurre cuando el número de herramientas expuestas al modelo supera la capacidad de atención efectiva del sistema. [Patil et al. (2023)](#ref-patil2023) identificaron que los LLM exhiben degradación en la selección de herramientas cuando el catálogo disponible supera las 20 herramientas en contexto. [Tang et al. (2025)](#ref-tang2025) cuantificaron que la tasa de alucinación en la especificación de parámetros de herramientas aumenta en un 23% cuando el número de herramientas disponibles pasa de 10 a 50. Este mecanismo es especialmente pronunciado en arquitecturas multi-MCP donde cada servidor contribuye con su propio catálogo de herramientas al contexto compartido del agente.

***Acumulación de Resultados Intermedios***

En el ciclo ReAct, los resultados de cada invocación de herramienta se incorporan al contexto del agente como observaciones. En conversaciones largas, estas observaciones se acumulan linealmente, desplazando hacia el centro del contexto las instrucciones iniciales y el historial de conversación más antiguo. [Liu et al. (2023)](#ref-liu2023) demostraron que los LLM exhiben una reducción de hasta el 40% en la utilización efectiva de información ubicada en el centro del contexto en comparación con la información ubicada al inicio o al final. Este efecto de lost-in-the-middle se intensifica cuando los resultados de herramientas —que suelen ser verbosos y poco comprimidos— ocupan la región central del contexto.

***Mezcla de Estados de Sesión***

En arquitecturas multi-MCP, cada servidor mantiene su propio estado de sesión y puede generar metadatos de contexto —mensajes de error, avisos de autenticación, paginación de resultados— que se incorporan al contexto del agente. La coexistencia de metadatos de múltiples servidores con semánticas distintas introduce ruido en el contexto que puede confundir al modelo sobre el estado actual de la tarea. [Chroma Research (2025)](#ref-chroma2025) documentó que los agentes multi-MCP exhiben tasas de error en la atribución de resultados a servidores correctos que aumentan del 3% en sesiones de un servidor al 18% en sesiones de cinco servidores, evidenciando el impacto de la mezcla de estados de sesión.

**Evidencia Empírica de Context Rot**

La evidencia empírica sobre la degradación de respuestas en contextos largos es convergente. [Liu et al. (2023)](#ref-liu2023) demostraron la degradación en tareas de recuperación de información con contextos de hasta 4,000 tokens. [Shi et al. (2023)](#ref-shi2023) mostraron que la presencia de información irrelevante en el contexto reduce la exactitud en tareas de razonamiento en hasta un 65%. [Chroma Research (2025)](#ref-chroma2025) documentó degradaciones superiores al 30% en la exactitud de respuestas de agentes LLM en producción después de 50 turnos de conversación. [Redis Labs (2025)](#ref-redis2025) reportó que el 67% del costo operativo de inferencia en sistemas multi-herramienta se atribuye a la acumulación de contexto, no a la generación de respuestas nuevas. Desde la industria, [Vercel (2025)](#ref-vercel2025) documentó que su agente d0 con 17–18 herramientas alcanzaba una tasa de éxito del 80%, mientras que al reducir el catálogo a operaciones mínimas la tasa subió al 100%, con una reducción del 37% en tokens, mejora de 3.5× en velocidad y 42% menos pasos necesarios—evidencia de producción que cuantifica directamente el impacto del tool overload.

**Técnicas de Memoria y Gestión de Contexto**

**Clasificación de los Sistemas de Memoria en Agentes LLM**

Siguiendo la taxonomía propuesta por [Wang et al. (2024)](#ref-wang2024), los sistemas de memoria en agentes LLM se clasifican en cuatro categorías según su mecanismo de almacenamiento y recuperación: (a) memoria en contexto (in-context memory), que utiliza directamente el historial de conversación almacenado en la ventana de contexto del modelo; (b) memoria externa (external memory), que almacena información en bases de datos vectoriales o relacionales externas al modelo; (c) memoria en parámetros (in-weights memory), que codifica el conocimiento en los pesos del modelo mediante fine-tuning; y (d) memoria en caché (in-cache memory), que reutiliza estados de activación del modelo para acelerar la inferencia sobre prefijos repetidos.

Esta tesis se enfoca en las técnicas de memoria externa y en caché, ya que son las que pueden ser implementadas a nivel de agente sin modificar los parámetros del modelo base —condición necesaria dado el uso de APIs comerciales— y las que tienen mayor impacto directo sobre el fenómeno de context rot.

**Retrieval-Augmented Generation**

La Generación Aumentada por Recuperación (Retrieval-Augmented Generation, RAG; [Lewis et al., 2020](#ref-lewis2020)) es la técnica de memoria externa más ampliamente adoptada en sistemas de agentes LLM. En su formulación original, RAG combina un modelo de recuperación densa —que convierte la consulta del usuario en un vector de embeddings y busca los documentos más similares en una base de datos vectorial— con un modelo de generación que utiliza los documentos recuperados como contexto adicional para producir la respuesta.

En el contexto de agentes LLM multi-MCP, RAG puede aplicarse de dos formas complementarias: (a) RAG de historial de conversación, que recupera los turnos pasados más relevantes para la consulta actual en lugar de mantener el historial completo en el contexto; y (b) RAG-MCP ([Tang et al., 2025](#ref-tang2025)), que aplica recuperación semántica sobre el catálogo de herramientas MCP para exponer al modelo solo las herramientas más relevantes para cada consulta, mitigando el tool overload.

[Tang et al. (2025)](#ref-tang2025) evaluaron RAG-MCP en escenarios con catálogos de 128 herramientas y reportaron una reducción del 68% en el consumo de tokens de descripción de herramientas con una pérdida de exactitud inferior al 2% en tareas de selección de herramientas. Estos resultados sugieren que RAG aplicado al catálogo de herramientas es una de las técnicas de mayor potencial para mitigar el tool overload en arquitecturas multi-MCP.

**SessionFacts y Compresión de Estado de Sesión**

SessionFacts es un mecanismo de gestión de contexto que comprime el estado de una sesión de conversación en una estructura de hechos clave-valor, eliminando la redundancia del historial de conversación completo. La idea subyacente es análoga a la compresión de estados en sistemas de control: en lugar de mantener la trayectoria completa del sistema, se mantiene un resumen suficiente para continuar operando correctamente.

En la práctica, SessionFacts se implementa mediante un proceso de extracción periódica de hechos relevantes del historial de conversación: el agente invoca un paso de summarization que identifica las entidades, hechos y restricciones mencionados en los turnos pasados y los almacena como pares clave-valor en una estructura separada del contexto activo. Esta estructura se inyecta en el contexto del agente al inicio de cada nuevo turno, reemplazando el historial completo por un resumen compacto. [Packer et al. (2023)](#ref-packer2023) reportaron reducciones de hasta el 70% en el consumo de tokens de historial mediante técnicas similares en el sistema MemGPT.

**MemoryBank y Memoria a Largo Plazo**

MemoryBank ([Hu et al., 2023](#ref-hu2023)) es un sistema de memoria a largo plazo para agentes LLM que combina almacenamiento externo con un mecanismo de recuperación basado en relevancia y una política de olvido inspirada en la curva de Ebbinghaus. El sistema mantiene una base de datos de memorias —fragmentos de información extraídos de conversaciones pasadas— que son recuperadas selectivamente cuando su relevancia para la consulta actual supera un umbral definido.

La política de olvido de MemoryBank asigna a cada memoria un peso de relevancia que decrece exponencialmente con el tiempo transcurrido desde su última recuperación, reduciendo la probabilidad de recuperar información obsoleta sin eliminarla permanentemente. Esta característica es especialmente valiosa en conversaciones largas donde la relevancia de la información varía a lo largo del tiempo. [Hu et al. (2023)](#ref-hu2023) evaluaron MemoryBank en simulaciones de conversación de hasta 500 turnos y reportaron una mejora del 37% en la coherencia conversacional respecto a agentes sin memoria externa.

**Semantic Caching**

El caching semántico (semantic caching) es una técnica de memoria en caché que reutiliza respuestas previas del agente para consultas semánticamente equivalentes, evitando la inferencia completa del modelo para preguntas similares. A diferencia del caching exacto —que requiere coincidencia literal de la consulta— el caching semántico utiliza similaridad coseno entre vectores de embeddings para identificar consultas equivalentes, tolerando variaciones en la formulación.

Implementaciones como RedisVL (Redis Labs, 2025) almacenan pares (embedding de consulta, respuesta) en una base de datos vectorial con índices de búsqueda aproximada de vecinos más cercanos (ANN). Cuando la similitud coseno entre la consulta entrante y una consulta almacenada supera un umbral de configuración (típicamente 0.92–0.95), la respuesta almacenada se retorna directamente sin invocar el modelo. Esta técnica no reduce el context rot directamente, pero reduce el número de invocaciones de herramientas MCP necesarias, lo que disminuye la acumulación de observaciones en el contexto.

**Mem0 y Memoria Personalizada**

Mem0 ([Chhikara et al., 2025](#ref-chhikara2025)) es un sistema de memoria adaptativa para agentes LLM que combina recuperación vectorial con grafos de conocimiento para mantener un perfil de memoria personalizado por usuario y sesión. A diferencia de MemoryBank, que trata todas las memorias de forma uniforme, Mem0 distingue entre memorias de usuario (preferencias, contexto personal), memorias de agente (configuraciones, instrucciones aprendidas) y memorias de sesión (estado de la conversación actual), gestionando cada tipo con estrategias de almacenamiento y recuperación diferenciadas.

**Estrategias de Tool Gating**

**Definición y Motivación**

Las estrategias de tool gating (también denominadas deferred tool loading o dynamic tool selection) son mecanismos que controlan qué herramientas del catálogo MCP se exponen al modelo en cada turno de la conversación, en lugar de exponer el catálogo completo de forma estática desde el inicio de la sesión. El objetivo es reducir el overhead de tokens de descripción de herramientas y mejorar la señal-ruido en el contexto del modelo, lo que a su vez reduce el riesgo de selección incorrecta de herramientas y de alucinación de parámetros.

**Filtrado Semántico por Relevancia**

El filtrado semántico por relevancia es la variante más estudiada de tool gating. En esta técnica, la consulta del usuario se convierte en un vector de embeddings que se compara con los vectores de embeddings de las descripciones de las herramientas disponibles mediante similitud coseno. Las herramientas cuya similitud con la consulta supera un umbral configurable son expuestas al modelo; las restantes permanecen en el catálogo pero no ocupan tokens en el contexto activo.

[Tang et al. (2025)](#ref-tang2025) implementaron esta técnica en RAG-MCP y reportaron que la exposición selectiva de las k herramientas más relevantes (con k típicamente entre 3 y 10) preserva una exactitud de selección superior al 95% incluso cuando el catálogo total contiene 128 herramientas, con una reducción del 68% en el consumo de tokens de descripción. El umbral óptimo de similitud y el valor de k dependen del dominio de aplicación y deben calibrarse mediante validación cruzada. Es relevante señalar que la industria ha explorado también el enfoque inverso: en lugar de filtrar dinámicamente qué herramientas exponer, [Vercel (2025)](#ref-vercel2025) optó por eliminar permanentemente el 80% de las herramientas de su agente d0 y reemplazarlas por un conjunto mínimo de operaciones de sistema de archivos. Los resultados fueron similares en dirección: reducción del 37% en tokens y mejora de la tasa de éxito del 80% al 100%. La diferencia entre ambos enfoques es que el filtrado dinámico (RAG-MCP, tool gating semántico) es más aplicable en arquitecturas multi-MCP donde no es posible eliminar herramientas estáticamente sin perder funcionalidad, que es el escenario central de esta investigación.

**Carga Diferida de Herramientas**

La carga diferida (lazy loading) es una estrategia complementaria al filtrado semántico en la que las herramientas MCP no se cargan en el contexto del modelo hasta que el agente determina, mediante un paso de razonamiento previo, que son necesarias para la tarea actual. A diferencia del filtrado semántico —que es un proceso pasivo que ocurre antes de la generación del turno— la carga diferida implica un ciclo adicional de razonamiento: el agente primero razona sobre qué categorías de herramientas necesita, luego solicita al sistema de tool gating que cargue solo esas categorías, y finalmente ejecuta el razonamiento completo con las herramientas cargadas.

Esta técnica introduce latencia adicional (un ciclo de razonamiento extra) pero puede reducir significativamente el overhead de tokens en sesiones donde el agente utiliza herramientas de dominios muy diferentes en distintas fases de la conversación. Es especialmente adecuada para agentes conectados a servidores MCP de dominios heterogéneos, como el caso típico de un agente empresarial conectado simultáneamente a servidores de búsqueda, bases de datos, calendario y comunicaciones.

**Evaluación de Agentes LLM y Benchmarks de Referencia**

**Dimensiones de Evaluación**

La evaluación de agentes LLM es un campo activo de investigación que ha producido múltiples frameworks y benchmarks en los últimos años. Para el problema específico de esta tesis —la medición del context rot en agentes multi-MCP— las dimensiones de evaluación más relevantes son: (a) exactitud de la respuesta final respecto a un ground truth anotado; (b) tasa de alucinación factual, que mide la proporción de afirmaciones verificables en la respuesta que son incorrectas; (c) coherencia conversacional, que evalúa la consistencia de las respuestas del agente a lo largo de una conversación extendida; (d) exactitud en la selección de herramientas, que mide si el agente invoca la herramienta correcta con los parámetros correctos; y (e) eficiencia computacional, medida a través del consumo de tokens por turno y la latencia de generación.

**LongMemEval**

LongMemEval ([Truong & Ho, 2023](#ref-truong2023)) es un benchmark diseñado específicamente para evaluar la memoria a largo plazo de agentes LLM en conversaciones extendidas. El dataset contiene conversaciones sintéticas de hasta 500 turnos con preguntas que requieren recuperar información mencionada en turnos muy anteriores de la conversación. LongMemEval evalúa cinco capacidades de memoria: recuperación de información única (single-hop retrieval), razonamiento sobre múltiples hechos pasados (multi-hop reasoning), seguimiento de entidades a través del tiempo (entity tracking), razonamiento temporal (temporal reasoning) y detección de ausencia de información (absence of memory).

**LoCoMo**

LoCoMo ([Maharana et al., 2024](#ref-maharana2024)) es un benchmark de conversaciones largas que evalúa la capacidad de los agentes LLM para mantener coherencia y consistencia en diálogos de múltiples sesiones. A diferencia de LongMemEval, que se enfoca en la recuperación de hechos específicos, LoCoMo evalúa aspectos más sutiles de la coherencia conversacional: la consistencia del tono y la personalidad del agente, la coherencia entre afirmaciones hechas en diferentes puntos de la conversación, y la capacidad de actualizar correctamente las creencias del agente ante nueva información contradictoria. Este benchmark es especialmente relevante para evaluar los efectos de la mezcla de estados de sesión en arquitecturas multi-MCP.

**SimpleToolHalluBench**

SimpleToolHalluBench ([Zeng et al., 2025](#ref-zeng2025)) es un benchmark focalizado en la evaluación de alucinaciones en el uso de herramientas. El benchmark presenta al modelo catálogos de herramientas de diferentes tamaños y evalúa la tasa de alucinación en tres dimensiones: (a) alucinación de nombres de herramientas (el modelo invoca una herramienta que no existe en el catálogo); (b) alucinación de parámetros (el modelo especifica parámetros incorrectos para una herramienta existente); y (c) alucinación de valores (el modelo especifica valores de parámetros inválidos o fuera del rango aceptado). SimpleToolHalluBench es directamente aplicable al problema de tool overload estudiado en esta tesis.

**ToolBench y ToolHaystack**

ToolBench ([Qin et al., 2023](#ref-qin2023)) es un benchmark de evaluación de agentes LLM en tareas de uso de herramientas reales, que incluye más de 16,000 APIs de servicios web reales. Aunque su escala lo hace adecuado para evaluar la capacidad general de uso de herramientas, su complejidad lo hace menos adecuado para el control experimental requerido por esta tesis. ToolHaystack es una variante más reciente que evalúa específicamente la capacidad del modelo de encontrar y utilizar la herramienta correcta en catálogos de gran tamaño (haystack de herramientas), lo que lo hace directamente relevante para el problema de tool overload.

**Métricas Complementarias**

Además de los benchmarks específicos, la evaluación en esta tesis incorporará métricas computacionales complementarias. El consumo de tokens se medirá mediante los contadores nativos de la API de Anthropic, distinguiendo entre tokens de prompt (contexto) y tokens de completion (respuesta generada). La latencia se medirá como el tiempo de pared (wall-clock time) entre el envío de la solicitud y la recepción del primer token de respuesta (time-to-first-token, TTFT) y el tiempo total de generación. La coherencia conversacional se medirá mediante BERTScore ([Zhang et al., 2020](#ref-zhang2020)), que calcula la similitud semántica entre pares de enunciados utilizando representaciones contextuales de BERT.

**Síntesis del Marco Teórico**

Los siete bloques teóricos desarrollados en este capítulo convergen en una cadena causal que fundamenta el problema de investigación: los agentes LLM basados en transformer operan dentro de una ventana de contexto limitada; cuando se conectan a múltiples servidores MCP, los mecanismos de tool overload, acumulación de observaciones y mezcla de estados de sesión consumen progresivamente el contexto disponible y degradan la calidad de las respuestas (context rot); las técnicas de memoria externa —RAG, SessionFacts, MemoryBank, semantic caching— y las estrategias de tool gating constituyen intervenciones de software que pueden mitigar esta degradación; y los benchmarks LongMemEval, LoCoMo y SimpleToolHalluBench, junto con las métricas de exactitud, coherencia, alucinación y consumo de tokens, proporcionan los instrumentos de medición necesarios para cuantificar el impacto de dichas intervenciones.

Esta cadena causal es la base sobre la que se construyen las hipótesis de la investigación (DOC-13) y el diseño experimental (desarrollado en el capítulo de metodología), garantizando la coherencia entre el marco teórico, el problema, los objetivos y el método.

**2.8 Harness Engineering como Marco Unificador**

[Zhou et al. (2026)](#ref-zhou2026) proponen el paradigma de la externalización como marco para explicar la evolución de los agentes LLM: el progreso práctico ya no depende principalmente de mejorar los pesos del modelo sino de reorganizar la infraestructura de ejecución que lo rodea. Las capacidades que antes se esperaba que el modelo recuperara internamente ahora se externalizan en módulos especializados que componen el entorno del agente.

El paper distingue cuatro formas de externalización: (a) la memoria, que externaliza el estado a través del tiempo; (b) las skills, que externalizan el conocimiento procedural; (c) los protocolos, que externalizan la estructura de interacción; y (d) el harness engineering, que actúa como capa de coordinación gobernada de todas las anteriores.

La tesis sitúa su contribución en la tercera era de este paradigma — la era del harness —, generando evidencia empírica cuantitativa sobre qué combinaciones de capas de memoria y protocolo minimizan el context rot en escenarios multi-MCP. Los resultados informan el diseño de harnesses efectivos para entornos multi-servidor en producción.

**Referencias**

<a id="ref-anil2023"></a>
Anil, R., Chowdhery, A., Roberts, A., Askell, A., Brants, T., Fawcett, M., Gauthier, A., Ghafouri, A., Gustavsson, A., Hagberg, P., Hoang, L., Krikun, M., Liang, C., Maystre, L., McMahan, B., Misra, I., Narang, S., Niang, F., & Dean, J. (2023). Gemini: A family of highly capable multimodal models. arXiv. [https://arxiv.org/abs/2312.11805](https://arxiv.org/abs/2312.11805)

<a id="ref-anthropic2024"></a>
Anthropic. (2024). Model Context Protocol specification (v1.0). Anthropic. [https://modelcontextprotocol.io/specification](https://modelcontextprotocol.io/specification)

<a id="ref-brown2020"></a>
Brown, T. B., Mann, B., Ryder, N., Subbiah, M., Kaplan, J., Dhariwal, P., Neelakantan, A., Shyam, P., Sastry, G., Askell, A., Agarwal, S., Herbert-Voss, A., Krueger, G., Henighan, T., Child, R., Ramesh, A., Ziegler, D. M., Wu, J., Winter, C., … Amodei, D. (2020). Language models are few-shot learners. Advances in Neural Information Processing Systems, 33, 1877–1901. [https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html](https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html)

<a id="ref-chhikara2025"></a>
Chhikara, P., Singh, D., Gupta, T., Goyal, A., & Tiwari, A. (2025). Mem0: Building production-ready AI agents with scalable long-term memory. arXiv. [https://arxiv.org/abs/2504.19413](https://arxiv.org/abs/2504.19413)

<a id="ref-chroma2025"></a>
Chroma Research. (2025). Context rot in production LLM systems: A benchmark study. Chroma. [https://www.trychroma.com/blog/context-rot](https://www.trychroma.com/blog/context-rot)

<a id="ref-hong2023"></a>
Hong, S., Zhuge, M., Chen, J., Zheng, X., Cheng, Y., Zhang, C., Wang, J., Wang, Z., Yau, S. K. S., Lin, Z., Zhou, L., Ran, C., Xiao, L., Wu, C., & Schmidhuber, J. (2023). MetaGPT: Meta programming for a multi-agent collaborative framework. arXiv. [https://arxiv.org/abs/2308.00352](https://arxiv.org/abs/2308.00352)

<a id="ref-hu2023"></a>
Hu, J., Huang, S., Luo, Y., Wu, F., & Lam, W. (2023). MemoryBank: Enhancing large language models with long-term memory. arXiv. [https://arxiv.org/abs/2305.10250](https://arxiv.org/abs/2305.10250)

<a id="ref-lewis2020"></a>
Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. Advances in Neural Information Processing Systems, 33, 9459–9474. [https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html](https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html)

<a id="ref-liu2023"></a>
Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2023). Lost in the middle: How language models use long contexts. Transactions of the Association for Computational Linguistics, 12, 157–173. [https://doi.org/10.1162/tacl\_a\_00638](https://doi.org/10.1162/tacl\_a\_00638)

<a id="ref-maharana2024"></a>
Maharana, A., Lee, D.-H., Tulyakov, S., Bansal, M., Barbieri, F., & Fang, Y. (2024). Evaluating very long-term conversational memory of LLM agents. arXiv. [https://arxiv.org/abs/2402.17753](https://arxiv.org/abs/2402.17753)

<a id="ref-openai2023"></a>
OpenAI. (2023). Function calling in the API. OpenAI. [https://platform.openai.com/docs/guides/function-calling](https://platform.openai.com/docs/guides/function-calling)

<a id="ref-ouyang2022"></a>
Ouyang, L., Wu, J., Jiang, X., Almeida, D., Wainwright, C. L., Mishkin, P., Zhang, C., Agarwal, S., Slama, K., Ray, A., Schulman, J., Hilton, J., Kelton, F., Miller, L., Simens, M., Askell, A., Welinder, P., Christiano, P., Leike, J., & Lowe, R. (2022). Training language models to follow instructions with human feedback. Advances in Neural Information Processing Systems, 35, 27730–27744. [https://proceedings.neurips.cc/paper\_files/paper/2022/hash/b1efde53be364a73914f58805a001731-Abstract-Conference.html](https://proceedings.neurips.cc/paper\_files/paper/2022/hash/b1efde53be364a73914f58805a001731-Abstract-Conference.html)

<a id="ref-packer2023"></a>
Packer, C., Wooders, S., Lin, K., Fang, V., Patil, S. G., Stoica, I., & Gonzalez, J. E. (2023). MemGPT: Towards LLMs as operating systems. arXiv. [https://arxiv.org/abs/2310.08560](https://arxiv.org/abs/2310.08560)

<a id="ref-patil2023"></a>
Patil, S. G., Zhang, T., Wang, X., & Gonzalez, J. E. (2023). Gorilla: Large language model connected with massive APIs. arXiv. [https://arxiv.org/abs/2305.15334](https://arxiv.org/abs/2305.15334)

<a id="ref-qin2023"></a>
Qin, Y., Liang, S., Ye, Y., Zhu, K., Yan, L., Lu, Y., Lin, Y., Cong, X., Tang, X., Qian, B., Zhao, S., Hong, L., Tian, R., Xie, R., Zhou, J., Gerstein, M., Li, D., Liu, Z., & Sun, M. (2023). ToolLLM: Facilitating large language models to master 16000+ real-world APIs. arXiv. [https://arxiv.org/abs/2307.16789](https://arxiv.org/abs/2307.16789)

<a id="ref-redis2025"></a>
Redis Labs. (2025). Enterprise AI deployment patterns: Token consumption and memory management. Redis. [https://redis.io/blog/enterprise-ai-memory-2025](https://redis.io/blog/enterprise-ai-memory-2025)

<a id="ref-vercel2025"></a>
Vercel. (2025, diciembre). We removed 80% of our agent’s tools. Vercel Engineering Blog. [https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools](https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools)

<a id="ref-schick2023"></a>
Schick, T., Dwivedi-Yu, J., Dessì, R., Raileanu, R., Lomeli, M., Zettlemoyer, L., Cancedda, N., & Scialom, T. (2023). Toolformer: Language models can teach themselves to use tools. Advances in Neural Information Processing Systems, 36. [https://arxiv.org/abs/2302.04761](https://arxiv.org/abs/2302.04761)

<a id="ref-shi2023"></a>
Shi, F., Chen, X., Misra, K., Scales, N., Dohan, D., Chi, E., Schärli, N., & Zhou, D. (2023). Large language models can be easily distracted by irrelevant context. Proceedings of the 40th International Conference on Machine Learning, 202, 31210–31227. [https://proceedings.mlr.press/v202/shi23a.html](https://proceedings.mlr.press/v202/shi23a.html)

<a id="ref-tang2025"></a>
Tang, R., Jin, Z., Alexandrov, A., Shao, Y., Shi, P., & Pan, L. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. arXiv. [https://arxiv.org/abs/2502.03415](https://arxiv.org/abs/2502.03415)

<a id="ref-touvron2023"></a>
Touvron, H., Lavril, T., Izacard, G., Martinet, X., Lachaux, M.-A., Lacroix, T., Rozière, B., Goyal, N., Hambro, E., Azhar, F., Rodriguez, A., Joulin, A., Grave, E., & Lample, G. (2023). LLaMA: Open and efficient foundation language models. arXiv. [https://arxiv.org/abs/2302.13971](https://arxiv.org/abs/2302.13971)

<a id="ref-truong2023"></a>
Truong, T. H., & Ho, T. B. (2023). LongMemEval: Benchmarking long-context language models on long-term interactive memory. arXiv. [https://arxiv.org/abs/2410.10813](https://arxiv.org/abs/2410.10813)

<a id="ref-vaswani2017"></a>
Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is all you need. Advances in Neural Information Processing Systems, 30. [https://proceedings.neurips.cc/paper\_files/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html](https://proceedings.neurips.cc/paper\_files/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html)

<a id="ref-wang2024"></a>
Wang, L., Ma, C., Feng, X., Zhang, Z., Yang, H., Zhang, J., Chen, Z., Tang, J., Chen, X., Lin, Y., Zhao, W. X., Wei, Z., & Wen, J.-R. (2024). A survey on large language model based autonomous agents. Frontiers of Computer Science, 18(6), 186345. [https://doi.org/10.1007/s11704-024-40231-1](https://doi.org/10.1007/s11704-024-40231-1)

<a id="ref-wei2022"></a>
Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). Chain-of-thought prompting elicits reasoning in large language models. Advances in Neural Information Processing Systems, 35, 24824–24837. [https://proceedings.neurips.cc/paper\_files/paper/2022/hash/9d5609613524ecf4f15af0f7b31abca4-Abstract-Conference.html](https://proceedings.neurips.cc/paper\_files/paper/2022/hash/9d5609613524ecf4f15af0f7b31abca4-Abstract-Conference.html)

<a id="ref-yao2022"></a>
Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. arXiv. [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)

<a id="ref-zeng2025"></a>
Zeng, Z., Liu, M., Lu, R., Wang, B., Liu, X., & Cheng, X. (2025). SimpleToolHalluBench: Towards a comprehensive assessment of tool call hallucination in large language models. arXiv. [https://arxiv.org/abs/2501.13395](https://arxiv.org/abs/2501.13395)

<a id="ref-zhang2020"></a>
Zhang, T., Kishore, V., Wu, F., Weinberger, K. Q., & Artzi, Y. (2020). BERTScore: Evaluating text generation with BERT. International Conference on Learning Representations. [https://openreview.net/forum?id=SkeHuCVFDr](https://openreview.net/forum?id=SkeHuCVFDr)

<a id="ref-zhou2026"></a>
Zhou, C., Chai, H., Chen, W., Guo, Z., Shan, R., Song, Y., Xu, T., Yang, Y., Yu, A., Zhang, W., Zheng, C., Zhu, J., Zheng, Z., Zhang, Z., Lou, X., Zhang, C., Fu, Z., Wang, J., Liu, W., Lin, J., & Zhang, W. (2026). Externalization in LLM agents: A unified review of memory, skills, protocols and harness engineering. arXiv:2604.08224. [https://doi.org/10.48550/arXiv.2604.08224](https://doi.org/10.48550/arXiv.2604.08224)
