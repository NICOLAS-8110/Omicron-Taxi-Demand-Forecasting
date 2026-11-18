<img width="1280" height="640" alt="WhatsApp Image 2026-11-17 at 3 00 46 PM (14)" src="https://github.com/user-attachments/assets/a7acf9e0-ae8c-4ded-a918-8bfd8799dd8c" />

# 🚕 Ο Proyecto Omicron | Predicción de Demanda de Taxis (Sweet Lift Taxi)

## 📋 Descripción
La compañía **Sweet Lift Taxi** busca anticipar la demanda de taxis en los aeropuertos para atraer un número adecuado de conductores durante los períodos de alta actividad. El objetivo principal de este proyecto es desarrollar un modelo de aprendizaje automático de series temporales capaz de predecir la cantidad de pedidos de taxis para la próxima hora utilizando datos históricos de solicitudes.

Para lograrlo, se implementó un flujo completo que incluyó análisis exploratorio de series temporales, descomposición de tendencias, ingeniería de características con retardos (*lags*) y medias móviles, y la evaluación de múltiples algoritmos de regresión.

## 🎯 Objetivos
- ✅ Cargar, ordenar cronológicamente y remuestrear los datos históricos de solicitudes de taxis por intervalos de una hora (`data.resample("1h").sum()`).
- ✅ Analizar la estacionalidad, tendencia y componentes residuales de la serie temporal.
- ✅ Diseñar características basadas en ingeniería temporal (`hour`, `day`, `dayofweek`), variables de desfase (`lag_1` a `lag_24`) y medias móviles (`rolling_mean`).
- ✅ Aplicar una división temporal estricta de los datos (`90%` entrenamiento / `10%` prueba, `shuffle=False`) para evitar fuga de datos.
- ✅ Entrenar y comparar modelos predictivos cumpliendo rigurosamente con el criterio de éxito del negocio: **RMSE < 48**.

## 🛠️ Herramientas y Habilidades Utilizadas
* **Lenguaje:** Python
* **Librerías:** Pandas, NumPy, Statsmodels, Scikit-Learn, LightGBM, XGBoost, Matplotlib y Seaborn
* **Entorno:** Jupyter Notebook ([Proyecto_Omicron_Predicción_de_Demanda_de_Taxis.ipynb](https://github.com/santidata7/Omicron-Taxi-Demand-Forecasting/blob/main/Proyecto_Omicron_Predicci%C3%B3n_de_Demanda_de_Taxis.ipynb))
* **Técnicas:** Análisis de Series Temporales, Descomposición Estacional, Ingeniería de Características (Lags y Rolling Mean), Validación Temporal y Modelos de Regresión Avanzados.

## 📊 Fuente de Datos y Variables
El análisis utiliza el conjunto de datos histórico `taxi.csv`:
| Variable / Componente | Descripción |
| :--- | :--- |
| `datetime` | Fecha y hora de la solicitud (configurada como índice cronológico) |
| `num_orders` | Cantidad de pedidos de taxis por hora (variable objetivo) |
| Características temporales | `hour`, `day`, `dayofweek`, etc., extraídas de la fecha |
| Variables de desfase (`lags`) | `lag_1`, `lag_24` para capturar persistencia horaria y diaria |
| Medias móviles (`rolling`) | `rolling_mean` para suavizar y capturar la tendencia local |

## ⚙️ Metodología
1. **Preparación de Datos:** Conversión de marcas de tiempo al formato *datetime*, indexación cronológica y remuestreo estricto a intervalos horarios mediante `data.resample("1h").sum()`.
2. **Análisis Exploratorio (EDA):** Identificación de la tendencia creciente en la demanda de taxis y patrones estacionales diarios mediante gráficos de descomposición (`statsmodels`).
3. **Ingeniería de Características:** Generación de atributos de calendario y creación de características retrospectivas (*lags* y *rolling mean*) para dotar al modelo de contexto histórico.
4. **División Temporal:** Partición cronológica de los datos respetando la naturaleza secuencial de las series de tiempo (`test_size = 0.10`, `shuffle = False`).
5. **Evaluación de Modelos:** Comparación sistemática de regresores frente a la línea base mediante la métrica **RMSE**.

## 💡 Comparación de Resultados
| Modelo Evaluado | RMSE | Criterio de Éxito (RMSE < 48) | Observaciones |
| :--- | :---: | :---: | :--- |
| **DummyRegressor (Modelo Base)** | 84.69 | ❌ | Línea base de referencia mínima |
| **Árbol de Decisión** | 50.09 | ❌ | No alcanza el estándar requerido |
| **Regresión Lineal** | 47.71 | ✅ | Cumple de forma justa el umbral |
| **Bosque Aleatorio (Random Forest)** | 46.40 | ✅ | Sólido desempeño predictivo |
| **LightGBM** | 46.19 | ✅ | Alta precisión y eficiencia |
| **XGBoost (Modelo Seleccionado)** | **41.79** | ✅ | **Mejor resultado obtenido de todo el estudio** |

### 🏆 Mejor Modelo: `XGBoost`
Con un **RMSE de 41.79** en el conjunto de prueba, **XGBoost** superó ampliamente el requisito mínimo de negocio establecido (`RMSE < 48`), demostrando una excelente capacidad para anticipar los picos de demanda en los aeropuertos.

## 📈 Principales Hallazgos
* **Valor de los componentes temporales:** La inclusión de características de desfase (*lags*) y medias móviles resultó indispensable para que los algoritmos de Machine Learning capturaran adecuadamente la estacionalidad diaria de la demanda de taxis.
* **Superioridad de Gradient Boosting:** Los modelos basados en árboles potenciados (**XGBoost** y **LightGBM**) obtuvieron los errores más bajos, superando a los enfoques lineales y de árboles individuales.
* **Cumplimiento de la meta operativa:** El modelo final de **XGBoost** ofrece la precisión necesaria para optimizar la asignación de conductores y mitigar los tiempos de espera de los usuarios en los aeropuertos.

## 📂 Archivos Principales
* [Proyecto_Omicron_Predicción_de_Demanda_de_Taxis.ipynb](https://github.com/santidata7/Omicron-Taxi-Demand-Forecasting/blob/main/Proyecto_Omicron_Predicci%C3%B3n_de_Demanda_de_Taxis.ipynb)
* [README.md](https://github.com/santidata7/Omicron-Taxi-Demand-Forecasting/blob/main/README.md)
* [taxi.csv](https://github.com/santidata7/Omicron-Taxi-Demand-Forecasting/blob/main/taxi.csv)

## 🏁 Conclusión
El proyecto demostró con éxito que los datos históricos de solicitudes permiten anticipar la demanda horaria de taxis para **Sweet Lift Taxi**. Mediante una sólida ingeniería de características temporales y el uso de **XGBoost** (**RMSE = 41.79**), se construyó un sistema predictivo confiable que cumple a cabalidad con el estándar técnico del negocio (`RMSE < 48`), facilitando la planificación operativa en periodos de alta actividad aeroportuaria.
