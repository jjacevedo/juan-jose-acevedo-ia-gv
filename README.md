# SI3003 — Inteligencia Artificial

**Universidad EAFIT** · Juan José Acevedo Otálvaro

Repositorio personal con todos los talleres, quices, retos de código y actividades prácticas de la asignatura. Los archivos base de cada taller vienen del repositorio oficial del curso: [EAFIT-IA/si3003-artificial-intelligence](https://github.com/EAFIT-IA/si3003-artificial-intelligence).

---

## Índice de Entregables y Talleres

Cada notebook y taller se completó **sobre el archivo original del profesor** (conservando explicaciones y celdas resueltas), se ejecutó de principio a fin y se guardó con sus salidas y justificaciones conceptuales.

| Módulo / Semana | Tema | Entregable | Notebook original |
|---|---|---|---|
| **Módulo 1** | Búsqueda, optimización y Q-Learning | [`taller_busqueda_optimizacion_q_learning.md`](talleres/modulo_01_busqueda_optimizacion_qlearning/taller_busqueda_optimizacion_q_learning.md) | `workshops/module1/taller_...md` |
| **Módulo 1** | Retos de código de búsqueda, optimización y RL | [`01_search`](talleres/modulo_01_busqueda_optimizacion_qlearning/01_search_code_challenge.ipynb), [`02_opt`](talleres/modulo_01_busqueda_optimizacion_qlearning/02_optimization_code_challenge.ipynb), [`03_qlearning`](talleres/modulo_01_busqueda_optimizacion_qlearning/03_q_learning_code_challenge.ipynb) | `workshops/module1/` |
| **Parcial 1** | Examen de Pacman con Q-Learning tabular | [`04_qlearning_pacman_examen_IA_ejecutado.ipynb`](evaluaciones/parcial_01_pacman/04_qlearning_pacman_examen_IA_ejecutado.ipynb) | `workshops/module1/Midterm Exam/` |
| **Semana 4** | Procesos de Decisión de Markov (MDP) | [`03_lab_warehouse_mdp.ipynb`](talleres/semana_04_mdp/03_lab_warehouse_mdp.ipynb) | `notebooks/lecture4/03_lab_warehouse_mdp_estudiantes.ipynb` |
| **Semana 5** | Q-Learning en entornos clásicos | [`03_qlearning_taxi.ipynb`](talleres/semana_05_q_learning/03_qlearning_taxi.ipynb), [`02_qlearning_frozenlake.ipynb`](talleres/semana_05_q_learning/02_qlearning_frozenlake.ipynb) | `notebooks/lecture5/` |
| **Semana 6** | Pipeline de Machine Learning (Wine dataset) | [`01_data_challenge.ipynb`](talleres/semana_06_machine_learning/01_data_challenge.ipynb) → [`02_training.ipynb`](talleres/semana_06_machine_learning/02_training_challenge.ipynb) → [`03_eval_deployment.ipynb`](talleres/semana_06_machine_learning/03_evaluation_deployment_challenge.ipynb) | `notebooks/lecture6/challenge/` |
| **Semana 7** | Modelos lineales y redes neuronales (Keras 3) | [`Challenge_Keras3_CIFAR10_Grayscale.ipynb`](talleres/semana_07_redes_neuronales/Challenge_Keras3_CIFAR10_Grayscale.ipynb), [`Challenge_Keras3_OlivettiFaces.ipynb`](talleres/semana_07_redes_neuronales/Challenge_Keras3_OlivettiFaces.ipynb) | `notebooks/lecture7/` |
| **Semana 8** | CNN y transfer learning con dataset propio | [`taller_transfer_learning_datos_propios_keras3.ipynb`](talleres/semana_08_cnn_transfer_learning/taller_transfer_learning_datos_propios_keras3.ipynb) | `notebooks/lecture8/transfer_learning/` |
| **Semana 8** | Detección de objetos con YOLO | [`yolo/Lecture_08_Yolo_Intro.ipynb`](talleres/semana_08_cnn_transfer_learning/yolo/Lecture_08_Yolo_Intro.ipynb) | `notebooks/lecture8/yolo/` |
| **Módulo 2** | Aprendizaje supervisado, redes y Transformers | [`taller_codigo_ml_nim.ipynb`](talleres/modulo_02_ml_redes_transformers/taller_codigo_ml_nim.ipynb), [`taller_ml_redes_transformers.md`](talleres/modulo_02_ml_redes_transformers/taller_ml_redes_transformers.md) | `workshops/module2/` |
| **Semana 10** | Workshop RAG con NVIDIA NIM, Qdrant y Gradio | [`semana_10_rag/`](talleres/semana_10_rag/) (100 / 100 pts, +0.5 bonificación, retos C1 y C3) | `notebooks/lecture10/` |

---

### Resultados principales

- **Módulo 1 (Búsqueda y Optimización):** Análisis de UCS en grafos con costos acumulados ($g=4$), simulación de Simulated Annealing aceptando empeoramientos estocásticos ($T=4, P=0.472$) y actualización temporal de Q-learning ($Q \to 3.3$).
- **Parcial 1 (Pacman Q-Learning):** Implementación del entorno tabular de Pacman con exploración $\varepsilon$-greedy y convergencia hacia políticas evasivas de fantasmas y recolección de comida.
- **Semana 4 (MDPs):** MDP del almacén modelado a partir del enunciado; Value Iteration y Policy Iteration convergen a la misma política óptima (umbral de `living_reward` $\approx -0.79$).
- **Semana 5 (Q-Learning):** Q-Learning en Taxi-v4; la política greedy completa el 100 % de los episodios de prueba.
- **Semana 6 (Machine Learning):** Dataset Wine (3 clases). Modelo campeón por validación cruzada: regresión logística ($CV = 0.979$; test: accuracy $0.972$, F1 macro $0.971$).
- **Semana 7 (Redes Neuronales):** CIFAR-10 en escala de grises ($36.3\%$ test). Olivetti Faces: diagnóstico del problema de *dying ReLU* y corrección con normalización centrada ($95\%$).
- **Semana 8 (Transfer Learning):** Clasificador propio *bicycle / bus / motorcycle* con EfficientNetB0 (ImageNet): test $97.73\%$ antes y después de fine-tuning (20 capas descongeladas, $\eta=10^{-5}$, `val_loss` reducido a $0.0644$).
- **Módulo 2 (ML + NVIDIA NIM):** Clasificación con árboles en Iris (`max_depth=2` vs `max_depth=5`), consultas LLM con `meta/llama-3.1-8b-instruct` vía NVIDIA NIM, análisis de sobreajuste y verificación con 6 imágenes externas independientes.
- **Semana 10 (Workshop RAG):** Calificación máxima de 100/100 puntos (+0.5 bonificación). Corpus propio de 10 documentos *NexusAI Solutions*, prompt endurecido con fallback estricto («No encuentro esa información en los documentos.»), visualización de scores de similitud coseno, evaluación multilingüe de papers de Attention y RAG, y Retos C1 (Benchmark FAISS HNSW vs FlatL2 con speedup de hasta 29x) y C3 (Gradio con filtrado por metadatos).

---

## Estructura del Repositorio

```text
.
├── README.md
├── requirements.txt
├── evaluaciones/
│   └── parcial_01_pacman/            # Parcial 1: entorno tabular y notebook ejecutado
├── talleres/
│   ├── modulo_01_busqueda_optimizacion_qlearning/ # Taller conceptual + 3 code challenges
│   ├── modulo_02_ml_redes_transformers/          # Taller conceptual + notebook scikit-learn/NIM
│   ├── semana_04_mdp/                            # MDP almacén + imagen del enunciado
│   ├── semana_05_q_learning/                     # Taxi-v4 y FrozenLake
│   ├── semana_06_machine_learning/               # Pipeline ML completo (data, artifacts, reports)
│   ├── semana_07_redes_neuronales/               # CIFAR-10 y Olivetti Faces
│   ├── semana_08_cnn_transfer_learning/          # Transfer learning propio + módulo YOLO
│   └── semana_10_rag/                            # Workshop RAG (README, RESPUESTAS, evidencias, notebooks)
├── quices/
│   └── juanJoseAcevedoOtalvaroGvQuiz01.md        # Análisis de agente en Hugging Face (PEAS)
└── actividades_clase/
    ├── semana_02/                                # Algoritmos de búsqueda en grafos
    ├── semana_09_chatbots_tokenizacion/          # Tokenización y chatbots NVIDIA NIM / Gradio
    └── semana_11_agentes_langgraph/              # Agentes autónomos y flujos con LangGraph
```

---

## Cómo ejecutar

```bash
python3.12 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

Cada notebook se ejecuta desde su propia carpeta (las rutas internas son relativas a ella).
