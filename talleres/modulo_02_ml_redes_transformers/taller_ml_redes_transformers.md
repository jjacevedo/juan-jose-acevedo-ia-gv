# Taller: Aprendizaje Supervisado, Redes Neuronales y Transformers

**Curso:** SI3003 — Inteligencia Artificial  
**Sesiones:** 6, 7, 8 y 9  
**Estudiante:** Juan José Acevedo Otálvaro  
**Universidad EAFIT**

---

## Parte A. Preguntas conceptuales (40 %)

### 1. Generalización y evaluación

* **¿Cuál elegiría inicialmente y qué sugieren estos resultados sobre el sobreajuste?**  
  Elegiría el segundo modelo (88 % train / 85 % val). El primer modelo evidencia sobreajuste (*overfitting*) severo al tener una brecha de 28 puntos porcentuales (100 % vs 72 %), mientras que el segundo generaliza mucho mejor con solo 3 puntos de diferencia y una exactitud en validación notablemente superior (85 % vs 72 %).

* **Un compañero propone probar distintas profundidades sobre el conjunto de prueba y entregar la mejor. ¿Qué problema tiene esa estrategia?**  
  Comete *fuga de información* (*data leakage* / contaminación del test set). El conjunto de prueba debe reservarse exclusivamente para la evaluación final imparcial; optimizar hiperparámetros sobre él sobreajusta la selección a esa muestra y anula la estimación del error real de generalización.

---

### 2. Árboles: elegir una división

Un nodo contiene 4 positivos y 4 negativos ($N=8$, $p=0.5$). Entropía inicial:  
$$H(0.5) = -0.5\log_2(0.5) - 0.5\log_2(0.5) = 1.0 \text{ bit}$$

1. **Cálculo de entropía inicial y ganancia de cada atributo:**
   * **Atributo A:**  
     * Rama izquierda: 3 pos, 1 neg ($p = 0.75 \implies H(0.75) \approx 0.811$ bits).  
     * Rama derecha: 1 pos, 3 neg ($p = 0.25 \implies H(0.25) \approx 0.811$ bits).  
     * Entropía ponderada: $\frac{4}{8}(0.811) + \frac{4}{8}(0.811) = 0.811$ bits.  
     * **Ganancia(A):** $1.0 - 0.811 = \mathbf{0.189}$ **bits**.
   * **Atributo B:**  
     * Ambas ramas tienen 2 pos y 2 neg ($p = 0.5 \implies H(0.5) = 1.0$ bit).  
     * Entropía ponderada: $\frac{4}{8}(1.0) + \frac{4}{8}(1.0) = 1.0$ bit.  
     * **Ganancia(B):** $1.0 - 1.0 = \mathbf{0.0}$ **bits**.
   * *Elección del árbol:* El árbol elige el **Atributo A** porque aporta la mayor ganancia de información ($0.189 > 0$), reduciendo la incertidumbre y separando parcialmente las clases.

2. **Atributo identificador único (ID único):**  
   * Al aislar cada uno de los 8 ejemplos en su propia hoja pura, la entropía en cada hoja es $H=0$, obteniendo una **ganancia máxima de 1.0 bit** ($1.0 - 0$).  
   * *¿Por qué generaliza peor?* Porque memoriza la muestra particular creando una regla espuria por cada ID. Ante cualquier ejemplo nuevo con un ID no visto en entrenamiento, el árbol no tiene ninguna regla general aplicable, colapsando su capacidad predictiva.

---

### 3. Redes: predicciones y pérdida

Etiqueta real: **perro**.  
* Modelo A: $P(\text{gato})=0.35, P(\text{perro})=0.40, P(\text{ave})=0.25$.  
* Modelo B: $P(\text{gato})=0.05, P(\text{perro})=0.90, P(\text{ave})=0.05$.

1. **Clase predicha y exactitud:**  
   Ambos modelos predicen **perro** ($\arg\max$). Su exactitud sobre esta muestra individual es idéntica ($1.0$ o 100 %), ya que la exactitud es binaria y no mide la confianza de la predicción.

2. **Cálculo de entropía cruzada $L = -\ln P(\text{clase real})$:**  
   * **Modelo A:** $L_A = -\ln(0.40) \approx \mathbf{0.9163}$.  
   * **Modelo B:** $L_B = -\ln(0.90) \approx \mathbf{0.1054}$.  
   * *Diferencia detectada:* La pérdida cuantifica la certeza y calibración: el Modelo B es casi 9 veces mejor penalizado que el Modelo A ($0.1054 \ll 0.9163$), reflejando que el Modelo A tiene una probabilidad vacilante e insegura.

3. **Para otra imagen de perro, un modelo asigna $P(\text{perro})=0.01$:**  
   * Pérdida: $L = -\ln(0.01) \approx \mathbf{4.6052}$.  
   * *Explicación:* La función logarítmica penaliza asintóticamente el error con alta confianza, produciendo un error masivo y gradientes de gran magnitud que obligan a corregir enérgicamente los pesos en backpropagation.

4. **Entrenamiento y no-linealidades:**  
   * Durante el entrenamiento se modifican los **pesos y sesgos** ($W$ y $b$), las etiquetas permanecen constantes.  
   * Apilar capas sin funciones de activación no lineales colapsa toda la red a una sola transformación lineal combinada ($W_2(W_1 x + b_1) + b_2 = W' x + b'$), impidiendo aprender fronteras de decisión complejas o resolver problemas no lineales como XOR.

---

### 4. CNN: tamaño de salida y filtros

Entrada: $32 \times 32 \times 3$. Filtros: 16 de tamaño $3 \times 3$, stride $S=1$, padding $P=1$.

* **Cálculo del tamaño de salida:**  
  $$\text{Alto} = \left\lfloor \frac{32 - 3 + 2(1)}{1} \right\rfloor + 1 = 32, \quad \text{Ancho} = \left\lfloor \frac{32 - 3 + 2(1)}{1} \right\rfloor + 1 = 32$$  
  Número de canales = 16 (uno por cada filtro convolucional).  
  **Tamaño final de salida:** $\mathbf{32 \times 32 \times 16}$.

* **Ventaja de compartir el mismo filtro (*parameter sharing*):**  
  Proporciona **equivarianza/invarianza a la traslación** (detecta una característica sin importar dónde se ubique) y reduce exponencialmente el número de parámetros a aprender (solo $16 \times (3 \times 3 \times 3 + 1) = 448$ pesos), mitigando drásticamente el sobreajuste.

---

### 5. Transferencia

* **Elección:** Reutilizaría una red preentrenada (**Transfer Learning**).  
* **Justificación:** 300 imágenes (100 por clase) son radicalmente insuficientes para entrenar desde cero los millones de parámetros de una CNN sin caer en sobreajuste masivo. Una arquitectura preentrenada (ej. MobileNet o EfficientNet en ImageNet) ya cuenta con detectores universales de bordes y texturas; basta con congelar la base y ajustar la cabeza densa final.

---

### 6. Completar texto con probabilidades de tokens

Contexto inicial: **«El estudiante»** ($c$).

1. **Selección voraz (*greedy*):**  
   * Primer token: $\max(0.50, 0.30, 0.20) \implies \mathbf{aprende}$ ($0.50$).  
   * Segundo token (dado «aprende»): $\max(0.40, 0.35, 0.25) \implies \mathbf{IA}$ ($0.40$).  
   * **Texto generado:** **«El estudiante aprende IA»**.

2. **Cálculo y comparación de probabilidades conjuntas:**  
   * $P(\text{aprende, IA} \mid c) = 0.50 \times 0.40 = \mathbf{0.200}$ ($20\%$).  
   * $P(\text{estudia, IA} \mid c) = 0.30 \times 0.90 = \mathbf{0.270}$ ($27\%$).  
   * *¿La selección voraz produjo la más probable?* **No**. La selección voraz eligió «aprende IA» ($0.200$), pero la secuencia globalmente más probable es «estudia IA» ($0.270$). Esto demuestra que la optimización miope de un paso (*greedy*) no garantiza el óptimo global.

3. **Sorteo estocástico del primer token:**  
   * Sí podría aparecer «duerme», ya que posee una probabilidad no nula del 20 % ($P=0.20$).  
   * Repetir la consulta no produce obligatoriamente el mismo texto, debido a la naturaleza aleatoria del muestreo multinomial en cada iteración.

4. **Dependencia condicional y veracidad:**  
   * La distribución del segundo token depende del primero por la regla de la cadena autorregresiva $P(t_2 \mid c, t_1)$, donde cada palabra previa reconfigura el contexto semántico.  
   * Que una afirmación tenga alta probabilidad estadística solo refleja patrones frecuentes en el corpus de preentrenamiento, pero no garantiza en absoluto que sea un hecho verídico en el mundo real.

---

## Parte B. Uso de herramientas (60 %)

### 7. Entrenar un clasificador con scikit-learn (20 %)

* **Características de entrada:** 4 variables morfológicas (`sepal length`, `sepal width`, `petal length`, `petal width`).  
* **Clases de salida:** 3 especies (`setosa`, `versicolor`, `virginica`).  
* **Particiones:** Entrenamiento = 90, Validación = 30, Prueba = 30 (estratificadas).

| Experimento | Profundidad (`max_depth`) | Exactitud Entrenamiento | Exactitud Validación |
|---|:---:|:---:|:---:|
| 1 | 2 | 0.9667 (96.7 %) | **0.9333 (93.3 %)** |
| 2 | 5 | 1.0000 (100.0 %) | **0.9333 (93.3 %)** |

* **Modelo seleccionado:** Árbol con `max_depth=2`.  
  * *Criterio de desempate:* Ambos alcanzan exactamente la misma exactitud en validación ($93.33\%$). Aplicando el principio de parsimonia (Navaja de Ockham), el árbol de profundidad 2 es preferible por ser más simple, interpretable y menos propenso a memorizar ruido.
* **Evaluación final en prueba:** **0.9333 (93.33 %)**.
* **Análisis de profundidad y sobreajuste:**  
  Aumentar la profundidad a 5 no mejoró en absoluto el rendimiento sobre datos no vistos (se mantuvo en 93.33 %), pero elevó el entrenamiento al 100 %. Obtener 100 % en entrenamiento no garantiza acertar en datos nuevos; por el contrario, suele ser síntoma inequívoco de sobreajuste por memorización de puntos frontera.

---

### 8. Consultar un LLM con NVIDIA NIM (20 %)

* **Modelo utilizado:** `meta/llama-3.1-8b-instruct` vía API NVIDIA NIM.
* **Consulta 1 (Pregunta propia):**  
  *Pregunta:* «¿Por qué en transfer learning congelamos las capas convolucionales base antes de entrenar la cabeza clasificadora?»  
  *Respuesta obtenida:* Se congelan para conservar los filtros visuales universales (bordes, texturas) aprendidos en ImageNet. Si no se congelaran, los gradientes grandes de una cabeza aleatoria destruirían esos pesos (olvido catastrófico) causando sobreajuste en datasets pequeños.
* **Consulta 2 (Consulta mejorada con restricciones):**  
  *Prompt:* «Explícale a un estudiante novato por qué en transfer learning congelamos la base convolucional antes de entrenar la cabeza. Da un ejemplo de la vida real y responde en máximo 100 palabras.»  
  *Respuesta obtenida:* Análoga a un chef profesional al que se le enseña una nueva receta: no necesita aprender a cortar ni hornear (ya lo domina). Congelar la base preserva esa experiencia previa y solo entrena la última capa para clasificar las nuevas categorías sin arruinar lo aprendido.
* **Consulta 3 (Verificación de afirmación sobre 100 % en entrenamiento):**  
  *Pregunta:* «Un árbol con 100 % de exactitud en entrenamiento siempre será el mejor en datos nuevos. ¿Es correcta? Justifica tu respuesta.»  
  *Respuesta obtenida:* Falso. Un árbol al 100 % suele sufrir de sobreajuste, memorizando particularidades y ruido del conjunto de entrenamiento. En datos no vistos su exactitud suele caer frente a árboles podados más generales.
* **Análisis crítico de la interacción:**  
  * La consulta mejorada ganó contundencia pedagógica y síntesis al delimitar el público objetivo y la extensión estricta.  
  * Las respuestas del LLM son lingüísticamente verosímiles pero deben contrastarse empíricamente con métricas de validación.  
  * Durante estas consultas **no se entrenó el modelo** ni se actualizaron sus pesos; únicamente se ejecutó **inferencia** (*forward pass*) sobre un modelo preentrenado congelado.

---

### 9. Retomar el clasificador con datos propios (20 %)

Basado en el trabajo del [Taller de Transfer Learning (Sesión 8)](../semana_08_cnn_transfer_learning/taller_transfer_learning_datos_propios_keras3.ipynb):

1. **Datos y adaptación arquitectónica:**  
   * **Clases:** `bicycle`, `bus`, `motorcycle` (3 clases).  
   * **Imágenes totales:** 270 (93 bicicletas, 86 buses, 91 motocicletas).  
   * **Particiones:** Entrenamiento = 188, Validación = 38, Prueba = 44.  
   * **Modelo base:** `EfficientNetB0` preentrenado en ImageNet.  
   * **Adaptación:** Toda la base permaneció congelada al inicio; se entrenó una cabeza personalizada con `GlobalAveragePooling2D`, `BatchNormalization`, `Dropout(0.3)`, `Dense(64, relu)`, `Dropout(0.2)` y `Dense(3, softmax)`.

2. **Antes y después del ajuste fino (*fine-tuning*):**  
   * **Fase 1 (Cabeza):** $\eta = 10^{-3}$, 10 épocas $\implies$ `val_accuracy = 0.9737`, `test_accuracy = 0.9773` (`val_loss = 0.0792`).  
   * **Fase 2 (Fine-tuning):** Se descongelaron las últimas 20 capas del modelo base con tasa muy reducida $\eta = 10^{-5}$, 8 épocas $\implies$ `val_accuracy = 0.9737`, `test_accuracy = 0.9773`.  
   * *Efecto del fine-tuning:* La exactitud se mantuvo idéntica en test ($97.73\%$), pero la pérdida de validación mejoró de $0.0792$ a **$0.0644$**, lo que indica que las probabilidades predichas quedaron mejor calibradas.

3. **Evaluación de 6 imágenes nuevas independientes:**

| Imagen | Clase real | Clase predicha | Probabilidad predicha | ¿Acertó? |
|---|---|---|---:|:---:|
| 1 (`bici_urbana.jpg`) | `bicycle` | `bicycle` | 0.984 | **Sí** |
| 2 (`bici_ruta.jpg`) | `bicycle` | `bicycle` | 0.976 | **Sí** |
| 3 (`bus_articulado.jpg`) | `bus` | `bus` | 0.998 | **Sí** |
| 4 (`bus_escolar.jpg`) | `bus` | `bus` | 0.992 | **Sí** |
| 5 (`moto_scooter.jpg`) | `motorcycle` | `motorcycle` | 0.989 | **Sí** |
| 6 (`moto_cross.jpg`) | `motorcycle` | `motorcycle` | 0.965 | **Sí** |

4. **Análisis de errores y generalización:**  
   * *Análisis de las imágenes de menor confianza:* Las imágenes 2 (`bici_ruta.jpg`, 0.976) y 6 (`moto_cross.jpg`, 0.965) presentaron menor certeza relativa debido a fondos de vegetación compleja y ángulos frontales cerrados donde la estructura de dos ruedas y manubrio presenta rasgos geométricos compartidos entre bicicletas y motos.  
   * *Mejora en los datos:* Incluir mayor diversidad de tomas frontales y tomas nocturnas con variaciones de iluminación artificial.  
   * *Límite de la muestra pequeña:* Acertar 6 de 6 imágenes es una comprobación cualitativa positiva pero estadísticamente insuficiente para garantizar generalización universal; se requiere evaluar en grandes conjuntos de prueba representativos con métricas agregadas (F1-score macro, matriz de confusión).
