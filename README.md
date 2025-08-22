# Detección Explicable de Fibrilación Auricular (FA) en Señales de ECG

**Investigación presentada en el Congreso Argentino de Bioingeniería y la Jornada de Ingeniería Clínica (SABI 2025).**

## Resumen

Este proyecto presenta un método para la detección automatizada de Fibrilación Auricular (FA) utilizando un enfoque de **Inteligencia Artificial Explicable (XAI)**. A diferencia de los modelos de "caja negra", nuestro sistema no solo clasifica las señales de ECG con alta precisión, sino que también expone los parámetros fisiológicos clave que influyen en cada decisión. Utilizando el algoritmo XGBoost y las explicaciones de **SHAP (SHapley Additive exPlanations)**, identificamos los biomarcadores más relevantes, ofreciendo transparencia y confianza para el diagnóstico clínico.

**Palabras clave:** Fibrilación Auricular (FA), Inteligencia Artificial Explicable (XAI), Cribado basado en ECG, SHAP.

---

## Autores y Afiliaciones

**Autores:**

- Liberczuk Sergio<sup>1,2,3</sup>
- Garcia Pedro<sup>4,5</sup>
- Barrera Pedro<sup>4</sup>
- Bonomini Maria Paula<sup>3,4,6</sup>

**Afiliaciones:**

1.  Instituto de Ingeniería y Agronomía (IIyA), Universidad Nacional Arturo Jauretche, Fcio. Varela, BsAs, Argentina.
2.  Centro de Altos Estudios en Tecnología Informática (CAETI), Facultad de Tecnología Informática, Universidad Abierta Interamericana (UAI), CABA, Argentina.
3.  Instituto de Ingeniería Biomédica (IIBM), Facultad de Ingeniería, Universidad de Buenos Aires, CABA, Argentina.
4.  Instituto Tecnológico de Buenos Aires (ITBA), CABA, Argentina.
5.  Eccosur Av. Córdoba 1367 Piso 8, Oficina 39, C1055 AAD, CABA, Argentina.
6.  Instituto Argentino de Matemáticas Alberto P. Calderón (IAM), CONICET, CABA, Argentina.

---

## Sobre el Conjunto de Datos

⚠️ **Nota Importante:** Por motivos de confidencialidad y debido a que los datos forman parte de una investigación en curso protegida por acuerdos de privacidad, **no es posible compartir públicamente el conjunto de datos original** utilizado en este estudio.

Sin embargo, para garantizar la reproducibilidad metodológica, a continuación se detalla la estructura y las características de los datos empleados, permitiendo que otros investigadores puedan aplicar el mismo análisis a conjuntos de datos alternativos.

### Descripción de los Datos

* **Fuente:** Señales de ECG de derivación única (single-lead) obtenidas de dispositivos portátiles.
* **Estructura:** El conjunto de datos procesado es una tabla (formato CSV) donde cada fila corresponde a un registro de ECG y cada columna a una característica extraída.
* **Características (Features):** Se extrajo un conjunto de características fisiológicas de cada señal. Para una descripción detallada de cada una, por favor consulte la **Tabla 1 del paper** de esta investigación.
* **Variable Objetivo:** La columna a predecir (`target`) es binaria, indicando la presencia (1) o ausencia (0) de Fibrilación Auricular.

### Alternativa con Datos Públicos

Para quienes deseen replicar el flujo de trabajo de XAI con un conjunto de datos público y de características similares, recomendamos utilizar la base de datos de **PhysioNet**. Específicamente, el desafío **"AF Classification from a Short Single Lead ECG Recording"** es una excelente opción.

-   **Enlace al Desafío:** [PhysioNet Challenge 2017](https://physionet.org/content/challenge-2017/1.0.0/)
-   **Adaptación:** Para usar estos datos, se debería implementar un script de preprocesamiento que extraiga las mismas características descritas en nuestro paper a partir de las señales en formato `.mat` provistas por PhysioNet.

---

## Cómo Replicar este Estudio

Para ejecutar el análisis y obtener los resultados presentados, sigue estos pasos.

### Prerrequisitos

Asegúrate de tener Python 3.8 o superior. Las librerías necesarias se encuentran en el archivo `requirements.txt`.

### Instalación

1.  **Clona este repositorio:**
    ```bash
    git clone [https://github.com/tu-usuario/XAI-Atrial-Fibrillation-Detection.git](https://github.com/tu-usuario/XAI-Atrial-Fibrillation-Detection.git)
    cd XAI-Atrial-Fibrillation-Detection
    ```

2.  **Crea un entorno virtual (recomendado):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # En Windows: venv\Scripts\activate
    ```

3.  **Instala las dependencias:**
    ```bash
    pip install -r requirements.txt
    ```

### Ejecución

El análisis completo, desde la carga de datos hasta la generación de explicaciones SHAP, se encuentra en el notebook Jupyter:

-   [`notebooks/XAI_Atrial_Fibrillation_Analysis.ipynb`](./notebooks/XAI_Atrial_Fibrillation_Analysis.ipynb)

Puedes abrirlo con Jupyter Lab, Jupyter Notebook, o directamente en Google Colab.

---

## Estructura del Repositorio

-   `notebooks/`: Contiene el notebook con todo el código del análisis exploratorio, entrenamiento del modelo y la aplicación de XAI.
-   `requirements.txt`: Lista de las librerías de Python necesarias para replicar el entorno de ejecución.
-   `LICENSE`: Licencia MIT, que permite la reutilización del código con la debida atribución.
-   `README.md`: Este archivo, que documenta el proyecto.

---

## Modelo y Resultados

Se entrenó un clasificador **XGBoost** que alcanzó un alto rendimiento en la detección de FA. Las explicaciones generadas por SHAP revelaron que las características más influyentes para el modelo son:

-   **Variabilidad del ritmo cardíaco (HRV):** Métricas como `P_RMSSD`, `P_SDNN` y la entropía (`P_SamEn`, `P_ShEn`) fueron consistentemente determinantes.
-   **Morfología de la señal:** Parámetros relacionados con la irregularidad y la complejidad del intervalo RR.

Estas visualizaciones (gráficos de cascada, dependencia y resumen de SHAP) permiten a un especialista comprender *por qué* una señal específica es clasificada como FA, aumentando la confianza en el sistema.
