# 🛍️ Análisis de Ventas Retail — Limpieza, EDA y Modelos de Regresión

Análisis exploratorio y modelado predictivo sobre un dataset de transacciones retail, con el objetivo de predecir el **monto total de una transacción** (`Total Amount`) a partir de las características del cliente y de la compra.

---

## 📁 Contenido del proyecto

| Archivo | Descripción |
|---|---|
| `retail_sales_dataset.csv` | Dataset original — 1,000 transacciones, 9 columnas. |
| `analisis_retail_sales.ipynb` | Notebook principal: limpieza, exploración de datos y modelado. |

---

## 📊 Diccionario de datos

| Columna | Descripción |
|---|---|
| `Transaction ID` | Identificador único de cada transacción. |
| `Date` | Fecha en que ocurrió la transacción. |
| `Customer ID` | Identificador único de cada cliente. |
| `Gender` | Género del cliente (`Male` / `Female`). |
| `Age` | Edad del cliente. |
| `Product Category` | Categoría del producto (`Beauty`, `Clothing`, `Electronics`). |
| `Quantity` | Unidades compradas. |
| `Price per Unit` | Precio unitario del producto. |
| `Total Amount` | Monto total de la transacción (**target**). |

---

## 🔧 Estructura del análisis

### 1. Limpieza de datos
- Identificación y eliminación de registros duplicados.
- Verificación y ajuste de tipos de dato (`Date` → `datetime`, variables categóricas → `category`).
- Revisión y normalización de valores categóricos (`Gender`, `Product Category`).
- Diagnóstico de valores faltantes y estrategia de imputación dentro del pipeline (mediana / moda).

### 2. Exploración de datos (EDA)
- Estadísticas descriptivas: tendencia central y dispersión por variable.
- Visualizaciones univariadas: histogramas y gráficos de barras.
- Visualizaciones multivariadas: boxplots por categoría, dispersión `Quantity` vs `Total Amount`, mapa de calor de correlaciones y evolución mensual de ventas.

### 3. Modelado predictivo
- **Variables predictoras:** `Gender`, `Age`, `Product Category`, `Quantity`, `Price per Unit`.
- **Variable objetivo:** `Total Amount`.
- **Preprocesamiento:** `Pipeline` + `ColumnTransformer` (imputación, escalado de numéricas, codificación one-hot de categóricas).
- **Modelos:** `DecisionTreeRegressor` y `RandomForestRegressor`.
- **Optimización:** `GridSearchCV` con validación cruzada (`cv=5`).
- **Métricas de evaluación:** R², MAE, MSE y RMSE.

---

## 🏆 Resultados principales

Ambos modelos alcanzan un **R² ≈ 1.0** en el conjunto de test. Esto se explica porque `Total Amount` está determinado casi exactamente por `Quantity × Price per Unit`, dos de las variables predictoras incluidas — relación que el feature importance del Random Forest confirma como dominante.

| Criterio | Decision Tree | Random Forest |
|---|---|---|
| Rendimiento (R²) | Muy alto | Muy alto |
| Robustez ante nuevos datos | Menor (sensible a profundidad) | Mayor (promedio de múltiples árboles) |
| Interpretabilidad | Alta (árbol único, reglas claras) | Menor (ensemble de árboles) |
| Recomendación | Ideal para explicar reglas de negocio | Ideal para producción |

---

## 🚀 Cómo ejecutar

1. Clonar o descargar este proyecto.
2. Instalar las dependencias:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```
3. Abrir y ejecutar el notebook:
   ```bash
   jupyter notebook analisis_retail_sales.ipynb
   ```

---

## 🛠️ Tecnologías utilizadas

- **Python 3**
- **pandas** / **numpy** — manipulación de datos
- **matplotlib** / **seaborn** — visualización
- **scikit-learn** — pipelines, preprocesamiento, modelos de regresión y `GridSearchCV`

