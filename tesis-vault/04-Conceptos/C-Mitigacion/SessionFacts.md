# SessionFacts

## Definición

Mecanismo de compresión de estado de sesión que extrae hechos, entidades, restricciones y decisiones relevantes del historial conversacional para representarlos en una estructura compacta clave-valor que reemplaza el historial completo. (DOC-11, Bloque 5)

El agente invoca un paso de *summarization* que produce una ficha de sesión estructurada con los elementos mínimos necesarios para continuar la conversación sin cargar el historial completo.

## Problema que resuelve

El historial completo de conversaciones multi-turno con múltiples servidores MCP acumula observaciones verbosas de herramientas, mensajes de error, metadatos de autenticación y paginación que ocupan la región central del [[Contexto activo]] — exactamente donde los LLMs pierden atención efectiva (efecto [[Lost in the middle]]).

SessionFacts extrae únicamente lo semánticamente relevante y descarta el resto, deteniendo el crecimiento lineal del contexto.

## Evidencia empírica

> Packer et al. (2023) evaluaron técnicas similares en el sistema **MemGPT** y reportaron **reducciones de hasta el 70% en el consumo de tokens de historial** sin pérdida significativa de coherencia conversacional.

Este resultado es el referente empírico para la hipótesis específica **HE2** de la tesis:
> *SessionFacts reduce al menos 50% los tokens de historial preservando coherencia conversacional medida por BERTScore.* → verificado con Wilcoxon para la dimensión de coherencia.

## Contenido estándar de una SessionFact

- **Objetivo activo** — qué está intentando lograr el usuario en esta sesión.
- **Hechos confirmados** — información ya verificada y acordada.
- **Entidades relevantes** — nombres, IDs, recursos, archivos involucrados.
- **Restricciones** — límites o condiciones que deben respetarse.
- **Decisiones tomadas** — elecciones ya hechas que no deben reconsiderarse.
- **Referencias a artefactos externos** — URLs, rutas de archivo, IDs de ticket.
- **Estado por servidor MCP** — qué retornó cada servidor en el último ciclo relevante.

## Indicadores de evaluación en la tesis

- **Tokens de historial por turno** — reducción esperada: ~70% (Packer et al., 2023).
- **BERTScore** — pérdida aceptable: margen de equivalencia según [[TOST]].
- **Coherencia conversacional** — medida con [[LoCoMo]] en 100 turnos.
- **Latencia adicional** — el paso de summarization agrega latencia al inicio de cada "compresión".

## Riesgos

- Perder detalles importantes durante la compresión.
- Mantener hechos obsoletos si no hay invalidación explícita.
- Mezclar preferencias estables con estado transitorio.
- Fallo silencioso: el agente actúa como si recordara algo que fue descartado.

## Relación con otras técnicas

- [[Context rot]] — el problema que SessionFacts ataca directamente
- [[MemoryBank]] — memoria a largo plazo vs. estado de sesión a corto plazo
- [[Mem0]] — gestión por tipo de memoria (usuario / agente / sesión)
- [[Compaction]] — compresión más agresiva del historial completo
- [[IQCR]] — índice que mide el impacto de SessionFacts en la calidad de respuesta

## Fuentes

- [[Bases Teoricas]] — bloque 5 (desarrollo completo)
- [[Packer 2023 - MemGPT]]

