# Catálogo inicial de fuentes

Índice de todas las fuentes. Cada fuente tiene su propia ficha en `05-Fuentes/` con referencia APA completa, método, métricas y aporte a la tesis.

---

## Fuentes teóricas principales

| Ficha | Aporte clave |
|---|---|
| [[Vaswani 2017 - Attention is All You Need]] | Arquitectura Transformer; base de la ventana de contexto |
| [[Brown 2020 - Language Models are Few-Shot Learners]] | GPT-3; paradigma de LLMs como motores de razonamiento general |
| [[Yao 2022 - ReAct]] | Ciclo razonamiento-acción del agente LLM |
| [[Schick 2023 - Toolformer]] | Selección selectiva de herramientas; base del tool gating |
| [[Lewis 2020 - RAG]] | RAG original; principio de recuperar solo lo relevante |
| [[Liu 2023 - Lost in the Middle]] | Evidencia empírica de degradación por posición en el contexto |
| [[Packer 2023 - MemGPT]] | Memoria virtual LLM; paradigma RAM/disco |
| [[Zhong 2023 - MemoryBank]] | MemoryBank con modelo de olvido de Ebbinghaus |
| [[Chhikara 2025 - Mem0]] | Capa de memoria adaptativa; reducción de 91% en tokens |
| [[Tang 2025 - RAG-MCP]] | RAG-MCP; antecedente directo del tool gating en multi-MCP |
| [[Yin 2026 - SimpleToolHalluBench]] | Benchmark de alucinación de herramientas |
| [[Maharana 2024 - LoCoMo]] | Benchmark de coherencia en conversaciones largas |
| [[Wu 2024 - LongMemEval]] | Benchmark de memoria a largo plazo multi-sesión |

---

## URLs de datasets y benchmarks

| Recurso | URL principal | URL de datos / código |
|---|---|---|
| LongMemEval | https://arxiv.org/abs/2410.10813 | https://github.com/xiaowu0162/LongMemEval · https://huggingface.co/datasets/xiaowu0162/longmemeval-cleaned |
| LoCoMo | https://arxiv.org/abs/2402.17753 | https://github.com/snap-research/locomo · https://snap-research.github.io/locomo/ |
| SimpleToolHalluBench | https://openreview.net/forum?id=xIq7qmyuYF | https://anonymous.4open.science/r/Reasoning_Trap-E5B6/ |
| ToolHaystack | https://arxiv.org/abs/2505.23662 · https://aclanthology.org/2025.findings-emnlp.1344/ | https://github.com/bwookwak/toolhaystack |

**Nota**: no usar arXiv:2501.13395 como fuente de SimpleToolHalluBench — esa URL no corresponde al benchmark correcto.

---

## Marcos teóricos unificadores

| Ficha | Aporte clave |
|---|---|
| [[Zhou 2026 - Externalization in LLM Agents]] | Paradigma de externalización: memoria + protocolos + harness como infraestructura cognitiva externa; progresión histórica pesos → contexto → harness |

---

## Fuentes institucionales

| Ficha | Aporte clave |
|---|---|
| [[Gartner 2025 - Agentic AI Projects Cancellation]] | >40% de proyectos agénticos cancelados para 2027 por complejidad técnica — evidencia de que los agentes en producción siguen siendo un problema no resuelto |

---

## Casos de producción

| Ficha | Aporte clave |
|---|---|
| [[Vercel 2025 - d0 Agent Tool Removal]] | Primer caso documentado de mejora cuantificable por reducción de herramientas en agente de producción (éxito +20pp, −37% tokens, 3.5× velocidad) |

---

## Fuentes técnicas y documentación

- Anthropic: Model Context Protocol → [[Model Context Protocol]]
- LangChain / LangGraph: gestión de estado de agentes → [[Agente LLM]]
- RedisVL: caching semántico → [[Caching semantico]]
- ChromaDB: recuperación vectorial → [[RAG]]

---

## Fuentes metodológicas

- Hernandez Sampieri et al. (2014): metodología de investigación → [[Diseno metodologico]]
- Montgomery (2017): diseño de experimentos → [[Diseno factorial 2k]]
- Killick et al. (2012): PELT para detección de puntos de cambio → [[PELT]]
- APA (2020): reporte estadístico y estilo académico
