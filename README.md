# 🧹 Kiva Crowdfunding Loans – Data Cleaning & Preparation with Python

Este proyecto se centra en el **procesamiento, limpieza y preparación de datos** utilizando **Python** en un entorno de **notebook (Jupyter / Google Colab)**, aplicando **buenas prácticas de Data Cleaning** sobre un dataset real de **Kiva Crowdfunding**.

El objetivo principal es transformar datos brutos (*raw data*) en un **dataset estructurado, consistente y reproducible**, listo para su posterior análisis o modelado predictivo, documentando de forma clara **cada decisión técnica tomada durante el proceso**.

---

## 🎯 Objetivos del proyecto

- Comprender la estructura y calidad inicial del dataset.
- Detectar y gestionar valores nulos, duplicados y tipos incorrectos.
- Normalizar y transformar variables clave.
- Crear columnas derivadas con valor analítico.
- Analizar y documentar outliers.
- Validar la calidad del dataset final.
- Exportar un dataset limpio en formato **CSV**.
- Entregar un notebook reproducible y bien documentado.

---

## 📊 Dataset utilizado

- **Nombre:** Data Science for Good – Kiva Crowdfunding  
- **Fuente:** Kaggle  
- **Link:** https://www.kaggle.com/datasets/kiva/data-science-for-good-kiva-crowdfunding  
- **Organización:** Kiva.org  

Dataset que contiene información sobre **préstamos de microfinanciación** otorgados a nivel global, incluyendo montos, países, sectores, prestamistas, fechas y estado del desembolso.

---

## 🧰 Tecnologías utilizadas

- **Python 3**
- **Google Colab / Jupyter Notebook**
- **Librerías**
  - pandas
  - numpy
  - matplotlib
  - seaborn
- **Control de versiones:** Git & GitHub
- **Formato de exportación:** CSV

---

## 🧭 Estructura del Notebook

1. Importación del dataset (local y Google Drive)
2. Exploración inicial
   - Dimensiones (shape)
   - Tipos de datos
   - Resumen estadístico
3. Diagnóstico de calidad de datos
   - Valores nulos
   - Duplicados
   - Formatos incorrectos
4. Limpieza y transformaciones
5. Creación de variables derivadas
6. Análisis visual exploratorio
7. Estudio de outliers
8. Validación post-limpieza
9. Exportación del dataset limpio

---

## 🔍 Proceso de limpieza y transformación

### 1️⃣ Eliminación de columnas con alto porcentaje de nulos

Durante la exploración inicial se identificaron columnas con muchos valores faltantes y bajo valor analítico para el estudio:

- tags  
- region  
- partner_id  

Estas columnas fueron eliminadas trabajando siempre sobre una **copia del dataset original**, preservando el raw data.

**Resultado:** dataset más limpio, legible y fácil de mantener.

---

### 2️⃣ Corrección de tipos de datos

Se detectó que varias columnas importantes, incluyendo fechas y valores numéricos, estaban almacenadas como tipo `object`.

Acciones realizadas:
- Conversión de columnas de fecha a tipo `datetime`
- Conversión de columnas numéricas a `int` o `float`

Este paso es fundamental para asegurar análisis, comparaciones y visualizaciones correctas.

---

### 3️⃣ Creación de columnas derivadas

#### 🔹 Tipo de préstamo según fecha de desembolso

Se creó la columna `loan_type` para clasificar los préstamos según el momento del desembolso:

python

kiva_loans_df["loan_type"] = np.where(
    kiva_loans_df["disbursed_time"] < kiva_loans_df["posted_time"],
    "pre_disbursed",
    "post_disbursed"
)
Esto permite analizar diferencias entre préstamos **pre_disbursed** y **post_disbursed**, aportando contexto temporal al estado del préstamo.

---

### 🔹 Categorización del monto del préstamo

Se creó la columna `loan_amount_category`, segmentando el monto del préstamo en:

- **Micro**
- **Small**
- **Medium**
- **Large**

Esta categorización facilita el análisis de distribuciones, comparaciones y patrones por tamaño de préstamo.

---

### 4️⃣ Análisis visual exploratorio

Se utilizaron distintos tipos de visualizaciones según el objetivo analítico:

#### 📊 Histogramas
- Mayor concentración de préstamos con monto inferior a **2.500**

#### 📊 Gráficos de barras
- Top países por `funded_amount` (destaca **Filipinas**)
- Distribución por sector (**Agriculture**, **Food**, **Retail**)
- Comparación entre préstamos **pre_disbursed** y **post_disbursed**

#### 📈 Gráficos de líneas
- Evolución mensual del monto medio del préstamo
- Picos claros en **enero**
- Descenso marcado en **2017**, posible línea de investigación futura

#### 🥧 Gráficos circulares
- Proporción de préstamos por país (**Top 8**)

---

### 5️⃣ Visualización geográfica

Se implementó un **choropleth map** para representar visualmente:

- Países
- Cantidad total de préstamos recibidos

Este enfoque facilita la comprensión del impacto geográfico y social de **Kiva**.

---

### 6️⃣ Análisis de outliers

Se realizó un análisis de valores atípicos utilizando:

- Cuartiles (**Q1**, **Q3**)
- Rango intercuartílico (**IQR**)
- Gráficos de densidad

#### 🔎 Resultados observados

- **Micro:** mayor densidad alrededor de **250**
- **Small:** concentración entre **500 y 1.000**
- **Medium:** densidad entre **2.000 y 3.000**, decreciendo hasta **6.000**
- **Large:** pico alrededor de **10.000**, con valores extremos cercanos a **50.000**

Las decisiones de conservación o exclusión de outliers fueron **documentadas y justificadas**.

---

### ✅ Validación post-limpieza

Se realizaron comprobaciones finales para asegurar la calidad del dataset:

- Conteos esperados
- Ausencia de nulos en columnas clave
- Coherencia de tipos de datos
- Revisión de muestras aleatorias

---

### 📤 Exportación del dataset limpio

El dataset final fue exportado:

- En formato **CSV**
- Tanto en **Google Drive** como en entorno local

Quedando listo para análisis posterior o modelado predictivo.

---

### 🧠 Conclusiones

- La limpieza de datos es un proceso crítico y estructurado
- Documentar cada decisión mejora la reproducibilidad
- La visualización ayuda a validar transformaciones
- El dataset final es consistente, legible y reutilizable
- Se aplicaron buenas prácticas de **Data Wrangling profesional**

---

### 🚀 Próximos pasos

- Exportar una versión en formato **Parquet**
- Automatizar el pipeline de limpieza
- Feature engineering avanzado
- Modelos predictivos sobre probabilidad de financiación

---

### 📌 Nota final

Este proyecto refleja un flujo de trabajo realista de un **Data Analyst**, poniendo énfasis en:

- Calidad de datos
- Reproducibilidad
- Trazabilidad
- Buen criterio técnico y analítico
