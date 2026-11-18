<img width="1280" height="640" alt="WhatsApp Image 2026-11-17 at 3 00 46 PM (14)" src="https://github.com/user-attachments/assets/a7acf9e0-ae8c-4ded-a918-8bfd8799dd8c" />

# 🚕 Proyecto Omicron | Predicción de Demanda de Taxis (Sweet Lift Taxi)

## 📋 Descripción
La compañía **Sweet Lift Taxi** busca anticipar la demanda de taxis en los aeropuertos para atraer un número adecuado de conductores durante los períodos de alta actividad. El objetivo de este proyecto es desarrollar un modelo de aprendizaje automático de series temporales capaz de predecir la cantidad de pedidos de taxis para la próxima hora utilizando datos históricos de solicitudes.

El requisito principal del proyecto es construir un modelo predictivo que cumpla con la métrica de negocio: **RMSE < 48**.

## 🎯 Objetivos
- ✅ Cargar, ordenar cronológicamente y remuestrear los datos de solicitudes de taxis por intervalos de una hora (`data.resample("1h").sum()`).
- ✅ Realizar un análisis exploratorio (EDA) para identificar tendencias, estacionalidad y componentes residuales de la serie temporal.
- ✅ Diseñar características temporales (`hora`, `día`, `mes`, `día de la semana`, `año`) y atributos históricos mediante variables de desfase (`lag_1`, `lag_24`) y medias móviles (`rolling_mean`).
- ✅ Aplicar una división estricta de los datos respetando el orden cronológico (`test_size = 0.10`, `shuffle = False`).
- ✅ Entrenar, optimizar y comparar múltiples modelos de regresión garantizando cumplir con la meta de **RMSE < 48**.

## 🛠️ Herramientas y Habilidades Utilizadas
* **Lenguaje:** Python
* **Librerías:** Pandas, NumPy, Statsmodels, Scikit-Learn, LightGBM, XGBoost, Matplotlib y Seaborn
* **Entorno:** Jupyter Notebook ([Proyecto_Omicron_Predicción_de_Demanda_de_Taxis.ipynb](https://github.com/santidata7/Omicron-Taxi-Demand-Forecasting/blob/main/Proyecto_Omicron_Predicci%C3%B3n_de_Demanda_de_Taxis.ipynb))
* **Técnicas:** Análisis de Series Temporales, Descomposición Estacional, Ingeniería de Características (*Lags* y *Rolling Mean*), Validación Temporal y Gradient Boosting.

## 📊 Fuente de Datos y Variables
El conjunto de datos (`taxi.csv`) contiene registros históricos de solicitudes con las siguientes características:
* **`datetime`**: Marca temporal de la solicitud (configurada como índice cronológico).
* **`num_orders`**: Cantidad de pedidos de taxis por hora (variable objetivo).
* **Características temporales y de desfase**: Atributos de calendario, 24 retardos y media móvil para capturar la persistencia diaria y estacional.

## ⚙️ Metodología
1. **Preparación de Datos:** Conversión al formato *datetime*, indexación cronológica y remuestreo estricto a intervalos horarios.
2. **Análisis Exploratorio (EDA):** Identificación visual de la tendencia creciente y los patrones estacionales diarios mediante descomposición de series temporales.
3. **Ingeniería de Características:** Creación automática de variables predictivas basadas en el comportamiento histórico y de calendario.
4. **División Temporal:** Partición estricta en entrenamiento (**90%**) y prueba (**10%**) sin barajar los datos.
5. **Evaluación de Modelos:** Comparación sistemática de algoritmos de regresión midiendo su desempeño mediante la métrica **RMSE**.

## 💡 Comparación de Resultados
| Modelo Evaluado | RMSE | Criterio de Éxito (RMSE < 48) | Observaciones |
| :--- | :---: | :---: | :--- |
| **DummyRegressor (Modelo Base)** | 84.69 | ❌ | Línea base mínima de referencia |
| **Árbol de Decisión** | 50.09 | ❌ | No alcanza el estándar requerido |
| **Regresión Lineal** | 47.71 | ✅ | Cumple de forma justa el umbral |
| **Bosque Aleatorio (Random Forest)** | 46.40 | ✅ | Sólido desempeño predictivo |
| **LightGBM** | 46.19 | ✅ | Alta velocidad y precisión |
| **XGBoost (Modelo Seleccionado)** | **41.79** | ✅ | **Mejor resultado obtenido del estudio** |

### 🏆 Mejor Modelo: `XGBoost`
Con un **RMSE de 41.79** en el conjunto de prueba, **XGBoost** superó ampliamente el requisito mínimo de negocio establecido (`RMSE < 48`), demostrando una excelente capacidad para anticipar con precisión los picos de demanda en los aeropuertos.

## 📈 Principales Hallazgos
* **Importancia de la ingeniería de características:** Las variables de desfase (*lags*) y la media móvil (*rolling_mean*) fueron fundamentales para que los modelos de Machine Learning asimilasen los ciclos diarios de la serie temporal.
* **Superioridad de Gradient Boosting:** Los algoritmos basados en árboles potenciados superaron claramente a los modelos lineales y tradicionales.
* **Cumplimiento operativo:** El modelo final de **XGBoost** proporciona la precisión necesaria para optimizar la asignación de conductores y reducir los tiempos de espera de los usuarios de **Sweet Lift Taxi**.

## 📂 Archivos Principales
* [Proyecto_Omicron_Predicción_de_Demanda_de_Taxis.ipynb](https://github.com/santidata7/Omicron-Taxi-Demand-Forecasting/blob/main/Proyecto_Omicron_Predicci%C3%B3n_de_Demanda_de_Taxis.ipynb)
* [taxi.csv](https://github.com/santidata7/Omicron-Taxi-Demand-Forecasting/blob/main/taxi.csv)

## 🏁 Conclusión
El proyecto culminó con éxito. Mediante un análisis riguroso de series temporales y el uso de **XGBoost** (**RMSE = 41.79**), se construyó un sistema predictivo robusto que cumple con creces el estándar técnico del negocio (`RMSE < 48`), facilitando la planificación operativa y la toma de decisiones en periodos de alta actividad en aeropuertos.
