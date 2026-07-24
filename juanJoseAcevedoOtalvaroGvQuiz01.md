# Actividad de Clase: Analizando Agentes de IA con Hugging Face Spaces

## 1. Nombre del Space

**Nombre:** WANMAN

**Enlace:** https://huggingface.co/spaces/loveseries/wanmanlove



## 2. ¿Qué hace el agente?

Es un sistema de inteligencia artificial que genera videos a partir de una imagen y/o un texto. El usuario proporciona las entradas y el modelo crea un video que intenta representar lo solicitado.



## 3. Análisis PEAS

**Performance:** El agente hace bien su trabajo cuando genera un video de buena calidad, que sea coherente con la imagen y el texto proporcionados, y lo hace en un tiempo razonable.

**Environment:** Interactúa con el usuario, la interfaz web de Hugging Face y los archivos de entrada, como imágenes y texto.

**Actuators:** Genera un video, lo muestra en pantalla y permite descargarlo.

**Sensors:** Recibe como entrada una imagen, un texto (prompt) y parámetros de configuración como la resolución o la duración del video.



## 4. Clasificación del entorno

**Observable:** Parcial. El agente solo conoce la información que el usuario le proporciona.

**Determinista:** No. Con la misma entrada pueden obtenerse resultados diferentes debido al proceso de generación.

**Episódico:** Sí. Cada generación de un video es independiente de las anteriores.

**Estático:** Sí. Mientras el agente genera el video, la entrada no cambia.

**Discreto:** No. Trabaja con imágenes, texto y video, que son datos continuos.

**Conocido:** Sí. El agente conoce las reglas del entorno y cómo procesar las entradas para generar una salida.



## 5. ¿Qué tipo de programa de agente creen que es?

**Agente basado en objetivos.**

Se clasifica así porque el usuario le da un objetivo (generar un video con ciertas características) y el agente intenta producir un resultado que cumpla ese objetivo. Aunque el modelo probablemente haya sido entrenado con aprendizaje automático, durante su uso no aprende de las interacciones del usuario, sino que utiliza el conocimiento adquirido durante el entrenamiento.x

## Juan José Acevedo Otálvaro