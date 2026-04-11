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

---

# Ejercicios complementarios semana 3

Estos ejercicios de la semana tres fueron hechos para reforzar los temas cubiertos a lo largo de las sesiones y las lecciones de **aula invertida**

- **T6**: Python para ciencia de datos
- **T7**: El proceso de ciencia de datos
- **T8**: Análisis exploratorio de datos en Python

## Prerrequisitos Recomendados
- **Programación**: Python básico (variables, funciones, loops)
- **Estadística**: Medidas de tendencia central, distribuciones, percentiles
- **Librerías**: NumPy, Pandas, Matplotlib

---

## Ejercicios con Python básico

## Ejercicio 1: Variables y Tipos de Datos

```python
# Ejercicios:
# 1. Crear variables de diferentes tipos: int, float, str, bool, list, dict
# 2. Convertir tipos: str a int, float a int, int a float
# 3. Usar f-strings para formatear: "El usuario tiene X años"
```

```python
# Crear variables
entero = 10
flotante = 3.14
cadena = "Hola"
booleano = True
lista = [1, 2, 3]
diccionario = {"nombre": "Daniel", "edad": 18}

# Conversión de tipos
texto_num = "25"
entero_convertido = int(texto_num)

float_num = 5.9
entero_desde_float = int(float_num)

entero_num = 7
float_convertido = float(entero_num)

# f-strings
edad = 18
mensaje = f"El usuario tiene {edad} años"
print(mensaje)
```

---

## Ejercicio 2: Control de flujo 

```python
#Número positivo, negativo o cero
numero = -5

if numero > 0:
    print("Positivo")
elif numero < 0:
    print("Negativo")
else:
    print("Cero")

# Menú con if-elif-else
opcion = 2

if opcion == 1:
    print("Opción 1 seleccionada")
elif opcion == 2:
    print("Opción 2 seleccionada")
else:
    print("Opción inválida")

# Loop for
lista = [10, 20, 30]
for elemento in lista:
    print(elemento)

# Factorial con while
n = 5
factorial = 1

while n > 0:
    factorial *= n
    n -= 1

print("Factorial:", factorial)

```

---

## Ejercicio 3: Funciones

```python
import math

# Área de un círculo
def area_circulo(radio):
    return math.pi * radio**2

# Celsius a Fahrenheit
def celsius_a_fahrenheit(c):
    return (c * 9/5) + 32

# Promedio de lista
def promedio(lista):
    return sum(lista) / len(lista)

# Máximo y mínimo
def max_min(lista):
    return max(lista), min(lista)

# prints
print(area_circulo(5))
print(celsius_a_fahrenheit(25))
print(promedio([1, 2, 3, 4]))
print(max_min([5, 2, 9, 1]))
```

---

## Ejercicios con NumPy

## Ejecicio 4: NumPy Arrays

```python
import numpy as np

arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.array([5, 4, 3, 2, 1])

suma = arr1 + arr2

# Multiplicación por escalar
escalar = arr1 * 2

# Estadísticas
media = np.mean(arr1)
mediana = np.median(arr1)
std = np.std(arr1)

# Valores únicos
unicos = np.unique(arr1)

# Reshape
reshape = arr1.reshape(5,1)

print(suma, escalar, media, mediana, std, unicos, reshape)
```

---

## Ejercicio 5: Álgebra con NumPy

```python
v1 = np.array([1, 2, 3])
v2 = np.array([4, 5, 6])

# punto
producto_punto = np.dot(v1, v2)

# cruz
producto_cruz = np.cross(v1, v2)

# Magnitud
magnitud_v1 = np.linalg.norm(v1)
magnitud_v2 = np.linalg.norm(v2)

# Normalización
norm_v1 = v1 / magnitud_v1
norm_v2 = v2 / magnitud_v2

print(producto_punto, producto_cruz, magnitud_v1, magnitud_v2)
```

---

## Ejercicios con Pandas

## Ejercicio 6: Pandas básico

```python

import pandas as pd

data = {
    'nombre': ['Ana', 'Luis', 'María', 'Carlos', 'Sofia'],
    'edad': [20, 22, 19, 21, 23],
    'carrera': ['Ing', 'Ing', 'Lic', 'Ing', 'Lic'],
    'promedio': [8.5, 9.0, 7.8, 8.2, 9.5]
}

df = pd.DataFrame(data)

# Seleccionar columna
print(df['nombre'])

# Filtrar
print(df[df['promedio'] > 8.5])

# Ordenar
print(df.sort_values(by='edad'))

# Nueva columna
df['aprobado'] = df['promedio'] >= 7

# Group by
print(df.groupby('carrera')['promedio'].mean())

```

---

## Ejercicio 7: Manipulación

```python
# Valores faltantes
df.loc[0, 'promedio'] = None
df['promedio'] = df['promedio'].fillna(df['promedio'].mean())

# Eliminar duplicados
df = df.drop_duplicates()

# Apply
df['doble_edad'] = df['edad'].apply(lambda x: x * 2)

# loc e iloc
print(df.loc[0])
print(df.iloc[0:2])

# Concatenar
df2 = df.copy()
df_concat = pd.concat([df, df2])

```

---

## Ejercicios de visualización

## Ejercicio 8: Matplotlib

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y = np.sin(x)

# Línea
plt.plot(x, y)
plt.title("Gráfico de línea")
plt.show()

# Scatter
plt.scatter(x, y)
plt.title("Scatter")
plt.show()

# Histograma
plt.hist(y)
plt.title("Histograma")
plt.show()

# Barras
plt.bar([1,2,3], [3,7,5])
plt.title("Barras")
plt.show()\
```

---

## Ejercicio 9: EDA

```python
import seaborn as sns

df = sns.load_dataset('iris')

# Info
print(df.info())

# Estadísticas
print(df.describe())

# Histogramas
df.hist()
plt.show()

# Correlación
corr = df.corr(numeric_only=True)
sns.heatmap(corr, annot=True)
plt.show()

# Boxplot
sns.boxplot(x='species', y='sepal_length', data=df)
plt.show()

# Outliers (IQR)
Q1 = df['sepal_length'].quantile(0.25)
Q3 = df['sepal_length'].quantile(0.75)
IQR = Q3 - Q1

outliers = df[(df['sepal_length'] < Q1 - 1.5*IQR) | (df['sepal_length'] > Q3 + 1.5*IQR)]
print(outliers)
```

---

## Ejercicios de Estadística

## Ejercicio 10: Medidas de Tendencia Central

```python
# Media
def media(lista):
    return sum(lista) / len(lista)

# Mediana (no burbuja)
def mediana(lista):
    lista = sorted(lista)
    n = len(lista)
    mid = n // 2
    if n % 2 == 0:
        return (lista[mid-1] + lista[mid]) / 2
    else:
        return lista[mid]

# Moda
def moda(lista):
    frecuencias = {}
    for num in lista:
        frecuencias[num] = frecuencias.get(num, 0) + 1
    return max(frecuencias, key=frecuencias.get)

datos = [5, 3, 8, 3, 7]

print("Media:", media(datos))
print("Mediana:", mediana(datos))
print("Moda:", moda(datos))
```
---

## Ejercicio 11: Dispersión

```python
import math

# Rango
def rango(lista):
    return max(lista) - min(lista)

# Varianza
def varianza(lista):
    m = sum(lista) / len(lista)
    return sum((x - m)**2 for x in lista) / len(lista)

# Desviación
def desviacion(lista):
    return math.sqrt(varianza(lista))

datos = [2,4,4,4,5,5,7,9]

print("Rango:", rango(datos))
print("Varianza:", varianza(datos))
print("Desviación:", desviacion(datos))
```
> Nota: Las capturas de pantalla para los ejercicios fueron omitidas para evitar relleno de evidencias en la documentación, sin embargo, la eficiencia de los códigos puede ser comprobada manualmente

## Ejercicios de investigación

## Ejercicio 12: El Proceso de Data Science

### 1. ¿Qué es el ciclo CRISP-DM?

CRISP-DM (Cross Industry Standard Process for Data Mining) es una metodología estándar utilizada en proyectos de ciencia de datos y minería de datos. Proporciona un enfoque estructurado para resolver problemas mediante el análisis de datos, asegurando que el proceso sea ordenado, iterativo y orientado a objetivos.

Se utiliza ampliamente en la industria porque permite organizar el trabajo desde la comprensión del problema hasta la implementación de soluciones basadas en datos.

### 2. ¿Cuáles son las fases del proceso de ciencia de datos?

El proceso de ciencia de datos generalmente sigue estas fases:

- Comprensión del negocio: Definir el problema y los objetivos.
- Comprensión de los datos: Explorar y analizar los datos disponibles.
- Preparación de los datos: Limpiar, transformar y organizar los datos.
- Modelado: Aplicar algoritmos y modelos predictivos.
- Evaluación: Verificar si el modelo cumple con los objetivos.
- Despliegue: Implementar la solución en un entorno real.

Estas fases no son lineales, ya que el proceso puede repetirse varias veces para mejorar los resultados.

### 3. ¿Qué es el MVP (Minimum Viable Product) en ciencia de datos?

El MVP (Producto Mínimo Viable) en ciencia de datos es una versión inicial de un modelo o solución que incluye solo las funcionalidades esenciales para resolver el problema principal.

Su objetivo es validar rápidamente si la solución funciona en la práctica, antes de invertir más tiempo y recursos en mejorarla. En lugar de buscar perfección desde el inicio, se prioriza obtener resultados útiles de forma rápida y luego iterar.

---

## Ejercicio 13: Caso de Estudio
Caso de estudio: Análisis de precios de Airbnb
1. ¿Qué preguntas buscaban responder?
- ¿Qué factores influyen en el precio de una propiedad?
- ¿Cómo afecta la ubicación al costo?
- ¿Existe relación entre el número de habitaciones y el precio?
- ¿Qué tipo de propiedad es más costosa?

---

2. ¿Qué técnicas usaron?
- Análisis exploratorio de datos (EDA)
- Estadísticas descriptivas (media, mediana, desviación estándar)

Visualizaciones:
- Histogramas
- Boxplots
- Gráficas de dispersión
- Mapas de calor (correlación)
- Detección de valores atípicos (outliers)

---

3. ¿Qué insights encontraron?
- El precio tiende a aumentar con el número de habitaciones.
- La ubicación es uno de los factores más importantes en el precio.
- Existen outliers (propiedades muy caras) que afectan el promedio.
- Algunas variables tienen mayor correlación con el precio que otras.
- La distribución de precios no es uniforme, mostrando concentración en rangos específicos.