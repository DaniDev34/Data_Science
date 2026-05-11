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


Estas herramientas fueron anteriormente instaladas dentro de un entorno virtual

Posteriormente, procedimos a descargar el dataset desde **Kaggle** en formato `.zip`, el cual fue descomprimido para obtener el archivo principal en formato `.csv`.

Una vez disponible el archivo, se cargó en un DataFrame de Pandas para poder trabajar con los datos de forma estructurada.


![parte1_1](/ss/1_1.png)

![parte1_2](/ss/1_2.png)

---

## Exploración inicial del dataset

Después de cargar el dataset, se realizó una exploración preliminar con el objetivo de comprender su estructura y contenido. En esta etapa se analizaron los siguientes aspectos:

- Número total de registros y columnas.
- Nombres de las variables.
- Tipos de datos de cada columna.
- Identificación de valores nulos o faltantes.

```python

df.info() # Información general


print("Filas:", df.shape[0]) # Para dimensiones
print("Columnas:", df.shape[1])


print(df.columns) # Nombres de columnas


print(df.isnull().sum()) # Para valores nulos
```


```python
df = df.drop_duplicates()# Eliminar duplicados


df = df.dropna() # Manejo de nulos

```

![parte2](/ss/2.png)

Gracias a esta exploración incial podemos detectar posibles problemas en los datos, tales como inconsistencias, valores faltantes o tipos de datos incorrectos, los cuales deberán ser considerados en etapas posteriores del análisis.

---

## Estructura de los datos

El dataset contiene múltiples variables relacionadas con las propiedades de Airbnb, las cuales pueden clasificarse en distintos tipos:

- **Variables numéricas:** como el precio, número de habitaciones, número de baños, entre otros.
- **Variables categóricas:** como el tipo de propiedad o la ubicación.
- **Variables descriptivas:** que contienen información adicional sobre las propiedades.

Esta diversidad de variables permite realizar un análisis más completo, tanto desde un enfoque descriptivo como relacional.

---

## Importancia de esta etapa

La correcta carga y comprensión inicial de los datos es un paso crítico en cualquier proyecto de ciencia de datos, ya que establece la base para todo el análisis posterior.

En esta etapa se logra:

- Verificar que los datos se cargaron correctamente.
- Identificar problemas de calidad en los datos.
- Comprender la estructura general del dataset.
- Preparar la información para el análisis exploratorio.

---

# Parte 2: Análisis Exploratorio de Datos



En esta etapa del proyecto se lleva a cabo el análisis exploratorio de datos (EDA), cuyo objetivo es comprender en profundidad el comportamiento del dataset, identificar patrones, tendencias y posibles anomalías dentro de los datos relacionados con Airbnb.

El EDA permite transformar los datos en información útil mediante el uso de estadísticas descriptivas y visualizaciones, lo cual facilita la interpretación de los datos y la toma de decisiones.

---


## Análisis descriptivo

Se realizó un análisis estadístico de las variables numéricas del dataset con el fin de entender su comportamiento. Para ello, se calcularon las siguientes medidas:

- **Media:** para conocer el valor promedio de las variables.
- **Mediana:** para identificar el valor central de los datos.
- **Moda:** para determinar los valores más frecuentes.
- **Desviación estándar:** para medir la dispersión de los datos.

```python
# Estadísticas generales
df.describe()

# Media
print("Media:", df['log_price'].mean())

# Mediana
print("Mediana:", df['log_price'].median())

# Moda
print("Moda:", df['log_price'].mode()[0])

# Desviación estándar
print("Desviación estándar:", df['log_price'].std())
```

![parte3](/ss/3.png)

Este análisis permite tener una visión general del comportamiento de las variables clave como el precio.

---

## Visualización de datos

Para complementar el análisis descriptivo, se generaron diversas visualizaciones utilizando bibliotecas como **Matplotlib** y **Seaborn**, con el objetivo de representar gráficamente los datos y facilitar su interpretación.

### Histogramas

Los histogramas se utilizaron para analizar la distribución de variables numéricas, especialmente el precio de las propiedades. 

```python
plt.figure(figsize=(8,5))
plt.hist(df['price'], bins=50)
plt.title("Distribución de precios")
plt.xlabel("Precio")
plt.ylabel("Frecuencia")
plt.show()
```
![parte4](/ss/4.png)

### Diagramas de caja (Boxplot)

Los diagramas de caja se emplearon para detectar valores atípicos (outliers), los cuales pueden afectar el análisis.

```python
plt.figure(figsize=(6,4))
sns.boxplot(x=df['log_price'])
plt.title("Boxplot de precios")
plt.show()
```
![parte5](/ss/5.png)

### Gráficas de dispersión (Scatter Plot)

Las gráficas de dispersión permitieron analizar la relación entre variables, como el número de habitaciones y el precio, ayudando a identificar posibles correlaciones.

```python
plt.figure(figsize=(8,5))
sns.scatterplot(x='bedrooms', y='price', data=df)
plt.title("Relación entre habitaciones y precio")
plt.show()
```

![parte6](/ss/6.png)

### Mapa de calor de correlaciones

Se utilizó un mapa de calor para visualizar la relación entre variables numéricas e identificar aquellas que tienen mayor impacto en el precio.

```python
plt.figure(figsize=(10,6))
corr = df.corr(numeric_only=True)
sns.heatmap(corr, annot=True, cmap="coolwarm")
plt.title("Mapa de correlación")
plt.show()
```
![parte7](/ss/7.png)

---

## Interpretación de resultados

A partir del análisis exploratorio, es posible identificar patrones relevantes en el comportamiento de los datos. Por ejemplo, ciertas características de las propiedades pueden influir directamente en su precio, mientras que la presencia de valores atípicos puede indicar propiedades con características especiales o segmentación dentro del mercado.

Este análisis proporciona una base sólida para comprender los datos y continuar con etapas más avanzadas, como la construcción de modelos predictivos.

# Proyecto final 

