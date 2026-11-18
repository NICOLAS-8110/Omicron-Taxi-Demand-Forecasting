<img width="1280" height="640" alt="WhatsApp Image 2026-11-17 at 3 00 46 PM (14)" src="https://github.com/user-attachments/assets/a7acf9e0-ae8c-4ded-a918-8bfd8799dd8c" />

# 🚕 Ο Proyecto Omicron | Predicción de Demanda de Taxis (Sweet Lift Taxi)

## 📋 Descripción
La compañía **Sweet Lift Taxi** ha recopilado datos históricos sobre pedidos de taxis en los aeropuertos. Para atraer a más conductores durante las horas pico, necesitamos predecir la cantidad de pedidos de taxis para la próxima hora utilizando modelos de aprendizaje automático y técnicas de series temporales.

El requisito principal del proyecto es que la métrica **RECM (RMSE)** en el conjunto de prueba **no sea superior a 48**.

## 🎯 Objetivos
- ✅ Descargar, ordenar cronológicamente y remuestrear los datos de solicitudes de taxis por intervalos de una hora (`data.resample("1h").sum()`).
- ✅ Realizar un análisis exploratorio de la serie temporal para identificar tendencia, estacionalidad y estacionalidad a corto plazo.
- ✅ Diseñar características basadas en ingeniería temporal (`year`, `month`, `day`, `dayofweek`), variables de desfase (*lags*) y medias móviles (`rolling_mean`).
- ✅ Dividir los datos cronológicamente respetando la secuencia temporal (`test_size = 0.10`, `shuffle = False`).
- ✅ Entrenar y comparar múltiples modelos evaluando su desempeño mediante **RECM**, asegurando cumplir con la meta de negocio de **RECM < 48**.

## 🛠️ Herramientas y Habilidades Utilizadas
* **Lenguaje:** Python
* **Librerías:** Pandas, NumPy, Statsmodels, Scikit-Learn y Matplotlib
* **Entorno:** Jupyter Notebook ([Proyecto_Omicron_Predicción_de_Demanda_de_Taxis.ipynb](https://github.com/santidata7/Omicron-Taxi-Demand-Forecasting/blob/main/Proyecto_Omicron_Predicci%C3%B3n_de_Demanda_de_Taxis.ipynb))
* **Técnicas:** Análisis de Series Temporales, Descomposición Estacional, Ingeniería de Características (*Lags* y *Rolling Mean*), Validación Temporal y Optimización de Hiperparámetros.

## 📊 Fuente de Datos y Variables
El conjunto de datos histórico (`taxi.csv`) contiene:
* **`datetime`**: Marca temporal de la solicitud (configurada como índice cronológico).
* **`num_orders`**: Cantidad de pedidos de taxis por hora (variable objetivo).
* **Características creadas:** Variables de calendario (`year`, `month`, `day`, `dayofweek`), 24 retardos (*lags*) y media móvil (`rolling_mean`).

## ⚙️ Metodología
1. **Preparación y Remuestreo:** Carga de datos, indexación y conversión a intervalos horarios con `data.resample("1h").sum()`.
2. **Análisis Exploratorio (EDA):** Identificación visual y estadística de la tendencia alcista constante y los patrones estacionales diarios mediante `statsmodels.tsa.seasonal.seasonal_decompose`.
3. **Ingeniería de Características:** Creación automática de atributos históricos y temporales mediante la función `make_features`.
4. **División de Datos:** Partición en entrenamiento, subconjunto de validación y prueba final cronológica (`10%` de test, `shuffle=False`).
5. **Entrenamiento y Validación:** Búsqueda de hiperparámetros óptimos para Árboles de Decisión y Bosques Aleatorios, junto con una Regresión Lineal de referencia.

## 💡 Comparación de Resultados en Validación
| Modelo Evaluado | Hiperparámetros Óptimos | RECM (Validación) |
| :--- | :--- | :---: |
| **Regresión Lineal** | Por defecto | **32.95** |
| **Bosque Aleatorio (Random Forest)** | `n_estimators=100`, `max_depth=15` | **34.35** |
| **Árbol de Decisión** | `max_depth=10` | **38.76** |

## 🏆 Evaluación en el Conjunto de Prueba
Tras seleccionar la **Regresión Lineal** por su excelente desempeño en validación (**RECM = 32.95**), se evaluó en la muestra de prueba (`10%` de los datos):
* **RECM Final en Prueba:** **45.54**
* **Criterio de Éxito (RECM < 48):** **Cumplido con éxito ✅**

## 📈 Principales Hallazgos
* El análisis exploratorio confirmó una clara tendencia ascendente en la demanda de taxis entre marzo y agosto de 2018, además de un ciclo diario muy marcado.
* La inclusión de características retrospectivas (*lags* y *rolling_mean*) aportó el contexto necesario para que los modelos capturaran adecuadamente las fluctuaciones de la serie temporal.
* La **Regresión Lineal** demostró una excelente capacidad de generalización en el conjunto de prueba, alcanzando un **RECM de 45.54**, superando el límite máximo establecido por el proyecto (`< 48`).

## 📂 Archivos Principales
* [Proyecto_Omicron_Predicción_de_Demanda_de_Taxis.ipynb]
* [taxi.csv]

## 🏁 Conclusión
El proyecto cumplió a cabalidad con los objetivos planteados. Mediante una adecuada preparación, análisis temporal y la construcción de un modelo de **Regresión Lineal** robusto, se obtuvo un **RECM de 45.54** en el conjunto de prueba, validando que el sistema es capaz de anticipar con precisión la demanda horaria de taxis para **Sweet Lift Taxi** y facilitar la asignación óptima de conductores en periodos de alta actividad.
