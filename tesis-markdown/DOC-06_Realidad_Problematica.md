# DOC-06 — Realidad Problemática

> **Tipo:** Tesis — Capítulo I  
> **Descripción:** Análisis del problema a nivel global y nacional: adopción de IA generativa y context rot.

---

**Medición del Impacto de Técnicas de Memoria y Gestión de Contexto sobre la Degradación de Respuestas en Agentes LLM Conectados a Múltiples Servidores MCP**

Edinson Núñez

\[Facultad / Escuela Profesional\]

\[Universidad\]

\[Asesor de Tesis\]

Abril 2026

**Capítulo I: Planteamiento del Problema**

**Realidad Problemática**

**La Expansión Global de la Inteligencia Artificial Generativa**

La inteligencia artificial generativa ha experimentado una expansión sin precedentes en los últimos años, transformando de forma estructural la manera en que organizaciones y personas interactúan con los sistemas computacionales. De acuerdo con [Microsoft (2025)](#ref-microsoft2025), la adopción global de herramientas de inteligencia artificial creció más del 80% entre octubre de 2024 y mediados de 2025, con aproximadamente una de cada seis personas en el mundo utilizando activamente herramientas de IA generativa. En el ámbito empresarial, la adopción de IA a nivel global alcanzó el 78% de las organizaciones en 2024, con el 92% de las empresas Fortune 500 reportando el uso activo de IA generativa en sus flujos de trabajo (Menlo Ventures, 2025).

El gasto global en IA generativa a nivel empresarial ascendió a 37 mil millones de dólares en 2025, frente a 11.5 mil millones en 2024, lo que representa un crecimiento de 3.2 veces en un solo año (Menlo Ventures, 2025). El mercado de modelos de lenguaje de gran escala (LLM) para aplicaciones empresariales, valorado en 8.8 mil millones de dólares en 2025, proyecta alcanzar 71.1 mil millones de dólares en 2034, con una tasa de crecimiento anual compuesta del 26.1% (Global Market Insights, 2025). Este crecimiento no es solo en experimentación: las organizaciones pusieron 11 veces más modelos de IA en producción en 2025 en comparación con el año anterior ([Databricks, 2025](#ref-databricks2025)), lo que evidencia una transición del piloto al despliegue operativo real.

Sin embargo, este crecimiento viene acompañado de advertencias serias sobre la viabilidad de los proyectos agentes en producción. [Gartner (2025)](#ref-gartner2025) predice que más del 40% de los proyectos de IA agéntica serán cancelados antes de 2027 por costos escalantes y complejidad técnica de despliegue, lo que subraya la necesidad de evidencia empírica sobre qué diseños de agente son más robustos en producción.

En el centro de esta transformación se encuentran los modelos de lenguaje de gran escala (LLM), sistemas de inteligencia artificial basados en arquitecturas transformer que han demostrado capacidades sorprendentes de razonamiento, generación de texto y resolución de problemas complejos ([Vaswani et al., 2017](#ref-vaswani2017)). Sin embargo, la evolución más significativa de los últimos dos años no ha sido la mejora de los modelos en sí, sino la arquitectura de los sistemas que los rodean: los agentes LLM, sistemas que dotan a estos modelos de herramientas externas, capacidad de planificación y memoria persistente ([Yao et al., 2022](#ref-yao2022); [Schick et al., 2023](#ref-schick2023)).

**El Surgimiento del Model Context Protocol y los Agentes Multi-Herramienta**

La evolución de los agentes LLM hacia sistemas conectados a múltiples fuentes de datos y herramientas externas culminó, en noviembre de 2024, con la publicación del Model Context Protocol (MCP) por parte de Anthropic. El MCP es un estándar abierto que define la manera en que los asistentes de IA se integran con repositorios de contenido, herramientas de gestión empresarial y entornos de desarrollo, mediante una arquitectura de tres capas: el host que coordina la conversación, los clientes que mantienen sesiones individuales con cada servidor, y los servidores que exponen herramientas, recursos y prompts al modelo ([Anthropic, 2024](#ref-anthropic2024)). Su adopción fue inmediata: en los primeros seis meses tras su publicación, cientos de organizaciones publicaron servidores MCP para calendarios, bases de datos, sistemas de gestión de proyectos, repositorios de código, herramientas de análisis de datos y servicios de comunicación.

Este fenómeno ha generado un escenario operativo inédito: agentes LLM conectados simultáneamente a cinco, diez o más servidores MCP, cada uno con su propio catálogo de herramientas y recursos. [Anthropic (2024)](#ref-anthropic2024) documenta despliegues en producción con cientos o miles de herramientas disponibles, donde solo las definiciones de las herramientas pueden consumir decenas de miles de tokens antes de que el agente procese la consulta real del usuario. Este escenario representa una amenaza directa a la calidad y eficiencia de los sistemas basados en LLM.

**El Problema Técnico: La Degradación Contextual (Context Rot)**

***Naturaleza y Magnitud del Fenómeno***

La investigación reciente ha comenzado a caracterizar con precisión un fenómeno que los profesionales del campo ya observaban en la práctica: la degradación progresiva de la calidad de las respuestas de los agentes LLM conforme crece el contenido de su contexto de entrada. [Chroma Research (2025)](#ref-chroma2025) denominó este fenómeno context rot y documentó que la precisión de los modelos se degrada más del 30% en posiciones intermedias de la ventana de contexto en los 18 modelos de frontera evaluados, incluso cuando todos los tokens relevantes están presentes en el contexto. Este hallazgo es particularmente relevante porque ocurre independientemente del tamaño de la ventana de contexto del modelo: no es un problema de capacidad de almacenamiento, sino de procesamiento desigual de la información.

Investigaciones adicionales han confirmado y ampliado este hallazgo. Un estudio controlado sobre cinco modelos de código abierto y propietarios en tareas de matemáticas, respuesta a preguntas y generación de código demostró que el rendimiento se degrada sustancialmente al aumentar la longitud de la entrada, incluso cuando el modelo puede recuperar perfectamente todos los tokens relevantes (arXiv, 2025). [Redis Labs (2025)](#ref-redis2025) documenta que las consultas empresariales consumen entre 50,000 y 100,000 tokens antes de que el modelo empiece a razonar, con la calidad de los metadatos —no el tamaño del contexto— como la restricción real de rendimiento. Se estima que más del 40% de los fallos en proyectos de IA se deben no al modelo en sí, sino a un contexto de mala calidad o irrelevante ([IntuitionLabs, 2025](#ref-intuitionlabs2025)). La evidencia proveniente de entornos de producción refuerza estos hallazgos: [Vercel (2025)](#ref-vercel2025) documentó que al reducir el catálogo de herramientas de su agente interno d0 de 17–18 herramientas a un conjunto mínimo de operaciones de sistema de archivos, la tasa de éxito pasó del 80% al 100%, el consumo de tokens se redujo en un 37%, la velocidad de respuesta mejoró 3.5 veces y el número de pasos necesarios disminuyó en un 42%. Este caso ilustra que la sobrecarga del catálogo de herramientas no es un problema teórico: tiene consecuencias operativas directas y medibles en sistemas de producción real.

***Manifestaciones Específicas en Arquitecturas Multi-MCP***

En el contexto específico de agentes LLM conectados a múltiples servidores MCP, el context rot se manifiesta a través de tres mecanismos interrelacionados. El primero es la sobrecarga de herramientas: Gan y Sun (2025) demostraron experimentalmente que, cuando el catálogo de herramientas disponibles supera cierto umbral, la tasa de selección correcta cae del 100% hacia el 13.62% en el baseline sin técnicas de mitigación. [Zhang et al. (2024)](#ref-zhang2024) documentaron que modelos avanzados como GPT-4o y Gemini-1.5-Pro solo alcanzan puntajes de 37.0 y 45.3 sobre 100, respectivamente, en la detección de situaciones donde la herramienta necesaria está ausente del catálogo disponible.

El segundo mecanismo es la acumulación no controlada de resultados intermedios: cada llamada a una herramienta MCP devuelve datos que se incorporan al contexto del modelo, incrementando el costo de procesamiento y diluyendo la señal relevante para la consulta actual ([LangChain, 2024](#ref-langchain2024)). En conversaciones largas con múltiples llamadas a herramientas, este efecto se acumula de forma que el modelo pierde capacidad de atender los tokens más relevantes para la consulta presente ([Wu et al., 2024](#ref-wu2024); [Maharana et al., 2024](#ref-maharana2024)).

El tercer mecanismo es la mezcla no estructurada de memorias: en ausencia de una arquitectura de memoria deliberada, las preferencias del usuario, los hechos operacionales, los resultados de herramientas previas y el estado conversacional actual se almacenan en la misma estructura sin diferenciación, generando contradicciones, staleness —datos desactualizados que el modelo trata como vigentes— y pérdida de coherencia entre sesiones ([Kirmayr et al., 2025](#ref-kirmayr2025); [Zhong et al., 2023](#ref-zhong2023); [Packer et al., 2023](#ref-packer2023)).

**El Estado Incompleto de las Técnicas de Mitigación**

La literatura científica ha comenzado a proponer y validar técnicas para mitigar el context rot, pero de forma fragmentada, cada trabajo abordando una sola dimensión del problema. Gan y Sun (2025) proponen RAG-MCP, una técnica de recuperación semántica sobre catálogos de herramientas que reduce el prompt en más del 50% y triplica la precisión de selección. [Chhikara et al. (2025)](#ref-chhikara2025) presentan Mem0, una capa de memoria longitudinal que reduce la latencia en el percentil 95 en un 91% y el costo de tokens en más del 90%. [Kirmayr et al. (2025)](#ref-kirmayr2025) demuestran que organizar la memoria por categorías predefinidas reduce significativamente las contradicciones y redundancias. [Packer et al. (2023)](#ref-packer2023) establecen el paradigma de gestión virtual de contexto inspirado en sistemas operativos, que permite a los LLM operar sobre información que excede su ventana de contexto inmediata.

Sin embargo, existe una brecha crítica en la literatura: ningún trabajo experimental mide el impacto combinado de múltiples técnicas sobre un agente LLM conectado a múltiples servidores MCP, ni lo hace usando el costo de tokens y la latencia de respuesta como variables dependientes primarias. Los benchmarks existentes —LongMemEval ([Wu et al., 2024](#ref-wu2024)), LoCoMo ([Maharana et al., 2024](#ref-maharana2024)) y ToolHaystack (2025)— miden dimensiones específicas del problema pero no su manifestación integrada en arquitecturas multi-MCP reales. Esta brecha es el punto de partida de la presente investigación.

**Realidad Problemática en el Contexto Nacional (Perú)**

**El Avance de la Transformación Digital en el Perú**

El Perú ha experimentado en los últimos años un avance significativo en su proceso de transformación digital, tanto en el sector privado como en el sector público. Según el Diario Oficial El Peruano (2024), el 76% de las empresas peruanas ha iniciado su proceso de transformación digital, un incremento sustancial frente al 34% registrado en 2021 y al 65% en 2022. Las áreas prioritarias de inversión son operaciones (81%) y tecnología (73%), lo que refleja una orientación hacia la automatización y optimización de procesos (EY Perú, 2024).

En el plano de la adopción de inteligencia artificial específicamente, las organizaciones peruanas invirtieron 50.1 millones de dólares en IA en 2024, con un crecimiento del 38.4% respecto al año anterior, con el 82.2% de esa inversión dirigida a soluciones de IA desarrolladas a medida (Visual ERP, 2025). A nivel de preparación gubernamental, el Perú se ubica en el puesto 60 del índice global de preparación gubernamental para la inteligencia artificial de Oxford Insights, siendo el quinto país de la región latinoamericana en ese ranking y superando a Colombia, Ecuador y México (Prensa Perú, 2025). En el Índice Latinoamericano de Inteligencia Artificial, el Perú avanzó de la octava posición en 2024 a la séptima en 2025, con una puntuación de 51.93 sobre 100 (ILIA, 2025).

Desde el ámbito del Estado, se han documentado 22 aplicaciones de inteligencia artificial implementadas en 17 entidades públicas peruanas, constituyendo lo que investigadores de la Universidad de Lima denominan la primera cartografía del ecosistema operativo de IA en la administración pública peruana (Revista Interfases, 2025). El gobierno peruano, a través de la Secretaría de Gobierno y Transformación Digital, ha establecido la plataforma IA Perú (gob.pe/iaperu) como punto de articulación de la política nacional de inteligencia artificial.

**Brechas y Desafíos Específicos del Contexto Peruano**

A pesar de los avances descritos, el Perú enfrenta desafíos específicos que hacen especialmente relevante la investigación sobre técnicas de optimización de sistemas LLM. En primer lugar, existe una brecha significativa en el uso avanzado de herramientas de IA: mientras que en Chile y Colombia el 17-18% de los usuarios reporta usar herramientas de IA de forma avanzada, en el Perú este porcentaje es solo el 6% (EY Perú, 2024). Esta brecha refleja una adopción predominantemente superficial de la tecnología, con uso limitado de las capacidades más sofisticadas, incluidos los agentes LLM con herramientas externas.

En segundo lugar, la infraestructura digital presenta disparidades importantes: según el Instituto Nacional de Estadística e Informática (INEI, 2024), solo el 58.4% de los hogares a nivel nacional cuenta con servicio de internet fijo, cifra que cae al 21.7% en los hogares rurales. Esta brecha de conectividad impone restricciones prácticas sobre el despliegue de sistemas de IA que dependen de comunicación continua con APIs remotas, como es el caso de los agentes LLM basados en MCP.

En tercer lugar, el principal obstáculo para la transformación digital reportado por las empresas peruanas no es tecnológico sino cultural y de capacidades: el 56% de las empresas identifica la cultura organizacional como el principal freno, seguido de la falta de habilidades digitales (EY Perú, 2024). En este contexto, el costo operativo de los sistemas de IA —expresado en costo de tokens y latencia— adquiere especial relevancia: sistemas más eficientes son más accesibles para organizaciones con presupuestos de tecnología limitados.

**La Relevancia de la Investigación para el Contexto Peruano**

La conjunción de los tres factores descritos —la acelerada adopción de IA generativa, la brecha en uso avanzado y las limitaciones de infraestructura y presupuesto— hace que el problema del context rot en agentes LLM multi-MCP sea especialmente relevante para el contexto peruano y latinoamericano. Las organizaciones que adoptan estos sistemas en etapas tempranas de madurez digital son particularmente vulnerables a los efectos del context rot: carecen de los procesos de monitoreo y optimización que las organizaciones tecnológicamente maduras han desarrollado, y son más sensibles al impacto económico del consumo excesivo de tokens y la latencia elevada.

La ausencia de investigación primaria en español sobre técnicas de memoria y mitigación del context rot en agentes LLM representa, además, una brecha específica del ecosistema científico hispanohablante. No se identificaron tesis doctorales, artículos de revistas indexadas ni ponencias en congresos iberoamericanos que aborden este problema de forma experimental y cuantitativa. La presente investigación tiene, por tanto, una doble contribución: empírica, al generar evidencia cuantitativa sobre el fenómeno en condiciones controladas; y contextual, al hacerlo desde y para el ecosistema tecnológico latinoamericano.

En síntesis, la realidad problemática evidencia que el context rot en agentes LLM conectados a múltiples servidores MCP es un problema técnico con consecuencias prácticas directas —en calidad de servicio, costo operativo y confiabilidad— que afecta a organizaciones de todo el mundo y que adquiere características específicas en el contexto de la transformación digital peruana. La investigación propuesta aborda esta brecha de forma sistemática, empírica y reproducible.

**Referencias**

<a id="ref-anthropic2024"></a>
Anthropic. (2024). Model Context Protocol specification. [https://modelcontextprotocol.io/specification/2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25)

<a id="ref-chroma2025"></a>
Chroma Research. (2025). Context rot: How increasing input tokens impacts LLM performance. [https://research.trychroma.com/context-rot](https://research.trychroma.com/context-rot)

<a id="ref-chhikara2025"></a>
Chhikara, P., Singh, T., Yadav, D., Nie, N., & Doerr, T. (2025). Mem0: Building production-ready AI agents with scalable long-term memory. arXiv. [https://arxiv.org/abs/2504.19413](https://arxiv.org/abs/2504.19413)

<a id="ref-databricks2025"></a>
Databricks. (2025). State of AI: Enterprise adoption & growth trends. [https://www.databricks.com/blog/state-ai-enterprise-adoption-growth-trends](https://www.databricks.com/blog/state-ai-enterprise-adoption-growth-trends)

<a id="ref-diario2024"></a>
Diario Oficial El Peruano. (2024). Transformación digital: 72% de las empresas en el Perú comenzará este proceso en el 2024. [https://elperuano.pe/noticia/235308-transformacion-digital-72-de-las-empresas-en-el-peru-comenzara-este-proceso-en-el-2024](https://elperuano.pe/noticia/235308-transformacion-digital-72-de-las-empresas-en-el-peru-comenzara-este-proceso-en-el-2024)

<a id="ref-ey2024"></a>
EY Perú. (2024). Nuevos horizontes de la madurez digital en el Perú 2024. EY. [https://www.ey.com/es\_pe/insights/revista-execution/central/inteligencia-artificial-hispanoamerica](https://www.ey.com/es\_pe/insights/revista-execution/central/inteligencia-artificial-hispanoamerica)

<a id="ref-gan2025"></a>
Gan, T., & Sun, Q. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. arXiv. [https://arxiv.org/abs/2505.03275](https://arxiv.org/abs/2505.03275)

<a id="ref-gartner2025"></a>
Gartner. (2025, junio 25). Gartner predicts over 40 percent of agentic AI projects will be canceled by end of 2027 \[Press release\]. [https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027](https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027)

<a id="ref-global2025"></a>
Global Market Insights. (2025). Enterprise LLM market size & share, statistics report 2025–2034. [https://www.gminsights.com/industry-analysis/enterprise-llm-market](https://www.gminsights.com/industry-analysis/enterprise-llm-market)

<a id="ref-intuitionlabs2025"></a>
IntuitionLabs. (2025). What is context engineering? A guide for AI & LLMs. [https://intuitionlabs.ai/articles/what-is-context-engineering](https://intuitionlabs.ai/articles/what-is-context-engineering)

<a id="ref-instituto2024"></a>
Instituto Nacional de Estadística e Informática. (2024). Estadísticas de tecnologías de información y comunicaciones en los hogares. INEI.

<a id="ref-kirmayr2025"></a>
Kirmayr, J., Stappen, L., Schneider, P., Matthes, F., & André, E. (2025). CarMem: Enhancing long-term memory in LLM voice assistants through category-bounding. En Proceedings of COLING 2025: Industry Track. ACL Anthology. [https://arxiv.org/abs/2501.09645](https://arxiv.org/abs/2501.09645)

<a id="ref-langchain2024"></a>
LangChain. (2024). LangGraph: State management and agent orchestration \[Documentación técnica\]. LangChain Inc. [https://langchain-ai.github.io/langgraph/](https://langchain-ai.github.io/langgraph/)

<a id="ref-maharana2024"></a>
Maharana, A., Lee, D.-H., Tulyakov, S., Bansal, M., Barbieri, F., & Fang, Y. (2024). Evaluating very long-term conversational memory of LLM agents. En Proceedings of ACL 2024 (pp. 13851–13870). [https://arxiv.org/abs/2402.17753](https://arxiv.org/abs/2402.17753)

<a id="ref-menlo2025"></a>
Menlo Ventures. (2025). 2025: The state of generative AI in the enterprise. [https://menlovc.com/perspective/2025-the-state-of-generative-ai-in-the-enterprise/](https://menlovc.com/perspective/2025-the-state-of-generative-ai-in-the-enterprise/)

<a id="ref-microsoft2025"></a>
Microsoft. (2025). Global AI adoption in 2025. AI Economy Institute. [https://www.microsoft.com/en-us/corporate-responsibility/topics/ai-economy-institute/reports/global-ai-adoption-2025/](https://www.microsoft.com/en-us/corporate-responsibility/topics/ai-economy-institute/reports/global-ai-adoption-2025/)

<a id="ref-oxford2024"></a>
Oxford Insights. (2024). Government AI readiness index 2024. Oxford Insights.

<a id="ref-packer2023"></a>
Packer, C., Fang, V., Patil, S. G., Lin, K., Wooders, S., & Gonzalez, J. (2023). MemGPT: Towards LLMs as operating systems. arXiv. [https://arxiv.org/abs/2310.08560](https://arxiv.org/abs/2310.08560)

<a id="ref-prensa2025"></a>
Prensa Perú. (2025). Índice de preparación de los gobiernos para la inteligencia artificial 2024. [https://prensaperu.pe/2025/03/29/indice-de-preparacion-de-los-gobiernos-para-la-inteligencia-artificial-2024](https://prensaperu.pe/2025/03/29/indice-de-preparacion-de-los-gobiernos-para-la-inteligencia-artificial-2024)

<a id="ref-redis2025"></a>
Redis Labs. (2025). Context window overflow: Breaking the barrier. [https://redis.io/blog/context-window-overflow/](https://redis.io/blog/context-window-overflow/)

<a id="ref-vercel2025"></a>
Vercel. (2025, diciembre). We removed 80% of our agent’s tools. Vercel Engineering Blog. [https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools](https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools)

<a id="ref-revista2025"></a>
Revista Interfases. (2025). Implementación de inteligencia artificial en el Estado peruano: catálogo analítico de aplicaciones. Universidad de Lima. [https://revistas.ulima.edu.pe/index.php/Interfases/article/view/8263](https://revistas.ulima.edu.pe/index.php/Interfases/article/view/8263)

<a id="ref-schick2023"></a>
Schick, T., Dwivedi-Yu, J., Dessì, R., Raileanu, R., Lomeli, M., Zettlemoyer, L., Cancedda, N., & Scialom, T. (2023). Toolformer: Language models can teach themselves to use tools. En Advances in Neural Information Processing Systems (NeurIPS 2023). [https://arxiv.org/abs/2302.04761](https://arxiv.org/abs/2302.04761)

<a id="ref-vaswani2017"></a>
Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is all you need. En Advances in Neural Information Processing Systems (Vol. 30). [https://arxiv.org/abs/1706.03762](https://arxiv.org/abs/1706.03762)

<a id="ref-visual2025"></a>
Visual ERP. (2025). Inteligencia artificial en empresas peruanas 2025. [https://grupovisualcont.com/noticias/inteligencia-artificial-en-empresas-peruanas-2025/](https://grupovisualcont.com/noticias/inteligencia-artificial-en-empresas-peruanas-2025/)

<a id="ref-wu2024"></a>
Wu, D., Wang, H., Yu, W., Zhang, Y., Chang, K.-W., & Yu, D. (2024). LongMemEval: Benchmarking chat assistants on long-term interactive memory. arXiv. [https://arxiv.org/abs/2410.10813](https://arxiv.org/abs/2410.10813)

<a id="ref-yao2022"></a>
Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. arXiv. [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)

<a id="ref-zhang2024"></a>
Zhang, Y., et al. (2024). ToolBeHonest: A multi-level hallucination diagnostic benchmark for tool-augmented large language models. arXiv. [https://arxiv.org/abs/2406.20015](https://arxiv.org/abs/2406.20015)

<a id="ref-zhong2023"></a>
Zhong, W., Guo, L., Gao, Q., Ye, H., & Wang, Y. (2023). MemoryBank: Enhancing large language models with long-term memory. arXiv. [https://arxiv.org/abs/2305.10250](https://arxiv.org/abs/2305.10250)
