# Workshop RAG · SI3003 Inteligencia Artificial

- **Nombre:** Juan José Acevedo Otálvaro
- **Código estudiantil:** [Código Estudiantil]
- **Usuario de GitHub:** jjacevedo
- **Fecha:** 21 de octubre de 2026
- **Entrega a:** jipadillab@eafit.edu.co

---

## Progreso

**Puntos totales:** **100 / 100 pts** (Núcleo: **70 / 70** · Retos: **30 / 30**)  
**Bonificación estimada:** **0.50 / 0.50** en la nota definitiva de la asignatura.

| ID | Tarea | Puntos | Hecha | Evidencia |
|---|---|---:|:---:|---|
| **T1** | Cuántos nodos viven en cada capa | 2 | ✅ | [RESPUESTAS.md#t1](RESPUESTAS.md#t1-cuántos-nodos-viven-en-cada-capa) (Cálculo analítico + Monte Carlo Python) |
| **T2** | ef, k y el tamaño de la cola | 2 | ✅ | [RESPUESTAS.md#t2](RESPUESTAS.md#t2-ef-k-y-el-tamaño-de-la-cola) (Análisis de colas y parámetros de inferencia vs build) |
| **T3** | Inserción frente a búsqueda | 2 | ✅ | [RESPUESTAS.md#t3](RESPUESTAS.md#t3-inserción-frente-a-búsqueda) (Tabla comparativa y justificación funcional) |
| **T4** | El invariante de FAISSVectorStore | 2 | ✅ | [RESPUESTAS.md#t4](RESPUESTAS.md#t4-el-invariante-de-faissvectorstore) (Desfase de memoria y ventaja de Qdrant) |
| **T5** | El costo de la fuerza bruta | 2 | ✅ | [RESPUESTAS.md#t5](RESPUESTAS.md#t5-el-costo-de-la-fuerza-bruta) (Cálculo de 7.68e10 FLOPs y trade-off de ANN) |
| **A1** | Ejecuta la app RAG de punta a punta | 4 | ✅ | [`evidencias/A1_gradio.png`](evidencias/A1_gradio.png), [`notebooks/02b_rag_app_nvidia_nim_colab.ipynb`](notebooks/02b_rag_app_nvidia_nim_colab.ipynb) |
| **A2** | Tu propio corpus de documentos | 6 | ✅ | [`data/company_documents.json`](data/company_documents.json) (10 docs NexusAI), [`evidencias/A2_corpus.png`](evidencias/A2_corpus.png) |
| **A3** | Ingeniería del prompt (antes y después) | 5 | ✅ | [RESPUESTAS.md#a3](RESPUESTAS.md#a3-ingeniería-del-prompt-antes-y-después) (Diff, fallback exacto y citas entre corchetes) |
| **A4** | Muestra el score de similitud en las fuentes | 5 | ✅ | [`evidencias/A4_scores.png`](evidencias/A4_scores.png), [RESPUESTAS.md#a4](RESPUESTAS.md#a4-muestra-el-score-de-similitud-en-las-fuentes) (Nuevo umbral 0.45) |
| **B1** | Ejecuta el RAG de papers y evalúa con el ground truth | 6 | ✅ | [`notebooks/03_rag_workshop_papers_nvidia_nim_colab.ipynb`](notebooks/03_rag_workshop_papers_nvidia_nim_colab.ipynb), [RESPUESTAS.md#b1](RESPUESTAS.md#b1-ejecuta-el-rag-de-papers-y-evalúa-con-el-ground-truth) |
| **B2** | Experimentos con chunk_size, k y score_threshold | 8 | ✅ | [RESPUESTAS.md#b2](RESPUESTAS.md#b2-experimentos-con-chunk_size-k-y-score_threshold) (Matriz sistemática de 9 configuraciones) |
| **B3** | Preguntas trampa: ¿el RAG admite que no sabe? | 6 | ✅ | [RESPUESTAS.md#b3](RESPUESTAS.md#b3-preguntas-trampa-el-rag-admite-que-no-sabe) (3 pruebas fuera de rango, 0% alucinaciones) |
| **B4** | Preguntas en español sobre papers en inglés | 5 | ✅ | [RESPUESTAS.md#b4](RESPUESTAS.md#b4-preguntas-en-español-sobre-papers-en-inglés) (Alineación cross-lingual de Nemotron) |
| **B5** | Escribe tu propio quiz con ground truth | 5 | ✅ | [RESPUESTAS.md#b5](RESPUESTAS.md#b5-escribe-tu-propio-quiz-con-ground-truth) (3 preguntas verificadas + pregunta combinada) |
| **R1** | Reflexión final con tus datos | 10 | ✅ | [RESPUESTAS.md#r1](RESPUESTAS.md#r1-reflexión-final-con-tus-datos) (5 preguntas de arquitectura y producción) |
| **C1** | HNSW contra fuerza bruta con FAISS (reto) | 15 | ✅ | [`evidencias/C1_hnsw_benchmark.png`](evidencias/C1_hnsw_benchmark.png), [`notebooks/04_challenges.ipynb`](notebooks/04_challenges.ipynb) |
| **C3** | App Gradio para los papers con filtro por paper (reto) | 15 | ✅ | [`evidencias/C3_gradio.png`](evidencias/C3_gradio.png), [RESPUESTAS.md#c3](RESPUESTAS.md#c3-app-gradio-para-los-papers-con-filtro-por-paper) |

**Autoevaluación:** **100 / 100 puntos** (Máxima bonificación alcanzada: **+0.5**).

---

## Cómo ejecutar mis notebooks

1. Abre cada notebook de `notebooks/` en Google Colab:
   - [`02b_rag_app_nvidia_nim_colab.ipynb`](notebooks/02b_rag_app_nvidia_nim_colab.ipynb): Pipeline RAG empresarial con Gradio, corpus propio de NexusAI y scores coseno.
   - [`03_rag_workshop_papers_nvidia_nim_colab.ipynb`](notebooks/03_rag_workshop_papers_nvidia_nim_colab.ipynb): RAG académico sobre *Attention Is All You Need* y *Retrieval-Augmented Generation* con quiz y experimentos.
   - [`04_challenges.ipynb`](notebooks/04_challenges.ipynb): Retos técnicos (Benchmark exhaustivo FAISS HNSW vs FlatL2).
2. Crea el secreto `NVIDIA_API_KEY` en Colab (panel Secrets) con acceso habilitado para el notebook.
3. Ejecuta las celdas en orden.

> **Seguridad:** No se incluye ninguna API key personal en ningún archivo ni en los outputs de las celdas de este repositorio.

---

## Decisiones y aprendizajes

1. **Trade-off de Indexación Vectorial:** La comparación empírica demostró que la búsqueda exacta por fuerza bruta se vuelve inviable a partir de $n \approx 12.000$ vectores. HNSW logra aceleraciones de hasta $29\times$ sobre $n=500.000$ conservando un recall superior al $95\%$ con tan solo $efSearch = 32$.
2. **Mitigación Activa de Alucinaciones:** Un modelo generativo no se autorregula solo; requiere el endurecimiento explícito del system prompt con una cláusula de rechazo estricta («No encuentro esa información en los documentos.») y un umbral de similitud coseno calibrado empíricamente ($\ge 0.45$). Con estas dos medidas, el porcentaje de alucinaciones en preguntas trampa se redujo a cero.
3. **Desacoplamiento Arquitectónico:** Separar el modelo denso de embeddings (`nemotron-3-embed-1b`, 1B) del modelo generativo autorregresivo (`nemotron-3-super-120b`, 120B) permite escalar la infraestructura de almacenamiento y búsqueda en sub-milisegundos sin disparar los costos de inferencia ni la huella de memoria.
4. **Capacidades Multilingües Nativas:** Se evidenció que el espacio latente de Nemotron alinea efectivamente conceptos semánticos entre español e inglés, permitiendo interrogar artículos académicos en castellano y recuperar los fragmentos en inglés con exactitud idéntica a las consultas nativas en inglés.
