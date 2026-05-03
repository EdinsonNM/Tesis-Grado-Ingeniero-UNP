# Zhou et al. (2026) — Externalization in LLM Agents

## Referencia APA

Zhou, C., Chai, H., Chen, W., Guo, Z., Shan, R., Song, Y., Xu, T., Yang, Y., Yu, A., Zhang, W., Zheng, C., Zhu, J., Zheng, Z., Zhang, Z., Lou, X., Zhang, C., Fu, Z., Wang, J., Liu, W., Lin, J., & Zhang, W. (2026). *Externalization in LLM Agents: A Unified Review of Memory, Skills, Protocols and Harness Engineering*. arXiv:2604.08224 [cs.SE]. https://doi.org/10.48550/arXiv.2604.08224

## Tipo de fuente

Preprint académico · arXiv · cs.SE + cs.MA · 54 páginas · 21 autores · Publicado: 9 abril 2026.

---

## Tesis central del paper

Los agentes LLM modernos se construyen cada vez menos modificando los pesos del modelo y cada vez más **reorganizando el entorno de ejecución que lo rodea**. Las capacidades que antes se esperaba que el modelo recuperara internamente ahora se *externalizan* en módulos especializados.

El paper propone una taxonomía de cuatro formas de externalización:

| Forma | Qué externaliza | Ejemplo en la tesis |
|---|---|---|
| **Memoria** | Estado a través del tiempo | [[SessionFacts]], [[MemoryBank]], [[Mem0]] |
| **Skills** | Conocimiento procedural | Prompts de sistema, AGENTS.md |
| **Protocolos** | Estructura de interacción | [[Model Context Protocol]] |
| **Harness Engineering** | Coordinación y ejecución gobernada | Capa que orquesta memoria + protocolos + herramientas |

---

## Progresión histórica

El paper traza tres eras:

1. **Era de los pesos** — mejoras via fine-tuning y RLHF
2. **Era del contexto** — in-context learning, RAG, prompting
3. **Era del harness** — el progreso práctico depende de la infraestructura externa, no solo del modelo

La tesis opera explícitamente en la era del harness: estudia qué técnicas de la capa de externalización (memoria, protocolos MCP, tool gating) minimizan el [[Context rot]].

---

## Citas clave

> *"Memory externalizes state across time, skills externalize procedural expertise, protocols externalize interaction structure, and harness engineering serves as the unification layer that coordinates them into governed execution."*

> *"Practical agent progress increasingly depends not only on stronger models, but on better external cognitive infrastructure."*

---

## Relevancia para la tesis

**Marco teórico unificador**: sitúa todas las técnicas estudiadas (SessionFacts, MemoryBank, RAG-MCP, tool gating, caching) dentro de un paradigma académico coherente — el paradigma de externalización. La tesis contribuye a este paradigma generando evidencia empírica cuantitativa sobre qué formas de externalización son más efectivas en escenarios multi-MCP.

**Conexión directa**: el paper cita explícitamente MemGPT (Packer 2023), MemoryBank (Zhong 2023) y Mem0 (Chhikara 2025) — todas fuentes ya en el marco referencial de la tesis.

**Uso en el documento**:
- [[Bases Teoricas]] — Bloque 8 (marco unificador de externalización)
- [[Antecedentes de la Investigación]] — antecedente teórico para sección de técnicas de memoria y filtrado
- [[Marco Referencial]] — nueva categoría académica
- DOC-11 (Bases Teóricas) — nuevo bloque
- DOC-02 (Catálogo de Fuentes) — nueva entrada

---

## Notas metodológicas

- Preprint en arXiv, aún no publicado en revista con peer review formal. Citar como *tech report* o *preprint* según normas APA 7ª ed.
- 54 páginas, alcance amplio — usarlo como marco de posicionamiento, no como fuente de datos empíricos.
- No reporta resultados experimentales propios; es una revisión unificada.

---

## Conceptos relacionados

[[Context rot]] · [[SessionFacts]] · [[MemoryBank]] · [[RAG-MCP]] · [[Tool gating]] · [[Model Context Protocol]] · [[Agente LLM]]
