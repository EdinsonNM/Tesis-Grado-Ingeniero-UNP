# DOC-13 — Hipótesis

> **Tipo:** Tesis — Capítulo I  
> **Descripción:** Hipótesis general y específicas con variables dependientes, independientes e indicadores.

---

Medición del Impacto de Técnicas de Memoria y Gestión de Contexto

sobre la Degradación de Respuestas en Agentes LLM

Conectados a Múltiples Servidores MCP

**DOC-13: Hipótesis General y Específicas**

Edinson Núñez

Tesis de Maestría

2026

**Hipótesis de la Investigación**

Las hipótesis de investigación son proposiciones tentativas sobre la relación entre las variables del estudio, formuladas de manera precisa y verificable, cuya validez o rechazo se determinará mediante el análisis de los datos experimentales. En el presente capítulo se formulan la hipótesis general y las cinco hipótesis específicas de la investigación, junto con sus correspondientes hipótesis nulas, los criterios de verificación empírica y la operacionalización de las variables involucradas.

Las hipótesis han sido formuladas siguiendo los criterios de especificidad, testabilidad y coherencia con el marco teórico. Cada hipótesis específica corresponde biunívocamente con un problema específico (DOC-07) y un objetivo específico (DOC-09), garantizando la coherencia interna del diseño de la investigación. La formulación incluye en todos los casos una dirección predicha de la relación entre las variables, lo que permite el uso de pruebas estadísticas unilaterales donde sea apropiado.

**Hipótesis General**

La hipótesis general de la investigación se enuncia del siguiente modo:

> **HG:** *La aplicación de técnicas de memoria y gestión de contexto reduce significativamente la degradación de respuestas (context rot) en agentes LLM conectados a múltiples servidores MCP, produciendo una mejora medible en el Índice de Calidad de Respuesta Compuesto (IQCR) respecto a una arquitectura base sin dichas técnicas, con al menos una configuración de técnicas que alcanza una mejora superior al 30% en el IQCR después de 50 turnos de conversación.*
> 
> **HG₀:** La aplicación de técnicas de memoria y gestión de contexto no produce una mejora estadísticamente significativa en el Índice de Calidad de Respuesta Compuesto (IQCR) respecto a la arquitectura base sin dichas técnicas en agentes LLM conectados a múltiples servidores MCP (α = 0.05).

La hipótesis general establece tres condiciones verificables: (a) la dirección del efecto —reducción de la degradación, equivalente a mejora del IQCR—; (b) el umbral de magnitud mínima del efecto —30% de mejora—; y (c) el punto de medición de referencia —después de 50 turnos de conversación—. El umbral del 30% se deriva de la evidencia reportada por [Chroma Research (2025)](https://www.trychroma.com/blog/context-rot), que documentó degradaciones superiores al 30% en sistemas de producción sin técnicas de memoria, lo que establece como criterio de relevancia práctica una mejora que revierta al menos la totalidad de esa degradación observada.

La hipótesis general es verificable mediante la comparación del IQCR promedio en el turno 50 entre el grupo de control (sin técnicas de memoria) y el mejor grupo de tratamiento (configuración óptima de técnicas), utilizando una prueba t de Student de una cola con α = 0.05. El tamaño del efecto se reportará mediante d de Cohen, considerando un efecto grande (d ≥ 0.8) como criterio adicional de relevancia práctica.

**Hipótesis Específicas**

Las hipótesis específicas desagregan la hipótesis general en componentes verificables de forma independiente, cada uno correspondiente a un objetivo específico de la investigación.

**Hipótesis Específica 1: Degradación Base**

> **HE1:** *En ausencia de técnicas de memoria o gestión de contexto, los agentes LLM conectados a múltiples servidores MCP exhiben una degradación estadísticamente significativa de al menos el 25% en la exactitud de respuesta y un incremento de al menos el 15% en la tasa de alucinación al comparar el turno 10 con el turno 50 de la conversación.*
> 
> **HE1₀:** En ausencia de técnicas de memoria o gestión de contexto, no existe una diferencia estadísticamente significativa (α = 0.05) en la exactitud de respuesta ni en la tasa de alucinación entre el turno 10 y el turno 50 de conversaciones con agentes LLM conectados a múltiples servidores MCP.

Esta hipótesis establece la existencia y magnitud del fenómeno de context rot como condición previa para justificar el resto del estudio experimental. Los umbrales del 25% en exactitud y el 15% en alucinación se derivan de los valores reportados en la literatura: [Liu et al. (2023)](https://doi.org/10.1162/tacl\_a\_00638) documentaron pérdidas de hasta el 40% en recuperación de información en contextos largos, y [Chroma Research (2025)](https://www.trychroma.com/blog/context-rot) reportó degradaciones superiores al 30% en agentes de producción. Los umbrales de esta hipótesis son conservadores respecto a esa evidencia, garantizando que la hipótesis sea verificable incluso si el context rot en el escenario multi-MCP específico de la tesis es menos severo que en los estudios previos.

La verificación se realizará mediante prueba de Wilcoxon de los rangos con signo (dado que los datos pueden no ser normales) comparando las distribuciones de exactitud y alucinación entre los turnos 10 y 50, con corrección de Bonferroni para comparaciones múltiples. El protocolo de muestreo incluirá mínimo 30 conversaciones independientes de 50 turnos para garantizar potencia estadística suficiente (1 - β ≥ 0.80).

**Hipótesis Específica 2: Técnicas Individuales de Memoria**

> **HE2:** *Al menos una de las técnicas individuales de memoria evaluadas —RAG semántico, SessionFacts, MemoryBank o semantic caching— produce una reducción estadísticamente significativa en la tasa de degradación de respuestas de los agentes LLM multi-MCP, con un efecto de tamaño medio o grande (d de Cohen ≥ 0.5) en al menos dos de las cuatro métricas primarias del IQCR.*
> 
> **HE2₀:** Ninguna de las técnicas individuales de memoria evaluadas produce una reducción estadísticamente significativa (α = 0.05) en la tasa de degradación de respuestas, o el tamaño del efecto es pequeño (d \< 0.5) para todas las métricas primarias del IQCR.

Esta hipótesis es la más central del estudio, pues verifica si las técnicas de memoria propuestas en la literatura tienen el efecto esperado en el escenario multi-MCP específico. La condición de tamaño del efecto medio o grande (d ≥ 0.5) es un criterio de relevancia práctica: una diferencia estadísticamente significativa con un efecto pequeño (d \< 0.2) tendría escasa relevancia para la toma de decisiones de diseño en entornos reales.

La verificación se realizará mediante ANOVA de un factor con post-hoc de Tukey para comparar los cinco grupos de tratamiento (baseline + cuatro técnicas individuales) en cada métrica del IQCR. Se aplicará la prueba de Shapiro-Wilk para verificar la normalidad de los residuos antes de seleccionar la prueba paramétrica o no paramétrica correspondiente. El análisis se realizará separadamente para cada longitud de conversación (30, 50, 100 turnos) para identificar si el efecto de las técnicas varía con la extensión de la sesión.

**Hipótesis Específica 3: Tool Gating**

> **HE3:** *Las estrategias de tool gating —filtrado semántico y carga diferida de herramientas— reducen el consumo de tokens de descripción de herramientas en al menos el 50% en catálogos de 50 y 100 herramientas MCP, sin producir una reducción estadísticamente significativa en la tasa de selección correcta de herramientas (p \> 0.05) ni un incremento mayor al 10% en la tasa de alucinación de parámetros.*
> 
> **HE3₀:** Las estrategias de tool gating no producen una reducción del 50% o mayor en el consumo de tokens de descripción de herramientas, o producen una reducción estadísticamente significativa (α = 0.05) en la tasa de selección correcta de herramientas, o producen un incremento mayor al 10% en la tasa de alucinación de parámetros.

Esta hipótesis es compuesta: requiere simultáneamente la verificación del beneficio (reducción de tokens) y la ausencia de efecto negativo relevante (mantenimiento de la exactitud). La formulación compuesta es intencionada: el objetivo del tool gating no es simplemente reducir tokens sino hacerlo sin sacrificar la capacidad del agente para seleccionar herramientas correctamente. El umbral del 50% de reducción de tokens se deriva del valor reportado por [Tang et al. (2025)](https://arxiv.org/abs/2502.03415) para RAG-MCP en catálogos de 128 herramientas.

La verificación del beneficio se realizará mediante prueba t de una cola comparando el consumo de tokens entre condiciones con y sin tool gating. La verificación de la ausencia de daño en la selección de herramientas se realizará mediante prueba de equivalencia (TOST, two one-sided tests) con un margen de equivalencia del 10% en la tasa de selección correcta, lo que proporciona evidencia positiva de ausencia de efecto dañino y no solo ausencia de evidencia de daño.

**Hipótesis Específica 4: Sinergia de Técnicas Combinadas**

> **HE4:** *La combinación óptima de técnicas de memoria y gestión de contexto, identificada mediante diseño factorial 2k reducido, produce un Índice de Calidad de Respuesta Compuesto (IQCR) significativamente superior al de cualquier técnica individual aplicada de forma aislada, con una mejora adicional de al menos el 15% sobre la mejor técnica individual en conversaciones de 50 o más turnos con tres o más servidores MCP activos.*
> 
> **HE4₀:** La combinación óptima de técnicas de memoria no produce un IQCR estadísticamente superior (α = 0.05) al de la mejor técnica individual, o la mejora adicional es menor al 15% sobre la mejor técnica individual.

Esta hipótesis evalúa la existencia de sinergia entre técnicas: que el efecto conjunto sea mayor que la suma de los efectos individuales. El umbral del 15% de mejora adicional sobre la mejor técnica individual es un criterio conservador que reconoce que los efectos de sinergia típicamente son menores que los efectos principales. La condición de conversaciones de 50 o más turnos restringe la verificación al régimen donde el context rot es clínicamente significativo, que es donde la sinergia entre técnicas tiene mayor relevancia.

La verificación se realizará mediante el análisis del diseño factorial: los coeficientes de interacción de segundo orden en el modelo factorial indicarán la presencia o ausencia de sinergias entre técnicas. Se utilizará el criterio de Lenth para identificar efectos activos en el diseño fraccionado. La comparación de la combinación óptima con las técnicas individuales se realizará mediante prueba t con corrección de Bonferroni para comparaciones múltiples.

**Hipótesis Específica 5: Umbrales de Degradación**

> **HE5:** *Existen umbrales discretos y estadísticamente detectables de longitud de contexto acumulado y número de servidores MCP activos a partir de los cuales la degradación de respuestas se vuelve estadísticamente significativa (p \< 0.05), localizables en el rango de 20,000 a 60,000 tokens acumulados para la condición sin técnicas de memoria y en el rango de 50,000 a 100,000 tokens para la condición con la combinación óptima de técnicas.*
> 
> **HE5₀:** No existen umbrales discretos estadísticamente detectables de longitud de contexto o número de servidores MCP a partir de los cuales la degradación de respuestas sea significativa, o si existen, no son localizables dentro de los rangos de experimentación del estudio con potencia estadística suficiente (1 - β ≥ 0.80).

Esta hipótesis tiene el mayor valor práctico para el diseño de sistemas en producción: si los umbrales son discretos y predecibles, es posible implementar políticas de activación automática de técnicas de memoria basadas en contadores de tokens o número de servidores activos. Los rangos predichos —20,000 a 60,000 tokens sin memoria y 50,000 a 100,000 con memoria— se derivan de la evidencia de [Liu et al. (2023)](https://doi.org/10.1162/tacl\_a\_00638) sobre el efecto lost-in-the-middle (observable a partir de 4,000 tokens en tareas de lectura) escalada al contexto de agentes multi-MCP donde el overhead de herramientas ocupa típicamente 10,000–20,000 tokens antes de que comience la conversación.

La verificación se realizará mediante el algoritmo PELT (Pruned Exact Linear Time) de detección de puntos de cambio, aplicado a las series temporales de exactitud de respuesta y tasa de alucinación a lo largo de las conversaciones experimentales. Los puntos de cambio detectados se validarán mediante bootstrapping (1,000 muestras) para estimar sus intervalos de confianza al 95%. La detección se realizará independientemente para cada combinación de número de servidores MCP (2, 3 y 5 servidores activos).

**Operacionalización de Variables**

La Tabla 1 presenta la operacionalización de las variables de las hipótesis, especificando para cada variable su definición conceptual, su definición operacional, el instrumento de medición y la escala de medida:

|                                    |                         |                                                                                                                                      |                                         |            |
| ---------------------------------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------- | ---------- |
| **Variable**                       | **Tipo**                | **Definición Operacional**                                                                                                           | **Instrumento**                         | **Escala** |
| **Técnica de memoria aplicada**    | Independiente (nominal) | Tipo de técnica: sin técnica, RAG, SessionFacts, MemoryBank, caching o combinación óptima. 6 niveles discretos.                      | Configuración del agente experimental   | Nominal    |
| **Índice IQCR**                    | Dependiente (continua)  | Media ponderada normalizada \[0,1\] de exactitud, complemento de alucinación, coherencia BERTScore y eficiencia de tokens por turno. | Módulo de evaluación automatizado       | Razón      |
| **Exactitud de respuesta**         | Dependiente (continua)  | Proporción de respuestas correctas según ground truth en cada turno. Rango \[0,1\].                                                  | Comparación automática con ground truth | Razón      |
| **Tasa de alucinación**            | Dependiente (continua)  | Proporción de afirmaciones incorrectas verificadas por el módulo de fact-checking. Rango \[0,1\].                                    | Verificación cruzada automatizada       | Razón      |
| **Consumo de tokens por turno**    | Dependiente (continua)  | Número de tokens de prompt + completion registrado por la API en cada turno.                                                         | API counter de Anthropic                | Razón      |
| **Longitud de contexto acumulado** | Moderadora (continua)   | Suma acumulada de tokens procesados desde el inicio de la sesión hasta el turno actual.                                              | API counter de Anthropic                | Razón      |
| **Número de servidores MCP**       | Moderadora (ordinal)    | Cantidad de servidores MCP activos en la sesión experimental. Valores: 2, 3 o 5.                                                     | Configuración del entorno experimental  | Ordinal    |

> *Nota.* Operacionalización de variables del diseño experimental. IQCR = Índice de Calidad de Respuesta Compuesto; MCP = Model Context Protocol; RAG = Retrieval-Augmented Generation.

**Criterios de Verificación y Nivel de Significancia**

Todas las hipótesis se verificarán con un nivel de significancia α = 0.05, salvo que se indique explícitamente lo contrario. Para las comparaciones múltiples derivadas de la evaluación de cinco tratamientos, se aplicará corrección de Bonferroni para controlar la tasa de error familiar (familywise error rate, FWER) al nivel α = 0.05, lo que equivale a un nivel de significancia por prueba de α' = 0.01.

La potencia estadística objetivo es 1 - β = 0.80 para todos los análisis confirmatorios. El cálculo del tamaño de muestra mínimo se realizará con el software G\*Power 3.1, asumiendo un tamaño del efecto medio (d = 0.5) como caso base conservador, y se ajustará tras el análisis exploratorio preliminar de la línea base (OE1) si los datos sugieren un efecto mayor.

Además de las pruebas de significancia estadística, se reportarán los tamaños del efecto (d de Cohen para comparaciones de dos grupos; η² parcial para ANOVA) y los intervalos de confianza al 95% para todos los estimadores clave. Esta práctica es consistente con las recomendaciones de la American Psychological Association (APA, 2020) para el reporte de resultados cuantitativos y con los estándares actuales de la comunidad de evaluación de IA.

**Síntesis de Hipótesis y Correspondencia con Problemas y Objetivos**

La Tabla 2 presenta la correspondencia completa entre cada hipótesis y su problema y objetivo específico asociados, así como el método estadístico de verificación y el criterio de rechazo de la hipótesis nula:

|          |           |          |                                                                  |                                                                                                            |
| -------- | --------- | -------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Hip.** | **Prob.** | **Obj.** | **Método de Verificación**                                       | **Criterio de Rechazo H₀**                                                                                 |
| **HG**   | PG        | OG       | Prueba t una cola; d de Cohen                                    | p \< 0.05; IQCR turno 50 mejora ≥ 30% sobre baseline                                                       |
| **HE1**  | PE1       | OE1      | Wilcoxon rangos con signo; corrección Bonferroni                 | p \< 0.05; exactitud cae ≥ 25% y alucinación sube ≥ 15% entre turnos 10 y 50                               |
| **HE2**  | PE2       | OE2      | ANOVA un factor + post-hoc Tukey; d de Cohen                     | p \< 0.05 para al menos una técnica; d ≥ 0.5 en ≥ 2 métricas del IQCR                                      |
| **HE3**  | PE3       | OE3      | Prueba t una cola (beneficio); TOST (ausencia de daño)           | Reducción ≥ 50% tokens; TOST p \< 0.05 dentro de margen de equivalencia ±10%                               |
| **HE4**  | PE4       | OE4      | Diseño factorial 2k; análisis de interacciones; t con Bonferroni | Interacción significativa p \< 0.05; combinación óptima mejora ≥ 15% sobre mejor técnica individual        |
| **HE5**  | PE5       | OE5      | PELT detección puntos de cambio; bootstrapping 1,000 muestras    | Puntos de cambio detectados con CI 95% en rangos predichos para ≥ 2 de 3 configuraciones de servidores MCP |

> *Nota.* Correspondencia entre hipótesis, problemas y objetivos. Hip. = Hipótesis; Prob. = Problema; Obj. = Objetivo; HG = Hipótesis General; HE = Hipótesis Específica; PG/PE = Problema General/Específico; OG/OE = Objetivo General/Específico; IQCR = Índice de Calidad de Respuesta Compuesto; PELT = Pruned Exact Linear Time; TOST = Two One-Sided Tests; CI = Intervalo de Confianza.

**Referencias**

American Psychological Association. (2020). Publication manual of the American Psychological Association (7.ª ed.). [https://doi.org/10.1037/0000165-000](https://doi.org/10.1037/0000165-000)

Chroma Research. (2025). Context rot in production LLM systems: A benchmark study. Chroma. [https://www.trychroma.com/blog/context-rot](https://www.trychroma.com/blog/context-rot)

Cohen, J. (1988). Statistical power analysis for the behavioral sciences (2.ª ed.). Lawrence Erlbaum Associates.

Faul, F., Erdfelder, E., Lang, A.-G., & Buchner, A. (2007). G\*Power 3: A flexible statistical power analysis program for the social, behavioral, and biomedical sciences. Behavior Research Methods, 39(2), 175–191. [https://doi.org/10.3758/BF03193146](https://doi.org/10.3758/BF03193146)

Hu, J., Huang, S., Luo, Y., Wu, F., & Lam, W. (2023). MemoryBank: Enhancing large language models with long-term memory. arXiv. [https://arxiv.org/abs/2305.10250](https://arxiv.org/abs/2305.10250)

Killick, R., Fearnhead, P., & Eckley, I. A. (2012). Optimal detection of changepoints with a linear computational cost. Journal of the American Statistical Association, 107(500), 1590–1598. [https://doi.org/10.1080/01621459.2012.737745](https://doi.org/10.1080/01621459.2012.737745)

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. Advances in Neural Information Processing Systems, 33, 9459–9474. [https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html](https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html)

Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2023). Lost in the middle: How language models use long contexts. Transactions of the Association for Computational Linguistics, 12, 157–173. [https://doi.org/10.1162/tacl\_a\_00638](https://doi.org/10.1162/tacl\_a\_00638)

Montgomery, D. C. (2017). Design and analysis of experiments (9.ª ed.). Wiley.

Packer, C., Wooders, S., Lin, K., Fang, V., Patil, S. G., Stoica, I., & Gonzalez, J. E. (2023). MemGPT: Towards LLMs as operating systems. arXiv. [https://arxiv.org/abs/2310.08560](https://arxiv.org/abs/2310.08560)

Tang, R., Jin, Z., Alexandrov, A., Shao, Y., Shi, P., & Pan, L. (2025). RAG-MCP: Mitigating prompt bloat in LLM tool selection via retrieval-augmented generation. arXiv. [https://arxiv.org/abs/2502.03415](https://arxiv.org/abs/2502.03415)

Zeng, Z., Liu, M., Lu, R., Wang, B., Liu, X., & Cheng, X. (2025). SimpleToolHalluBench: Towards a comprehensive assessment of tool call hallucination in large language models. arXiv. [https://arxiv.org/abs/2501.13395](https://arxiv.org/abs/2501.13395)
