# Actividad 4

# 1.- Preparación de los datos

## Introducción

En esta actividad se llevó a cabo el análisis de dos conjuntos de datos con el objetivo de aplicar modelos de regresión para la predicción y clasificación de información relevante.

En la primera parte, se trabajó con un dataset de vehículos, donde se analizaron variables como el precio de venta, kilometraje y condiciones del vehículo para predecir su valor mediante un modelo de regresión lineal múltiple.

En la segunda parte, se utilizó el dataset del Titanic con el propósito de identificar los factores que influyen en la sobrevivencia de los pasajeros mediante un modelo de regresión logística.


---

## Limpieza de datos

La limpieza de datos consiste en identificar y corregir problemas dentro del dataset que puedan afectar el análisis y el rendimiento del modelo.

Algunos de los problemas más comunes incluyen:

* **Valores faltantes**
* **Datos inconsistentes**
* **Columnas irrelevantes**
* **Valores extremos (outliers)**

Para solucionar estos problemas se aplicaron las siguientes técnicas:

* Eliminación de columnas no relevantes para el análisis
* Eliminación o imputación de valores nulos
* Filtrado de valores inválidos (por ejemplo, precios o kilometraje negativos)
---

## Estandarización de datos

La estandarización de datos permite transformar la información a un formato adecuado para su procesamiento.

En esta actividad se realizaron acciones como:

* Conversión de variables categóricas a valores numéricos
* Ajuste de tipos de datos
* Preparación de variables para modelos de machine learning
---

## Relación con el modelo de regresión

La calidad de los datos influye directamente en el desempeño de los modelos de regresión.

En la primera parte:

* **Variable dependiente (y):** `sellingprice`
* **Variables independientes (X):** `odometer`, `year`, `condition`, `mmr`

En la segunda parte:

* **Variable dependiente (y):** `survived`
* **Variables independientes (X):** variables como `age`, `sex`, `pclass`, `fare`

---

## Obtención de los datos

Para el desarrollo de esta actividad se utilizaron dos datasets:

* Dataset de ventas de vehículos obtenido de Kaggle
* Dataset del Titanic obtenido de OpenML

Ambos datasets contienen información relevante para el análisis y fueron seleccionados por su utilidad en la aplicación de modelos de regresión.

---

## Carga de datos

Una vez obtenidos los datasets, se procedió a cargarlos en el entorno de trabajo utilizando Pandas.

```python
import pandas as pd
df = pd.read_csv("car_prices.csv")
print("Datos cargados:")
print(f"Shape: {df.shape}")
print(df.head())

df2 = pd.read_csv("titanic.csv")
print("Datos del Titanic cargados:")
print(f"Shape: {df2.shape}")
print(df2.head())
```
---

## Exploración inicial del dataset

Se realizó un análisis preliminar para comprender la estructura de los datos.

```python

print("Información del dataset:")
print(df.info())
print("Descripción:")
print(df.describe())
print("Valores nulos:")
print(df.isnull().sum())

print("Información del dataset:")
print(df2.info())
print("Columnas disponibles:", df2.columns.tolist())
print()
```

Con base en la exploración inicial, se aplicaron técnicas de limpieza en ambos datasets.

Para el dataset de vehículos:

```python
df_limpio = df[['mmr', 'odometer', 'sellingprice']].dropna()
print(f"Datos originales: {len(df)} filas")
print(f"Datos después de limpiar nulos: {len(df_limpio)} filas")
```

Para el dataset del Titanic:

```python
columnas_eliminar = ['name', 'ticket', 'cabin', 'boat', 'body', 'home.dest']
df2_limpio = df2.drop(columns=columnas_eliminar)
print("Columnas eliminadas:", columnas_eliminar)
print()

print("Valores nulos antes de limpiar:")
print(df2_limpio.isnull().sum())
print()

df2_limpio = df2_limpio.dropna()
print(f"Datos después de limpiar nulos: {len(df2_limpio)} filas")
print()
print("Tipos de datos:")
print(df2_limpio.dtypes)
```
---

## Selección de variables

Se definieron las variables necesarias para los modelos.

Para vehículos:

* **X:** `odometer`, `year`, `condition`, `mmr`
* **y:** `sellingprice`

```python
X = df_limpio[['mmr', 'odometer']]  # Variables independientes
y = df_limpio['sellingprice']  # Variable dependiente

print("\nVariables definidas:")
print(f"- Variables independientes: {X.columns.tolist()}")
print(f"- Variable dependiente: sellingprice")
print(f"- Forma de X: {X.shape}")
print(f"- Forma de y: {y.shape}")
```

Para Titanic:

* **X:** variables relevantes del dataset
* **y:** `survived`
```python

X2 = df2_limpio[['pclass', 'sex', 'age', 'sibsp', 'parch', 'fare', 'embarked']]
y2 = df2_limpio['survived']


```


---

# 2.- Análisis exploratorio de datos

## Análisis exploratorio

Se realizó un análisis exploratorio para identificar patrones, relaciones y comportamiento de las variables.

---

## Estadísticas descriptivas

```python
print("Descripción:")
print(df.describe())
```
---

## Análisis de correlación

```python

corr = df.corr(numeric_only=True)
plt.figure(figsize=(8, 6))
sns.heatmap(corr, annot=True, cmap="coolwarm")
plt.title("Matriz de correlación")
plt.show()
```

![heatmap](ss3/1.png)
---

# 3.- Modelado

## Instalación de librerías

Para el modelado se utilizó la librería **scikit-learn**, la cual permite implementar modelos de forma eficiente.

```bash
pip install scikit-learn
```

---

## Importación de librerías

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import r2_score, mean_squared_error
```

---

## División de datos

El dataset se dividió en:

* Entrenamiento (80%)
* Prueba (20%)

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

---

## Creación del modelo

Para vehículos:

```python

df_limpio = df[['mmr', 'odometer', 'sellingprice']].dropna()
print(f"Datos originales: {len(df)} filas")
print(f"Datos después de limpiar nulos: {len(df_limpio)} filas")

X = df_limpio[['mmr', 'odometer']]  # Variables independientes
y = df_limpio['sellingprice']  # Variable dependiente

print("\nVariables definidas:")
print(f"- Variables independientes: {X.columns.tolist()}")
print(f"- Variable dependiente: sellingprice")
print(f"- Forma de X: {X.shape}")
print(f"- Forma de y: {y.shape}")

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

print("\nDivisión de datos:")
print(f"- Conjunto de entrenamiento: {X_train.shape[0]} muestras")
print(f"- Conjunta de prueba: {X_test.shape[0]} muestras")

modelo = LinearRegression()
modelo.fit(X_train, y_train)

print("\nModelo de Regresión Lineal Múltiple entrenado")
print(f"- Intercepto: {modelo.intercept_:.4f}")
print(f"- Coeficientes: {dict(zip(X.columns, modelo.coef_))}")

y_pred = modelo.predict(X_test)

r2 = r2_score(y_test, y_pred)
mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)

print("\nEvaluación del modelo:")
print(f"- R² (Coeficiente de determinación): {r2:.4f}")
print(f"- Error Cuadrático Medio (MSE): {mse:.4f}")
print(f"- Raíz del Error Cuadrático Medio (RMSE): {rmse:.4f}")

print("\nEjemplo de predicciones:")
for i in range(5):
    print(f"Muestra {i+1}:")
    print(f"  - Variables: mmr={X_test.iloc[i]['mmr']}, odometer={X_test.iloc[i]['odometer']}")
    print(f"  - Valor real: {y_test.iloc[i]:.2f}")
    print(f"  - Predicción: {y_pred[i]:.2f}")
    print()

print(f"El modelo de regresión lineal múltiple explica aproximadamente el {r2*100:.2f}% de la variabilidad")
print("en los precios de venta de los vehículos utilizando las variables independientes:")
print("- mmr (precio de mercado recomendado)")
print("- odometer (kilometraje)")
print()
print(f"El error promedio en las predicciones es de aproximadamente ${rmse:.2f}.")
print()
print("Variables explicativas:")
print(f"  - mmr: {modelo.coef_[0]:.4f}")
print(f"  - odometer: {modelo.coef_[1]:.4f}")
print()

efectividad = 'es efectivo' if r2 > 0.7 else 'tiene un rendimiento moderado'

print("Conclusión: El modelo de regresión lineal múltiple " + efectividad + " para predecir precios de vehículos.")
```

Para Titanic:

```python

print("Regresión logistica - Titanic")

from scipy import stats
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

df2 = pd.read_csv("titanic.csv")
print("Datos del Titanic cargados:")
print(f"Shape: {df2.shape}")
print(df2.head())

print("Información del dataset:")
print(df2.info())
print("Columnas disponibles:", df2.columns.tolist())
print()

columnas_eliminar = ['name', 'ticket', 'cabin', 'boat', 'body', 'home.dest']
df2_limpio = df2.drop(columns=columnas_eliminar)
print("Columnas eliminadas:", columnas_eliminar)
print()

print("Valores nulos antes de limpiar:")
print(df2_limpio.isnull().sum())
print()

df2_limpio = df2_limpio.dropna()
print(f"Datos después de limpiar nulos: {len(df2_limpio)} filas")
print()
print("Tipos de datos:")
print(df2_limpio.dtypes)

df2_limpio['sex'] = df2_limpio['sex'].astype('category')
df2_limpio['embarked'] = df2_limpio['embarked'].astype('category')

df2_limpio['age'] = pd.to_numeric(df2_limpio['age'], errors='coerce')
df2_limpio['fare'] = pd.to_numeric(df2_limpio['fare'], errors='coerce')

df2_limpio = df2_limpio.dropna()

df2_limpio['sex'] = df2_limpio['sex'].cat.codes
df2_limpio['embarked'] = df2_limpio['embarked'].cat.codes

print("\nDatos después de conversión:")
print(df2_limpio.dtypes)
print()
print(df2_limpio.head())

sobrevividos = df2_limpio[df2_limpio['survived'] == 1]['age']
no_sobrevividos = df2_limpio[df2_limpio['survived'] == 0]['age']

t_stat, p_value = stats.ttest_ind(sobrevividos, no_sobrevividos)

print("\nPrueba t-test: Edad vs Sobrevivencia")
print(f"Media de edad de sobrevivientes: {sobrevividos.mean():.2f}")
print(f"Media de edad de no sobrevividos: {no_sobrevividos.mean():.2f}")
print(f"Estadístico t: {t_stat:.4f}")
print(f"Valor p: {p_value:.4f}")
print()
if p_value < 0.05:
    print("La diferencia ES estadísticamente significativa (p < 0.05)")
else:
    print("La diferencia NO es estadísticamente significativa (p >= 0.05)")

X2 = df2_limpio[['pclass', 'sex', 'age', 'sibsp', 'parch', 'fare', 'embarked']]
y2 = df2_limpio['survived']

print("\nVariables definidas para regresión logística:")
print(f"- Variables independientes: {X2.columns.tolist()}")
print(f"- Variable dependiente: survived")
print(f"- Forma de X: {X2.shape}")
print(f"- Forma de y: {y2.shape}")

X2_train, X2_test, y2_train, y2_test = train_test_split(X2, y2, test_size=0.2, random_state=42)

print("\nDivisión de datos - Titanic:")
print(f"- Conjunto de entrenamiento: {X2_train.shape[0]} muestras")
print(f"- Conjunto de prueba: {X2_test.shape[0]} muestras")

modelo_log = LogisticRegression(max_iter=1000)
modelo_log.fit(X2_train, y2_train)

print("Modelo de Regresión Logística")
print(f"- Intercepto: {modelo_log.intercept_[0]:.4f}")
print(f"- Coeficientes:")
for nombre, coef in zip(X2.columns, modelo_log.coef_[0]):
    print(f"    {nombre}: {coef:.4f}")

print("concluson: El modelo de regresión logística muestra cómo cada variable independiente afecta la probabilidad de supervivencia en el Titanic.")
print("------------------------------------------------------------------------")
```

---

# 4.- Evaluación del modelo

## Evaluación del modelo

Se utilizaron métricas para evaluar el desempeño:

* MSE
* MAE
* R²

```python
mse = mean_squared_error(y_test, y_pred)
print(f"MSE: {mse}")

mae = mean_absolute_error(y_test, y_pred)
print("MAE:", mae)

r2 = r2_score(y_test, y_pred)
print("R2:", r2)
```

---

# Parte 5: Visualización de resultados

## Visualización del modelo

Se generaron gráficas para facilitar la interpretación de los resultados.

```python
plt.figure(figsize=(10, 5))
sns.countplot(x='sex', hue='survived', data=df2_limpio)
plt.title('Sobrevivencia por sexo')
plt.show()

plt.figure(figsize=(10, 5))
sns.countplot(x='pclass', hue='survived', data=df2_limpio)
plt.title('Sobrevivencia por clase')
plt.show()

plt.figure(figsize=(10, 5))
sns.boxplot(x='survived', y='age', data=df2_limpio)
plt.title('Edad vs Sobrevivencia')
plt.show()

plt.figure(figsize=(10, 5))
sns.boxplot(x='survived', y='fare', data=df2_limpio)
plt.title('Tarifa vs Sobrevivencia')
plt.show()

corr2 = df2_limpio.corr(numeric_only=True)
plt.figure(figsize=(8, 6))
sns.heatmap(corr2, annot=True, cmap="coolwarm")
plt.title("Matriz de correlación - Titanic")
plt.show()
```

![captura](ss3/2.png)

![captura](ss3/3.png)

![captura](ss3/4.png)

![captura](ss3/5.png)

![captura](ss3/6.png)


---

# 6.- Comparación e interpretación de resultados

## Comparación de resultados

```python
resultados = pd.DataFrame({
    'Real': y_test.values,
    'Predicho': y_pred
})

print(resultados.head())
```

---

## Interpretación de resultados

Los resultados muestran cómo las variables influyen en las predicciones. En el caso de vehículos, variables como el kilometraje afectan negativamente el precio. En Titanic, variables como el sexo y la clase influyen en la sobrevivencia.

---

# Conclusión

Se concluye que:

* La calidad de los datos es fundamental para obtener buenos resultados
* La selección de variables influye directamente en el modelo
* Los modelos permiten identificar patrones importantes en los datos

---


# Ejercicios Complementarios - Semana 5 

## Temas Cubiertos

* Preparación de datos
* Análisis exploratorio
* Regresión lineal
* Regresión logística

---

## Ejercicio 1: Covarianza Manualmente

### Datos:
- X = [1, 2, 3, 4, 5]
- Y = [2, 4, 5, 4, 5]

### Paso 1: Calcular medias
```
X̄ = (1+2+3+4+5)/5 = 15/5 = 3
Ȳ = (2+4+5+4+5)/5 = 20/5 = 4
```

### Paso 2: Calcular covarianza

| xi | yi | xi - X̄ | yi - ȳ | (xi-X̄)(yi-ȳ) |
|----|----|--------|--------|--------------|
| 1  | 2  | -2     | -2      | 4            |
| 2  | 4  | -1     | 0       | 0            |
| 3  | 5  | 0      | 1       | 0            |
| 4  | 4  | 1      | 0       | 0            |
| 5  | 5  | 2      | 1       | 2            |

```
Σ(xi-X̄)(yi-ȳ) = 4 + 0 + 0 + 0 + 2 = 6
Cov(X,Y) = 6 / (5-1) = 6/4 = 1.5
```

>**Covarianza = 1.5**

---

## Ejercicio 2: Correlación de Pearson

###  1.- Calcular desviaciones estándar

Desviación estándar de X:
```
VAR(X) = Σ(xi-X̄)²/(n-1) = ((-2)²+(-1)²+0²+1²+2²)/4 = (4+1+0+1+4)/4 = 10/4 = 2.5
σX = √2.5 = 1.58
```

Desviación estándar de Y:
```
VAR(Y) = Σ(yi-ȳ)²/(n-1) = ((-2)²+0²+1²+0²+1²)/4 = (4+0+1+0+1)/4 = 6/4 = 1.5
σY = √1.5 = 1.22
```

### 2.- Calcular r
```
r = Cov(X,Y) / (σX * σY)
r = 1.5 / (1.58 * 1.22)
r = 1.5 / 1.93
r ≈ 0.78
```

>- **r = 0.78 está entre 0 y 1**
>- Significa que cuando X aumenta, Y también tiende a aumentar

---

## Ejercicio 3: Correlación en Python

```python
import pandas as pd
import numpy as np
from scipy import stats

df = pd.DataFrame({
    'horas_estudio': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    'calificacion': [35, 45, 50, 55, 65, 70, 75, 85, 90, 95]
})

print("Correlación:", df['horas_estudio'].corr(df['calificacion']))

r, p_value = stats.pearsonr(df['horas_estudio'], df['calificacion'])
print("p-value:", p_value)

print("Covarianza:", df.cov())
```


> - Correlación ≈ 0.99 ddd   
---

## Ejercicio 4: Intervalo de Confianza

### Datos:
- n = 25
- x̄ = 100
- s = 15
- Nivel de confianza = 95%

### 1.- Buscar t para 95% y 24 grados de libertad
- t ≈ 2.064 (valor de tabla t para 24 gl y 95%)

### 2.- Calcular el intervalo
```
IC = x̄ ± t * (s / √n)
IC = 100 ± 2.064 * (15 / √25)
IC = 100 ± 2.064 * (15 / 5)
IC = 100 ± 2.064 * 3
IC = 100 ± 6.192
IC = [93.81, 106.19]
```

**El intervalo de confianza es [93.81, 106.19]**

> Estamos 95% seguros de que la verdadera media poblacional está entre 93.81 y 106.19

---

## Ejercicio 5: Cálculo de p-valor

### Datos:
- H0: μ = 50
- Ha: μ ≠ 50
- n = 30
- x̄ = 55
- s = 10

### 1.- Calcular estadístico t
```
t = (x̄ - μ) / (s / √n)
t = (55 - 50) / (10 / √30)
t = 5 / (10 / 5.477)
t = 5 / 1.826
t ≈ 2.74
```

### 2.- Encontrar p-valor
- gl = 30 - 1 = 29
- Para t = 2.74 con 29 gl, el p-valor bilateral ≈ 0.01

### 3.- Decisión
- α = 0.05
- p-valor = 0.01 < 0.05

> RECHAZAR H0. Hay evidencia suficiente para decir que la media es diferente de 50.

---

## Ejercicio 6: Fórmula de Regresión Lineal

### Datos:
- X = [1, 2, 3, 4, 5]
- Y = [2, 4, 5, 4, 5]

### Ya calculado anteriormente:
- X̄ = 3, Ȳ = 4
- Cov(X,Y) = 1.5
- VAR(X) = 2.5

### Calcular β1:
```
β1 = Cov(X,Y) / Var(X)
β1 = 1.5 / 2.5
β1 = 0.6
```

### Calcular β0:
```
β0 = Ȳ - β1 * X̄
β0 = 4 - 0.6 * 3
β0 = 4 - 1.8
β0 = 2.2
```

### Ecuación de regresión:
```
ŷ = 2.2 + 0.6 * x
```

### Predecir para X = 6:
```
ŷ = 2.2 + 0.6 * 6
ŷ = 2.2 + 3.6
ŷ = 5.8
```

> ŷ = 2.2 + 0.6x, para X=6 predecimos Y=5.8

---

## Ejercicio 7: Regresión Lineal en Python

```python
import numpy as np
from sklearn.linear_model import LinearRegression

X = np.array([[1], [2], [3], [4], [5], [6], [7], [8], [9], [10]])
y = np.array([2, 4, 5, 4, 5, 6, 7, 8, 9, 11])

modelo = LinearRegression()
modelo.fit(X, y)

print(f"Intercepto: {modelo.intercept_}")  
print(f"Pendiente: {modelo.coef_[0]}")     

prediccion = modelo.predict([[11]])
print(f"Predicción para X=11: {prediccion}")  
```
> - Intercepto (β0) ≈ 1.4
> - Pendiente (β1) ≈ 0.8
> - Para X=11, Y ≈ 10.8

---

## Ejercicio 8: Coeficiente de Determinación (R²)

```python
from sklearn.metrics import r2_score

y_real = [1, 2, 3, 4, 5]
y_predicho = [1.1, 2.2, 2.9, 4.1, 4.9]

SS_res = sum((y - pred)**2 for y, pred in zip(y_real, y_predicho))
SS_tot = sum((y - sum(y_real)/len(y_real))**2 for y in y_real)

r2 = 1 - (SS_res / SS_tot)
print(f"R²: {r2}")

print(f"R² sklearn: {r2_score(y_real, y_predicho)}")
```

> R² ≈ 0.99 (el modelo explica 99% de la variabilidad)


---

## Ejercicio 9: Error Estándar de la Estimación

```python
import numpy as np
from sklearn.metrics import mean_squared_error, mean_absolute_error

y_real = [10, 20, 30, 40, 50]
y_predicho = [12, 18, 32, 38, 52]

rmse = np.sqrt(mean_squared_error(y_real, y_predicho))
mae = mean_absolute_error(y_real, y_predicho)

print(f"RMSE: {rmse}")  # Error promedio 
print(f"MAE: {mae}")   # Error absoluto medio
```


> - RMSE ≈ 2.0 (error promedio de 2 unidades)
> - MAE ≈ 2.0 (error médio de 2 unidades)

---

## Ejercicio 10: Análisis de Residuos

```python
import numpy as np
import matplotlib.pyplot as plt

X = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
y_real = np.array([2.1, 4.2, 5.8, 4.3, 5.5, 6.8, 7.5, 8.2, 9.1, 10.5])
y_predicho = [2.3, 4.1, 5.9, 4.2, 5.6, 6.5, 7.4, 8.3, 9.0, 10.4]

residuos = np.array(y_real) - np.array(y_predicho)

print("Residuos:", residuos)
print("Media de residuos:", np.mean(residuos))  
```


> - Los residuos son las diferencias entre valores reales y predichos
> - Deben estar distribuidos aleatoriamente alrededor de 0
> - No debe haber patrones claros

---

## Ejercicio 11: Supuestos de Regresión

### 1. Linealidad
- **Qué es:** La relación entre X y Y debe ser línea
- **Cómo verificarla:** Scatter plot de Y vs X debe mostrar una línea o patrón

### 2. Independencia
- **Qué es:** Los residuos no deben estar correlacionados entre sí
- **Qué es autocorrelación:** Cuando un residuo predice el siguiente
- **Cómo detectarla:** Gráfico de residuos vs orden

### 3. Homocedasticidad
- **Qué es:** Los residuos tienen la misma varianza en todo X
- **Qué es heterocedasticidad:** Varianza cambia con X
- **Cómo detectarla:** Gráfico de residuos vs valores predichos

### 4. Normalidad
- **Qué es:** Los residuos deben seguir una distribución normal
- **Qué es Q-Q plot:** Gráfico que compara residuos con distribución normal teórica
- **Cómo interpretarla:** Si los puntos siguen la línea, los residuos son normales

---

## Ejercicio 12: Prueba t para Correlación

```python
from scipy import stats

x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = [2, 4, 5, 4, 5, 6, 7, 8, 9, 11]

r, p_value = stats.pearsonr(x, y)

print(f"r: {r}")
print(f"p-value: {p_value}")

if p_value < 0.05:
    print("Rechazar H0: La correlación es significativa")
else:
    print("No rechazar H0: La correlación no es significativa")
```

> - r ≈ 0.96
> - 7.451501383552617e-06
>-    RECHAZAR H0, la correlación es significativa

---

## Ejercicios 13 y 14: Investigación

### Ejercicio 13: Aplicaciones de Regresión Lineal

1. **Regresión a la media:** Es un fenómeno estadístico donde valores extremos tienden a acercarse a la media en mediciones sucesivas

2. **Ejemplos de uso en negocios:**
   - Predecir ventas futuras basadas en gasto publicitario
   - Estimar precios de casas según tamaño
   - Predecir demanda de productos

3. **Diferencia entre correlación y causalidad:**
   - Correlación: Dos variables varían juntas
   - Causalidad: Una variable causa cambios en la otra
   - Correlación no implica causalidad

### Ejercicio 14: Limitaciones

1. **Relaciones no lineales:** La regresión lineal simple solo captura relaciones líneas, no curvas

2. **Extrapolación:** Predecir fuera del rango de datos es riesgoso porque supuesto de linealidad puede no cumplir

3. **Variable omitida:** Cuando una variable importante no está en el modelo, puede causar estimaciones incorrectas 

---