# SI3003 — Inteligencia Artificial

**Universidad EAFIT** · Juan José Acevedo Otálvaro

Repositorio personal con los talleres, quices y actividades de la asignatura. Los archivos base de cada taller vienen del repositorio oficial del curso: [EAFIT-IA/si3003-artificial-intelligence](https://github.com/EAFIT-IA/si3003-artificial-intelligence).

## Entregables: talleres semanas 4 a 8

Cada notebook se completó **sobre el archivo original del profesor** (se conservan sus explicaciones y celdas resueltas), se ejecutó de principio a fin y se guardó con sus salidas.

| Semana | Tema | Entregable | Notebook original |
|---|---|---|---|
| 4 | Procesos de Decisión de Markov | [`03_lab_warehouse_mdp.ipynb`](talleres/semana_04_mdp/03_lab_warehouse_mdp.ipynb) | `notebooks/lecture4/03_lab_warehouse_mdp_estudiantes.ipynb` |
| 5 | Q-Learning | [`03_qlearning_taxi.ipynb`](talleres/semana_05_q_learning/03_qlearning_taxi.ipynb) | `notebooks/lecture5/03_qlearning_taxi.ipynb` |
| 5 | *(trabajo en clase)* | [`02_qlearning_frozenlake.ipynb`](talleres/semana_05_q_learning/02_qlearning_frozenlake.ipynb) | `notebooks/lecture5/02_qlearning_frozenlake.ipynb` |
| 6 | Machine Learning: pipeline de clasificación | [`01_data_challenge.ipynb`](talleres/semana_06_machine_learning/01_data_challenge.ipynb) → [`02_training_challenge.ipynb`](talleres/semana_06_machine_learning/02_training_challenge.ipynb) → [`03_evaluation_deployment_challenge.ipynb`](talleres/semana_06_machine_learning/03_evaluation_deployment_challenge.ipynb) | `notebooks/lecture6/challenge/` |
| 7 | Modelos lineales y redes neuronales (Keras 3) | [`Challenge_Keras3_CIFAR10_Grayscale.ipynb`](talleres/semana_07_redes_neuronales/Challenge_Keras3_CIFAR10_Grayscale.ipynb), [`Challenge_Keras3_OlivettiFaces.ipynb`](talleres/semana_07_redes_neuronales/Challenge_Keras3_OlivettiFaces.ipynb) | `notebooks/lecture7/` |
| 8 | CNN y transfer learning | [`taller_transfer_learning_datos_propios_keras3.ipynb`](talleres/semana_08_cnn_transfer_learning/taller_transfer_learning_datos_propios_keras3.ipynb) | `notebooks/lecture8/transfer_learning/` |
| 8 | *(ejercicio YOLO)* | [`yolo/Lecture_08_Yolo_Intro.ipynb`](talleres/semana_08_cnn_transfer_learning/yolo/Lecture_08_Yolo_Intro.ipynb) | `notebooks/lecture8/yolo/Lecture_08_Yolo_Intro.ipynb` |

### Resultados principales

- **Semana 4:** MDP del almacén modelado a partir de la imagen del enunciado; Value Iteration y Policy Iteration encuentran la misma política. Se incluyen las respuestas de la Parte 5, los experimentos A, B y C y el bonus (umbral de `living_reward` ≈ −0.79).
- **Semana 5:** Q-Learning en Taxi-v4; la política greedy completa el 100 % de 100 episodios de prueba. Experimento: α = 0.1 vs α = 0.5.
- **Semana 6:** dataset Wine (3 clases). Campeón por validación cruzada: regresión logística (CV 0.979); test: accuracy 0.972, F1 macro 0.971.
- **Semana 7:** CIFAR-10 en gris: 36.3 % en test. Olivetti: con la configuración pedida la red no aprende (2.5 %, *dying ReLU*); se documenta un diagnóstico adicional (entradas centradas: 95 %).
- **Semana 8:** clasificador propio *bicycle / bus / motorcycle* con EfficientNetB0: test 97.7 % antes y después del fine-tuning, con análisis de errores.

## Estructura

```text
.
├── README.md
├── requirements.txt
├── talleres/                         # entregables semanas 4–8
│   ├── semana_04_mdp/                # notebook + img/warehouse.png (imagen del enunciado)
│   ├── semana_05_q_learning/
│   ├── semana_06_machine_learning/   # 3 notebooks + data/, artifacts/, reports/ que generan
│   ├── semana_07_redes_neuronales/
│   └── semana_08_cnn_transfer_learning/
│       └── yolo/
├── quices/
│   └── juanJoseAcevedoOtalvaroGvQuiz01.md   # análisis de un agente en Hugging Face Spaces (PEAS)
└── actividades_clase/
    └── semana_02/02_algoritmos_busqueda_grafo.ipynb   # BFS, UCS, GBF y A*
```

## Cómo ejecutar

```bash
python3.12 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

Cada notebook se ejecuta desde su propia carpeta (las rutas son relativas a ella).

- **Semana 6:** ejecutar en orden `01` → `02` → `03`. Los archivos de `data/processed/`, `artifacts/` y `reports/` son las salidas de esos notebooks.
- **Semana 7:** CIFAR-10 y Olivetti Faces se descargan automáticamente (Keras / scikit-learn).
- **Semana 8:** el dataset propio (`data_raw/`, `dataset/`) **no se sube** al repositorio porque son imágenes de internet con licencias desconocidas. Si `data_raw/` no existe, el notebook vuelve a descargar las imágenes con las mismas búsquedas; como el buscador cambia sus resultados, el dataset y las métricas pueden diferir de las guardadas. La lista de imágenes eliminadas en la limpieza está en el propio notebook. Los pesos `yolo26n.pt` los descarga Ultralytics automáticamente.
