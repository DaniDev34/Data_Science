# Avance del proyecto - Ciencia de Datos

---

# Parte 1: Base de datos

## Introducción

En esta primera etapa del proyecto se realiza la carga y exploración inicial del conjunto de datos correspondiente al mercado inmobiliario, específicamente basado en información de propiedades de **Airbnb**. Esta fase es fundamental dentro del flujo de trabajo en ciencia de datos, ya que permite comprender la estructura, calidad y características generales de los datos antes de proceder con cualquier tipo de análisis.

El dataset utilizado proviene de la plataforma **Kaggle**, el cual contiene información relevante sobre precios, ubicaciones, características físicas de las propiedades y otros atributos que pueden influir en el valor de una vivienda.

---

## Carga de datos

Para comenzar con el análisis, se importaron las librerías necesarias para el procesamiento y visualización de datos en Python. Entre las principales herramientas utilizadas se encuentran:

- **Pandas:** para la manipulación y análisis de datos.
- **NumPy:** para operaciones numéricas.
- **Matplotlib y Seaborn:** para la visualización de datos.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

sns.set(style="whitegrid")# Configuración visual

df = pd.read_csv("train.csv") # Cargar dataset 

df.head()# Mostrar primeras filas
```

Estas herramientas fueron instaladas dentro de un entorno virtual

Posteriormente, procedimos a descargar el dataset desde **Kaggle** en formato `.zip`, el cual fue descomprimido para obtener el archivo principal en formato `.csv`.

Una vez disponible el archivo, se cargó en un DataFrame de Pandas para poder trabajar con los datos de forma estructurada.

---

## Exploración inicial del dataset

Después de cargar el dataset, se realizó una exploración preliminar con el objetivo de comprender su estructura y contenido. En esta etapa se analizaron los siguientes aspectos:

- Número total de registros y columnas.
- Nombres de las variables.
- Tipos de datos de cada columna.
- Identificación de valores nulos o faltantes.

Esta exploración permite detectar posibles problemas en los datos, como inconsistencias, valores faltantes o tipos de datos incorrectos, los cuales deberán ser considerados en etapas posteriores del análisis.

---

## Estructura de los datos

El dataset contiene múltiples variables relacionadas con las propiedades de Airbnb, las cuales pueden clasificarse en distintos tipos:

- **Variables numéricas:** como el precio, número de habitaciones, número de baños, entre otros.
- **Variables categóricas:** como el tipo de propiedad o la ubicación.
- **Variables descriptivas:** que contienen información adicional sobre las propiedades.

Esta diversidad de variables permite realizar un análisis más completo, tanto desde un enfoque descriptivo como relacional, facilitando la identificación de factores que influyen en el precio de una vivienda.

---

## Importancia de esta etapa

La correcta carga y comprensión inicial de los datos es un paso crítico en cualquier proyecto de ciencia de datos, ya que establece la base para todo el análisis posterior.

En esta etapa se logra:

- Verificar que los datos se cargaron correctamente.
- Identificar problemas de calidad en los datos.
- Comprender la estructura general del dataset.
- Preparar la información para el análisis exploratorio.

---

# Parte 2: Análisis Exploratorio de Dato



En esta etapa del proyecto se lleva a cabo el análisis exploratorio de datos (EDA), cuyo objetivo es comprender en profundidad el comportamiento del dataset, identificar patrones, tendencias y posibles anomalías dentro de los datos relacionados con Airbnb.

El EDA permite transformar los datos en información útil mediante el uso de estadísticas descriptivas y visualizaciones, lo cual facilita la interpretación de los datos y la toma de decisiones.

---


## Análisis descriptivo

Se realizó un análisis estadístico de las variables numéricas del dataset con el fin de entender su comportamiento. Para ello, se calcularon las siguientes medidas:

- **Media:** para conocer el valor promedio de las variables.
- **Mediana:** para identificar el valor central de los datos.
- **Moda:** para determinar los valores más frecuentes.
- **Desviación estándar:** para medir la dispersión de los datos.

Este análisis permite obtener una visión general del comportamiento de variables clave como el precio, así como identificar posibles anomalías.

---

## Visualización de datos

Para complementar el análisis descriptivo, se generaron diversas visualizaciones utilizando bibliotecas como **Matplotlib** y **Seaborn**, con el objetivo de representar gráficamente los datos y facilitar su interpretación.

### Histogramas

Los histogramas se utilizaron para analizar la distribución de variables numéricas, especialmente el precio de las propiedades. Esto permite identificar la concentración de datos en ciertos rangos.

### Diagramas de caja (Boxplot)

Los diagramas de caja se emplearon para detectar valores atípicos (outliers), los cuales pueden afectar significativamente el análisis.

### Gráficas de dispersión (Scatter Plot)

Las gráficas de dispersión permitieron analizar la relación entre variables, como el número de habitaciones y el precio, ayudando a identificar posibles correlaciones.

### Mapa de calor de correlaciones

Se utilizó un mapa de calor para visualizar la relación entre variables numéricas, facilitando la identificación de aquellas que tienen mayor impacto en el precio.

---

## Interpretación de resultados

A partir del análisis exploratorio, es posible identificar patrones relevantes en el comportamiento de los datos. Por ejemplo, ciertas características de las propiedades pueden influir directamente en su precio, mientras que la presencia de valores atípicos puede indicar propiedades con características especiales o segmentación dentro del mercado.

Este análisis proporciona una base sólida para comprender los datos y continuar con etapas más avanzadas, como la construcción de modelos predictivos.

---