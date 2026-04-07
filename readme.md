# Avance del proyecto Ciencia de Datos

## Parte 1: Base de datos

## Introducción

En esta primera etapa del proyecto se realiza la carga y exploración inicial del conjunto de datos correspondiente al mercado inmobiliario, específicamente basado en información de propiedades de `Airbnb`. Este paso nos permite comprender la estructura, calidad y características generales de los datos antes de realizar cualquier tipo de análisis.

El dataset utilizado proviene de la plataforma `Kaggle`, el cual contiene información relevante sobre precios, ubicaciones, características físicas de las propiedades y otros atributos que pueden influir en el valor de una vivienda.

---

## Carga de datos

Para comenzar con nuestro análisis, se importaron las librerías necesarias para el procesamiento y visualización de datos en Python. Entre las principales herramientas utilizadas se encuentran:

- **Pandas:** para la manipulación y análisis de datos.
- **NumPy:** para operaciones numéricas.
- **Matplotlib y Seaborn:** para la visualización de datos.

```bash
pip install pandas numpy matplotlob
```

Dichas herramientas fueron instaladas en nuestro entorno virtual desde la terminal de VS Code.

Posteriormente, se procedió a cargar el dataset en un DataFrame, lo que nos permite trabajar con los datos de forma estructurada.

---

## Exploración inicial del dataset

Una vez que cargamos los datos, realizamos una revisión preliminar con el objetivo de comprender su estructura. Para ello, se analizaron los siguientes aspectos:

- Número de registros y columnas del dataset.
- Tipos de datos de cada variable.
- Identificación de valores nulos o faltantes.
- Visualización de las primeras filas del dataset.

Con esta exploración inicial pudimos identificar posibles problemas en los datos, como inconsistencias, valores faltantes o tipos de datos incorrectos, los cuales deberán ser considerados en etapas posteriores del análisis.

---

## Estructura de los datos

Nuestro dataset contiene múltiples variables relacionadas con las propiedades, entre las cuales se pueden encontrar:

- Variables numéricas (Ej. precio, número de habitaciones, etc.).
- Variables categóricas (de propiedad, ubicación, etc.).
- Variables descriptivas (información adicional de las propiedades).

Con diversidad de variables podemos hacer un más análisis completo, tanto descriptivo como relacional, lo cual es esencial para comprender factores que influyen en el precio de una vivienda.

---
## Parte 2: Análisis Exploratorio de Datos (EDA)

## Introducción

En esta parte del proyecto llevaremos a cabo el análisis exploratorio de datos (EDA), el cual tiene como objetivo comprender en profundidad las características del dataset, identificar patrones, tendencias y posibles anomalías dentro de los datos relacionados con `Airbnb`.

---

## Análisis descriptivo

Se realizó un análisis estadístico de las variables numéricas del dataset con el fin de obtener métricas que permitan entender su comportamiento. Entre las principales medidas calculadas se encuentran:

- **Media:** permite conocer el valor promedio de las variables.
- **Mediana:** indica el valor central de los datos.
- **Moda:** identifica los valores más frecuentes.
- **Desviación estándar:** mide la dispersión de los datos respecto a la media.

Además, se evaluaron las variables que podrían tener mayor influencia en el precio de una vivienda, considerando tanto variables numéricas como categóricas.

---

## Visualización de datos

Para complementar el análisis descriptivo, se generaron diversas visualizaciones utilizando bibliotecas como `Matplotlib`, con el objetivo de representar gráficamente la información y facilitar su interpretación.

### Histogramas

Se utilizaron histogramas para analizar la distribución de variables numéricas, especialmente el precio de las propiedades.

### Diagramas de caja (Boxplot)

Los diagramas de caja se utilizaron para detectar la presencia de valores atípicos en variables como el precio. Estos valores pueden influir significativamente en el análisis y deben ser considerados cuidadosamente.

### Gráficas de dispersión (Scatter Plot)

Se emplearon gráficas de dispersión para analizar la relación entre variables, como el número de habitaciones y el precio de las propiedades. Gracias a esto podemos identificar tendencias o correlaciones entre variables.

### Mapa de calor de correlaciones

Se generó un mapa de calor para visualizar las correlaciones entre variables numéricas. Esta herramienta es útil para identificar qué variables tienen mayor relación con el precio, lo que es fundamental para futuros modelos predictivos.

---

## Interpretación de resultados

El análisis realizado nos permite comprender mejor el comportamiento del mercado inmobiliario representado en el dataset. La identificación de patrones y relaciones entre variables nos proporciona información valiosa que puede ser utilizada para la toma de decisiones.

Por ejemplo, la relación entre el tamaño de una propiedad y su precio sugiere que características físicas influyen directamente en su valor. Asimismo, la presencia de valores atípicos indica la existencia de propiedades con precios significativamente diferentes al promedio, lo cual puede representar segmentos específicos del mercado.

---
