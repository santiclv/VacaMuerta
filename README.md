# Efecto Vaca Muerta en el mercado inmobiliario

Este proyecto analiza cómo la actividad hidrocarburífera de **Vaca Muerta** impacta en los precios inmobiliarios de la región, con foco especial en la localidad de **Añelo** y su comparación con **Neuquén capital** y ciudades dormitorio cercanas.
La pregunta central es:
> Hasta qué punto la demanda industrial y logística asociada a Vaca Muerta logró “romper” la lógica tradicional del mercado inmobiliario residencial?

---

## 1. Contexto e hipótesis

En un mercado inmobiliario “normal”, los precios de las propiedades tienden a ser más altos en:
- capitales provinciales,
- ciudades con mejor infraestructura,
- mayor dotación de servicios y amenidades urbanas.

En cambio, **Añelo** es una localidad pequeña en el desierto neuquino que se transformó en el epicentro operativo de Vaca Muerta. La hipótesis de trabajo es que:

> **La presión de demanda generada por la industria petrolera y gasífera en Añelo produjo una “prima inmobiliaria” que no se explica por atributos urbanos tradicionales, sino por su rol estratégico dentro del complejo hidrocarburífero.**

---

## 2. Datos

- **Fuente:** dataset público de avisos inmobiliarios de Argentina (Properati / Kaggle). https://www.kaggle.com/datasets/alejandroczernikier/properati-argentina-dataset
- **Cobertura temporal del análisis:**  
  Se trabaja con publicaciones cuyo `start_date` está entre:
  - **2019-01-01** y  
  - **2020-12-31**
En la práctica, el dataset contiene avisos entre **2019-07-04** y **2020-07-27**, por lo que el análisis es una **foto transversal** de un período de alta actividad.

---

## 3. Alcance geográfico

Del universo de avisos se seleccionan solo las observaciones de las provincias:
- **Neuquén**
- **Río Negro**

Dentro de ellas, se filtran las ciudades que conforman el ecosistema directo de Vaca Muerta:
- Neuquén
- General Roca  
- Cipolletti  
- Plottier  
- Añelo  
- Centenario  
- Rincón de los Sauces  
- General Fernández Oro  
- Cinco Saltos  

Adicionalmente se excluyen ciudades claramente influenciadas por turismo (ej. Bariloche, Villa La Angostura, San Martín de los Andes), ya que responden a otra lógica de valorización.

---

## 4. Segmentación por tipo de mercado y moneda

El dataset incluye operaciones de:
- **Venta**
- **Alquiler**
- **Alquiler temporal**

y distintas monedas:
- **USD**
- **ARS**

Dado el contexto bimonetario argentino y la brecha cambiaria histórica, se adopta la siguiente estrategia:
- **Ventas:** se analizan únicamente las operaciones en **USD**.  
- **Alquileres:** se consideran solo las operaciones en **ARS**.

No se homogeneizan las monedas por tres motivos:

1. El mercado inmobiliario argentino funciona de forma dual:
   - ventas como **reserva de valor** en dólares,
   - alquileres como **flujo de caja** en pesos.
2. No existe un único tipo de cambio representativo (oficial vs. paralelo).
3. Cualquier conversión mecánica USD→ARS sin una serie de tiempo de tipo de cambio introduciría más ruido que información.

En este proyecto, el análisis profundo se centra en el **mercado de ventas en USD**.

---

## 5. Limpieza y preparación de datos

Sobre el subconjunto de **ventas en USD** en las ciudades seleccionadas, se aplican los siguientes criterios de limpieza:

1. **Registros completos en variables clave**
   - Se eliminan avisos sin `price` o sin `surface_total`.

2. **Rango razonable de precios (USD)**
   - Se conservan propiedades con precios entre **USD 20.000** y **USD 1.000.000**.  
   - Esto elimina valores claramente erróneos o extremos (cero, multimillonarios, etc.).

3. **Rango razonable de superficie total**
   - Se filtran propiedades con `surface_total` entre **20 m²** y **500 m²**.

4. **Consistencia en dormitorios y baños**
   - `bedrooms` entre **0 y 6** (o `NaN`).
   - `bathrooms` entre **1 y 5** (o `NaN`).

5. **Unificación Neuquén / Confluencia**
   - Se reemplaza `Confluencia` por `Neuquén` en la columna `l3` para evitar duplicar la plaza inmobiliaria de la capital.

Finalmente, se construye la variable:

price_m2 = price / surface_total

## 6. Metodología de análisis

El análisis se organiza en dos niveles:
1. **Precio total de venta (USD)**  
   Se utiliza como una descripción preliminar del mercado inmobiliario regional.  
   Dado que esta métrica combina efectos de tamaño, tipo de propiedad y estructura urbana,
   sus resultados se interpretan de manera descriptiva y no inferencial.

2. **Precio por metro cuadrado (USD/m²)**  
   Esta métrica constituye la base principal del análisis comparativo.
   Al ajustar por superficie, permite aislar con mayor precisión el efecto de la localización
   y la cercanía al nodo productivo petrolero sobre los valores inmobiliarios.


En todos los casos se utilizan principalmente:
- **Mediana** como medida de tendencia central, por ser menos sensible a valores extremos.  
- **Diagramas de caja (boxplots)** para visualizar la estructura y dispersión de precios por ciudad.

---

## 7. Resultados principales

### 7.1. Precio total de venta (USD)

A partir de las medianas de precio de venta se observa que:
- **Añelo** presenta un precio mediano de venta superior al de **Plottier** y comparable al de **General Roca**.  
- **Neuquén capital** continúa siendo la ciudad con el precio mediano más alto de la región, aunque la brecha con Añelo se reduce de manera significativa.

En términos relativos:
- Una propiedad en **Añelo** cuesta aproximadamente un **60% más** que en **Plottier**.  
- El valor mediano en **Añelo** representa alrededor del **75%** del valor de una propiedad en **Neuquén capital**.

Este resultado es inusual para una localidad pequeña, con menor infraestructura y menor oferta de servicios urbanos que la capital provincial.

---

### 7.2. Precio por metro cuadrado (USD/m²)

El análisis por metro cuadrado revela un patrón aún más marcado:
- El **precio mediano por m² en Añelo** es:
  - varias veces superior al de **Plottier** y supera incluso al de **Neuquén capital**.

De forma aproximada:
- **Añelo** muestra una prima cercana al **+400% por m²** respecto a **Plottier**.  
- El precio por m² en Añelo es del orden del **130%** del observado en **Neuquén capital**.

Estos resultados sugieren que:
- las propiedades en Añelo tienden a ser **más pequeñas**, pero **considerablemente más caras por unidad de superficie**, lo que es consistente con una fuerte presión de demanda sobre una oferta inmobiliaria limitada.

---

## 8. Interpretación económica

Los resultados son consistentes con la hipótesis de un **“Efecto Vaca Muerta”**:
- La valorización inmobiliaria en Añelo no se explica por calidad urbana, infraestructura o amenidades residenciales tradicionales.  
- En cambio, parece responder principalmente a:
  - la demanda laboral ligada a la actividad petrolera, las necesidades de alojamiento del personal técnico y operativo y las restricciones de oferta en un territorio que funciona como un **nodo productivo especializado**.

En este contexto, el mercado inmobiliario de Añelo se desacopla parcialmente de los determinantes urbanos clásicos y se alinea con la lógica de **enclaves económicos intensivos**, similar a la observada en otros polos extractivos o industriales a nivel global.

---

## 9. Limitaciones y líneas futuras

Este trabajo debe entenderse como un **análisis exploratorio transversal**, sujeto a varias limitaciones:
- Se basa en **precios publicados**, que no necesariamente coinciden con los precios finales de cierre.  
- El período temporal analizado es relativamente acotado (aprox. **2019–2020**).  
- No se incluyen variables explícitas vinculadas a:
  - calidad de construcción, antigüedad de la propiedad, amenities internas (cochera, pileta, seguridad, etc.).
