# Análisis Cuantitativo de la Distorsión de Precios Inmobiliarios en el Corredor Vaca Muerta (2019-2020)

> **Evaluación del impacto económico de la industria hidrocarburífera sobre el mercado inmobiliario residencial en la cuenca neuquina.**

## Descripción del Proyecto

Este proyecto presenta un análisis exploratorio y estadístico (EDA) del mercado inmobiliario en la provincia de Neuquén y Río Negro, diseñado para aislar y cuantificar el fenómeno conocido como **"Efecto Vaca Muerta"**.

Utilizando un dataset de avisos clasificados de kaggle correspondiente al periodo de alta actividad **2019-2020**, se aplicaron técnicas de análisis de datos para evaluar cómo la demanda industrial distorsiona los precios residenciales, desacoplándolos de las variables urbanas tradicionales (infraestructura y servicios).
<img width="1187" height="677" alt="image" src="https://github.com/user-attachments/assets/467bcdde-d1f0-4870-886f-9e483a24dbe0" />

Ante la limitación de datos históricos extensos, decidí cambiar el enfoque: en lugar de una serie de tiempo, realicé un estudio de corte transversal, lo que permitió medir con precisión la diferencia de precios en el momento de mayor actividad.

## Hipótesis

En un mercado racional, el valor del m² correlaciona positivamente con la calidad de vida y los servicios urbanos.
La urgencia logística de la industria petrolera rompe esta lógica en **Añelo** (zona de extracción), generando una prima de precio significativa sobre ciudades dormitorio consolidadas como **Plottier** o **General Roca**, a pesar del déficit de infraestructura de la primera.

## 🛠️ Metodología y Stack Tecnológico

El análisis fue realizado íntegramente en **Python**.

* **Procesamiento de Datos:** Limpieza, normalización de fechas y tratamiento de outliers con Pandas.
* **Segmentación:** Filtrado geográfico (excluyendo zonas turísticas como Bariloche) y monetario (**Ventas en USD**) para neutralizar el efecto inflacionario del Peso Argentino.
* **Análisis Estadístico:** Cálculo de medianas, distribuciones y cuartiles para evitar sesgos por propiedades de lujo extremas.
* **Visualización:** Generación de Boxplots con Seaborn y Matplotlib.

## Principales Hallazgos

### 1. La Anomalía de Añelo
El análisis de distribución confirmó que la mediana de precios en la zona petrolera supera a la de zonas residenciales consolidadas. La dispersión de precios en Añelo es baja, indicando una oferta homogeneizada y funcional.
<img width="1184" height="784" alt="image" src="https://github.com/user-attachments/assets/f42b6ecd-212d-405a-bf83-1413315c8c51" />

### 2. Cuantificación de la Distorsión (Snapshot 2019-2020)
El cálculo de precios relativos confirma la existencia de una 'Prima Vaca Muerta' mediante los siguientes indicadores:

| Comparativa | Resultado | Interpretación |
| :--- | :--- | :--- |
| **Añelo vs. Plottier** | **+59.2%** | Prima pagada por **eficiencia logística** (cercanía al pozo). |
| **Añelo vs. Gral. Roca** | **+6.2%** | El precio en el "desierto" supera al de ciudades desarrolladas de Río Negro. |
| **Añelo vs. Neuquén** | **73.5%** | Convergencia: El valor en Añelo alcanza casi 3/4 del valor de la Capital. |

## Conclusiones

El estudio confirma que el mercado inmobiliario de la región no es homogéneo y coexisten dos lógicas de valoración:
1.  Una basada en la **amenidad urbana** (Neuquén Capital/Cipolletti).
2.  Otra basada estrictamente en la **rentabilidad logística y escasez de oferta** (Añelo).

La prima del **~60%** muestra que el mercado está dispuesto a pagar un sobreprecio por la proximidad al yacimiento, ignorando la falta de servicios residenciales ("Impuesto a la distancia").
