# Aspectos Administrativos

→ Capítulo [[Cap 4 - Aspectos Administrativos]]
Fuente: `DOC-15_Aspectos_Administrativos.docx`

---

## 4.1 Recursos Necesarios

**Recursos humanos:** investigador principal (tesista) asume diseño experimental, implementación, ejecución, análisis estadístico y redacción. Asesor de tesis participa en revisiones y retroalimentación. No se requiere personal de campo dado el carácter íntegramente computacional del estudio.

**Recursos tecnológicos:** API Anthropic (Claude Sonnet 4.5), API OpenAI (embeddings text-embedding-3-small), instancias AWS EC2 + S3, Redis Cloud para [[Caching semantico]], computadora personal ≥16 GB RAM.

**Recursos de información:** datasets LongMemEval y LoCoMo (GitHub, acceso libre), bases bibliográficas (arXiv, Semantic Scholar, Google Scholar), código fuente de ChromaDB, RedisVL y MLflow.

---

## 4.2 Presupuesto Estimado

| Categoría | Ítem | Costo USD | Costo PEN |
|---|---|---|---|
| APIs de IA | API Anthropic ~1M tokens | $15.00 | S/. 56.25 |
| APIs de IA | API OpenAI embeddings ~5M tokens | $1.00 | S/. 3.75 |
| Infraestructura | AWS EC2 t3.medium × 3 meses | $90.00 | S/. 337.50 |
| Infraestructura | AWS S3 50GB × 6 meses | $6.90 | S/. 25.88 |
| Infraestructura | Redis Cloud Essentials × 3 meses | $21.00 | S/. 78.75 |
| Software | GitHub Pro × 12 meses | $48.00 | S/. 180.00 |
| Software | MLflow Cloud (plan gratuito) | $0.00 | S/. 0.00 |
| Bibliografía | Montgomery *Design of Experiments* (libro) | $80.00 | S/. 300.00 |
| Difusión | Impresión y empastado × 3 ejemplares | $60.00 | S/. 225.00 |
| Difusión | Preprint arXiv | $0.00 | S/. 0.00 |
| Contingencia 10% | Costos imprevistos de API y cómputo | $32.19 | S/. 120.71 |
| **TOTAL** | | **$354.09** | **S/. 1,327.84** |

*Tipo de cambio referencial: S/. 3.75 por USD.*

---

## 4.3 Cronograma de Actividades (jul 2025 – jun 2026)

| Actividad | J | A | S | O | N | D | E | F | M | A | M | J |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **FASE 1 — Planificación y Diseño** | | | | | | | | | | | | |
| 1.1 Revisión sistemática de literatura | ● | ● | | | | | | | | | | |
| 1.2 Redacción proyecto de tesis (DOC-01 a DOC-13) | ● | ● | ● | | | | | | | | | |
| 1.3 Aprobación por comité | | | ● | | | | | | | | | |
| **FASE 2 — Desarrollo Experimental** | | | | | | | | | | | | |
| 2.1 Implementación agente base (baseline) | | | | ● | ● | | | | | | | |
| 2.2 Implementación técnicas de memoria | | | | ● | ● | | | | | | | |
| 2.3 Módulo de evaluación automatizado | | | | | ● | ● | | | | | | |
| 2.4 Prueba piloto y ajuste de protocolo | | | | | | ● | | | | | | |
| 2.5 Experimentos: línea base | | | | | | | ● | ● | | | | |
| 2.6 Experimentos: técnicas individuales | | | | | | | ● | ● | | | | |
| 2.7 Experimentos: tool gating | | | | | | | | ● | | | | |
| 2.8 Diseño factorial 2^k | | | | | | | | ● | ● | | | |
| **FASE 3 — Análisis y Redacción** | | | | | | | | | | | | |
| 3.1 Análisis estadístico completo | | | | | | | | | ● | ● | | |
| 3.2 Detección de umbrales ([[PELT]]) | | | | | | | | | ● | | | |
| 3.3 Redacción de resultados y discusión | | | | | | | | | ● | ● | | |
| 3.4 Revisión y corrección de tesis completa | | | | | | | | | | ● | ● | |
| **FASE 4 — Difusión y Sustentación** | | | | | | | | | | | | |
| 4.1 Presentación ante comité | | | | | | | | | | | ● | |
| 4.2 Publicación preprint arXiv | | | | | | | | | | | ● | ● |
| 4.3 Sustentación pública | | | | | | | | | | | | ● |

*J=Jul·25 A=Ago S=Sep O=Oct N=Nov D=Dic E=Ene·26 F=Feb M=Mar A=Abr M=May J=Jun*

> Los meses de mayor uso de API (enero–marzo, fases de ejecución experimental) coinciden con la mayor acumulación de costos de infraestructura cloud. Se contempla una ventana de corrección de dos meses (abril–mayo) antes de la sustentación.

---

## Fuentes

- [[Diseno metodologico]] — fases experimentales que sustentan el cronograma
- [[Hipotesis de investigacion]] — los análisis estadísticos que requieren cómputo en Fase 3
