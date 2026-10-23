# Taller: Búsqueda, Optimización y Q-Learning (Resuelto)

**Curso:** SI3003 — Inteligencia Artificial  
**Estudiante:** Juan José Acevedo Otálvaro  
**Universidad EAFIT**

---

## 1. Algoritmos de búsqueda

Considere el grafo del problema con costos en las aristas:
* $S \to A$ (costo 2), $S \to B$ (costo 1)
* $A \to C$ (costo 2), $A \to G$ (costo 5)
* $B \to D$ (costo 2), $B \to G$ (costo 4)
* $C \to G$ (costo 2)
* $D \to G$ (costo 1)

Estado inicial: $S$. Objetivo: $G$. Expansión de sucesores: de izquierda a derecha ($A$ antes que $B$).

### Actividad

1. **Contenido de la frontera después de expandir $S$:**
   * **BFS (Cola FIFO):** `[A, B]`
   * **DFS (Pila LIFO):** `[B, A]` (o `[A, B]` si se apila primero $B$ y queda $A$ en el tope)
   * **UCS (Cola de prioridad por costo acumulado $g$):** `[(B, g=1), (A, g=2)]`

2. **Siguiente nodo que se expande para cada algoritmo:**
   * **BFS:** Expande **$A$** (primer elemento en la cola FIFO).
   * **DFS:** Expande **$A$** (nodo en el tope de la pila / rama izquierda más profunda).
   * **UCS:** Expande **$B$** (nodo con el menor costo acumulado $g(B) = 1$).

3. **Expansiones necesarias hasta que UCS seleccione el objetivo $G$:**

| Iteración | Nodo seleccionado | Costo acumulado $g(n)$ | Frontera después de expandir |
|---:|:---:|:---:|---|
| **1** | $S$ | 0 | `{(B, g=1), (A, g=2)}` |
| **2** | $B$ | 1 | `{(A, g=2), (D, g=3), (G, g=5)}` |
| **3** | $A$ | 2 | `{(D, g=3), (C, g=4), (G, g=5)}` |
| **4** | $D$ | 3 | `{(C, g=4), (G, g=4)}` *(alcanza $G$ por $D$ con $3+1=4 < 5$)* |
| **5** | $C$ *(o desempate)* | 4 | `{(G, g=4)}` |
| **6** | **$G$** | **4** | **Objetivo seleccionado** *(meta alcanzada)* |

4. **Preguntas de análisis:**
   * **a. ¿Por qué UCS selecciona primero $B$, aunque $A$ y $B$ estén en la misma profundidad?**  
     Porque UCS ignora la profundidad y prioriza estrictamente por la función de costo acumulado $g(n)$. Como $g(B) = 1 < g(A) = 2$, $B$ tiene mayor prioridad en la cola.
   * **b. ¿Cuál camino encuentra UCS?**  
     Encuentra el camino **$S \to B \to D \to G$**, con un costo total óptimo de **$g = 4$** ($1 + 2 + 1$).
   * **c. ¿El primer camino que llega a $G$ necesariamente es el camino que UCS debe aceptar? Justifique.**  
     **No.** Un camino puede descubrir a $G$ tempranamente al expandir un nodo (por ejemplo, al expandir $B$ se genera $G$ con costo 5), pero UCS solo acepta la meta cuando esta es **extraída de la frontera** como el nodo de menor costo de toda la cola. Esto garantiza optimalidad en grafos con costos no negativos.
   * **d. Si todas las conexiones tuvieran costo 1, ¿qué relación existiría entre BFS y UCS?**  
     Serían algoritmos **equivalentes**. Cuando todos los costos son uniformes ($c=1$), el costo acumulado $g(n)$ coincide exactamente con la profundidad $d(n)$, por lo que la cola de prioridad de UCS se comporta de forma idéntica a la cola FIFO de BFS.

---

## 2. Optimización: Simulated Annealing

Estado actual: $f(s_{\text{actual}}) = 8$. Vecino generado: $f(s_{\text{nuevo}}) = 11$. Temperatura: $T = 4$.  
Minimización: $\Delta = f(s_{\text{nuevo}}) - f(s_{\text{actual}})$. Probabilidad de aceptación si empeora: $P(\text{aceptar}) = e^{-\Delta / T}$.  
Número aleatorio generado: $r = 0.35$.

### Actividad

1. **Cálculo de $\Delta$:**  
   $$\Delta = 11 - 8 = \mathbf{+3}$$

2. **¿El nuevo estado es mejor o peor?**  
   Es **peor**, porque en un problema de minimización un costo mayor implica menor calidad de solución ($\Delta > 0$).

3. **Cálculo de la probabilidad de aceptación:**  
   $$P(\text{aceptar}) = e^{-3 / 4} = e^{-0.75} \approx \mathbf{0.4724} \quad (\approx 47.24\%)$$

4. **Comparación con $r$ y decisión del algoritmo:**  
   Como $r = 0.35 \le 0.4724$, la condición estocástica se cumple. El algoritmo **SÍ acepta el movimiento** hacia el estado peor.

5. **Efecto de la temperatura:**  
   * **a. Si $T = 0.5$:** $\Delta / T = 3 / 0.5 = 6 \implies P = e^{-6} \approx \mathbf{0.0025}$ ($0.25\%$). La probabilidad es casi nula; el algoritmo casi nunca aceptaría empeorar (comportamiento puramente explotador/voraz).  
   * **b. Si $T = 20$:** $\Delta / T = 3 / 20 = 0.15 \implies P = e^{-0.15} \approx \mathbf{0.8607}$ ($86.07\%$). Aceptaría con alta frecuencia casi cualquier movimiento (comportamiento altamente explorador).

6. **Preguntas conceptuales:**  
   * **a. ¿Por qué Simulated Annealing puede aceptar una solución peor?**  
     Para tener la capacidad de escapar de óptimos locales y mesetas donde un algoritmo voraz quedaría irremediablemente atrapado.
   * **b. ¿Qué ventaja tiene esta decisión frente a Hill Climbing?**  
     Permite explorar regiones distintas del espacio de búsqueda y encontrar el óptimo global, mientras que Hill Climbing se detiene en el primer pico/valle local que encuentra.
   * **c. ¿Qué debería ocurrir con la exploración cuando $T \to 0$?**  
     La exploración debe desaparecer gradualmente y dar paso a la explotación pura: $P(\text{aceptar}) \to 0$ para empeoramientos, comportándose exactamente como Hill Climbing voraz en la fase final.
   * **d. Si el vecino tuviera costo 5, ¿sería necesario calcular una probabilidad?**  
     **No.** Como $5 < 8$, se trata de una mejora estricta ($\Delta = -3 < 0$), por lo que en Simulated Annealing las mejoras se aceptan de manera determinista e inmediata ($P=1$).

---

## 3. Q-Learning

Estado actual: $S$. Parámetros: $\alpha = 0.5$, $\gamma = 0.9$.  
Valor en el siguiente estado $S'$: $\max_{a'} Q(S', a') = 4$.  
Acción seleccionada: **Avanzar** (resultado inmediato: llega a $S'$, $r = +1$, $Q(S, \text{Avanzar}) = 2.0$).

### Actividad

1. **Valores identificados:**  
   * $Q(S, \text{Avanzar}) = \mathbf{2.0}$  
   * Recompensa inmediata $r = \mathbf{+1}$  
   * $\max_{a'} Q(S', a') = \mathbf{4}$

2. **Cálculo del objetivo temporal (TD Target):**  
   $$\text{Target} = r + \gamma \max_{a'} Q(S', a') = 1 + 0.9(4) = 1 + 3.6 = \mathbf{4.6}$$

3. **Cálculo del error temporal (TD Error $\delta$):**  
   $$\delta = \text{Target} - Q(S, \text{Avanzar}) = 4.6 - 2.0 = \mathbf{+2.6}$$

4. **Actualización de $Q(S, \text{Avanzar})$:**  
   $$Q(S, \text{Avanzar}) \leftarrow 2.0 + 0.5(2.6) = 2.0 + 1.3 = \mathbf{3.3}$$

5. **¿El valor aumentó o disminuyó y por qué?**  
   **Aumentó** (de 2.0 a 3.3). Aumentó porque el retorno esperado observado (la recompensa inmediata $+1$ más el valor descontado del estado futuro $3.6$, total $4.6$) fue superior a la estimación previa ($2.0$), produciendo un error temporal positivo ($\delta = +2.6$).

---

### Preguntas de análisis

6. **Si el agente aprende correctamente, ¿cómo debería ser el valor de Saltar frente a las demás acciones?**  
   Debería ser significativamente más bajo y fuertemente negativo ($Q(S, \text{Saltar}) \ll Q(S, \text{Avanzar})$), reflejando la penalización catastrófica de morir ($-10$).

7. **Si morir termina inmediatamente el episodio, ¿se debe considerar el valor de un estado futuro en la actualización de Saltar?**  
   **No.** Al ser un estado terminal, el episodio finaliza y no existen transiciones futuras ni recompensas subsiguientes; por lo tanto, el término $\max_{a'} Q(S', a')$ es formalmente $0$, y la actualización depende únicamente de la recompensa inmediata: $r + \gamma(0) = r = -10$.

8. **¿Por qué el valor actual de $Q(S, \text{Saltar}) = -2$ todavía podría ser demasiado alto?**  
   Porque la recompensa real de morir es $-10$. Un valor de $-2$ indica que el agente ha probado pocas veces esa transición y el valor Q aún no ha convergido a su retorno acumulado real; a medida que se apliquen actualizaciones, $Q$ convergerá hacia $-10$.

9. **Según la tabla actual, ¿qué acción seleccionaría una política completamente voraz?**  
   Seleccionaría **Avanzar**, ya que posee el valor $Q$ más alto: $\max(2.0, 0.5, -2.0) = 2.0$.

10. **¿Significa lo anterior que el agente nunca puede seleccionar otra acción durante el entrenamiento?**  
    **No.** Si se utiliza una política $\varepsilon$-greedy, con probabilidad $1 - \varepsilon$ explotará eligiendo Avanzar, pero con probabilidad $\varepsilon$ explorará seleccionando uniformemente al azar entre todas las acciones disponibles (incluyendo Esperar o Saltar), permitiendo descubrir nueva información sobre el entorno.

11. **Si Avanzar entregara recompensa inmediata 0 pero condujera a recompensas altas a futuro, ¿puede tener un valor Q alto?**  
    **Sí.** Gracias al término de descuento $\gamma \max_{a'} Q(S', a')$, el algoritmo propaga hacia atrás el valor de las recompensas futuras diferidas; por tanto, una acción con $r=0$ que conduzca a un estado con valor $100$ alcanzará un valor $Q \approx \gamma(100) = 90$.

12. **Control y efecto de los hiperparámetros:**

| Parámetro | ¿Qué controla? | ¿Qué podría ocurrir si es muy alto? |
|---|---|---|
| **$\alpha$** *(Tasa de aprendizaje)* | La velocidad a la que se incorporan nuevas observaciones frente al conocimiento acumulado. | Si es muy alto ($\alpha \to 1$), el agente sobreescribe agresivamente sus valores $Q$ con cada nueva experiencia; en entornos estocásticos el aprendizaje oscila y no converge. |
| **$\gamma$** *(Factor de descuento)* | La importancia relativa de las recompensas futuras frente a las inmediatas (horizonte temporal). | Si es muy alto ($\gamma \approx 1$ o $>1$), el agente puede volverse miope a costos inmediatos buscando retornos infinitamente lejanos, y en tareas sin término el valor Q puede divergir. |
| **$\varepsilon$** *(Tasa de exploración)* | La probabilidad de seleccionar una acción aleatoria para explorar el entorno en vez de la mejor conocida. | Si es muy alto ($\varepsilon \to 1$), el agente actúa casi puramente al azar, desaprovechando el conocimiento aprendido y sufriendo penalizaciones innecesarias. |
