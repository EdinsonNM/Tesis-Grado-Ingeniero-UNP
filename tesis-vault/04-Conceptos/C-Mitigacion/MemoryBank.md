# MemoryBank

## Definición

Sistema de memoria a largo plazo para agentes LLM que almacena fragmentos relevantes de conversaciones pasadas y los recupera según relevancia, aplicando una política de olvido inspirada en la **curva de Ebbinghaus**. (DOC-11, Bloque 5; Hu et al., 2023)

El peso de relevancia de cada memoria decrece exponencialmente con el tiempo transcurrido desde su última recuperación — replicando el patrón de olvido natural humano. Las memorias frecuentemente recuperadas mantienen peso alto; las no recuperadas se degradan hasta ser descartadas.

## Evidencia empírica

> Hu et al. (2023) evaluaron MemoryBank en simulaciones de conversación de hasta **500 turnos** y reportaron una **mejora del 37% en coherencia conversacional** respecto a agentes sin memoria externa, medida mediante evaluación humana y métricas automáticas de consistencia.

Este resultado es el referente empírico para la hipótesis específica **HE4** de la tesis:
> *MemoryBank mejora al menos 20% la coherencia conversacional en sesiones de 100 turnos.* → verificado con [[LoCoMo]] y [[BERTScore]].

## Mecanismo de recuperación

1. Cada turno, la consulta del usuario se convierte en vector de embeddings.
2. Se recuperan las k memorias con mayor similitud coseno al vector de consulta.
3. El peso de cada memoria recuperada se actualiza (se "refresca").
4. Solo las memorias recuperadas se inyectan en el contexto del turno.
5. Las memorias no recuperadas durante N turnos tienen su peso decrementado.

## Diferencia con SessionFacts

| Dimensión | SessionFacts | MemoryBank |
|---|---|---|
| Alcance temporal | Sesión actual | Multi-sesión (largo plazo) |
| Estructura | Clave-valor compacto | Fragmentos indexados por vector |
| Política de olvido | Reemplazo por compresión | Decaimiento exponencial (Ebbinghaus) |
| Latencia de recuperación | Baja (estructura fija) | Mayor (búsqueda vectorial) |

## Función en la tesis

Representa la técnica de memoria externa a largo plazo, evaluada individualmente y en combinación con [[Tool gating]] y [[SessionFacts]] en el diseño factorial [[Diseno factorial 2k|2^k]].

## Riesgos

- Recuperar memorias obsoletas con peso aún alto por recuperaciones pasadas.
- Introducir contradicciones al mezclar memorias de sesiones con contextos diferentes.
- Aumentar latencia por búsqueda vectorial en cada turno.
- Cold start: las primeras sesiones tienen poco banco de memoria útil.

## Relación con otras técnicas

- [[SessionFacts]] — estado de sesión a corto plazo, complementario
- [[Mem0]] — extiende MemoryBank con distinción por tipo de memoria
- [[RAG]] — mismo principio de recuperación semántica, aplicado a documentos
- [[Context rot]] — el problema que MemoryBank mitiga en sesiones largas
- [[Coherencia conversacional]] — la métrica principal que mejora

## Fuentes

- [[Bases Teoricas]] — bloque 5
- [[Zhong 2023 - MemoryBank]]

