# COVID-19 US States Exploratory Data Analysis (EDA) 📊

Documentación y código del flujo de Análisis Exploratorio de Datos (EDA) sobre el impacto y evolución epidemiológica del COVID-19 en las jurisdicciones de los Estados Unidos.

---

## 📌 Descripción del Proyecto

Este proyecto ejecuta un EDA riguroso y estructurado sobre el conjunto de datos público `all-states-history.csv`. El dataset abarca **20,780 registros y 41 columnas** correspondientes a **56 estados y territorios** de EE. UU. (incluyendo Guam, Islas Vírgenes, Samoa Estadounidense, Islas Marianas del Norte, Puerto Rico y Washington D.C.), cubriendo el periodo del **13 de enero de 2020 al 7 de marzo de 2021**.

---

## 🛠️ Requisitos y Librerías

El proyecto incluye un archivo `requirements.txt` para garantizar la reproducibilidad completa del entorno analítico. Las librerías principales empleadas son: 
- **Manipulación de datos:** `pandas`, `numpy`
- **Visualización gráfica:** `matplotlib`, `seaborn`, `missingno`
- **Estadística e inferencia:** `scipy.stats`
---
## 🚀 Estructura y Fases del EDA

### 🔹 Fase 0: Ingesta y Profiling Inicial

- Carga e inspección de dimensiones (`20,780 filas × 41 columnas`). 
- Conversión explícita del campo `date` al tipo de dato `datetime64`.

### 🔹 Fase 1: Calidad de Datos, Limpieza e Imputación

- **Diagnóstico de faltantes:** Identificación de 373,695 celdas nulas (43.9% del total) distribuidas en 30 columnas.
- **Mecanismos de pérdida:** Clasificación anatómica evidenciando patrones MNAR (datos no perdidos al azar debido a políticas heterogéneas de reporte por estado).
- **Filtrado:** Descarte de 6 columnas críticas con &gt;90% de nulos hacia el contenedor `df_dispersas`.
- **Limpieza e Imputación:** Eliminación de incrementos diarios negativos por reajustes administrativos, imputación de 2,728 ceros iniciales previos al primer caso por estado e interpolación temporal acotada a huecos $le 14$ días (75 celdas).

### 🔹 Fase 2: Estadísticos Descriptivos y Análisis Univariado

- Cálculo de medidas de tendencia central y dispersión (media, mediana, desviación estándar e IQR) a nivel global e interestatal.
- Análisis de forma evaluando la alta asimetría positiva y la curtosis leptocúrtica en el ritmo diario de contagios y fallecimientos.
- Identificación de días atípicos (*outliers*) y brotes mediante histogramas con KDE y diagramas de caja (*box plots*).

### 🔹 Fase 3: Feature Engineering (Métricas Epidemiológicas)

- **Tasa de Positividad Diaria:** Relación entre casos positivos nuevos y pruebas totales realizadas.
- **Tasa de Letalidad Observada (CFR):** Proporción acumulada entre fallecimientos y casos confirmados.
- **Ratios de Ocupación Crítica:** Proporción de hospitalizados en UCI y pacientes con ventilación mecánica.
- **Promedio Móvil de 7 Días:** Aplicación de ventana deslizante por estado (`rolling(7)`) para suprimir el ruido del efecto fin de semana.

### 🔹 Fase 4: Inferencia Estadística y Pruebas de Hipótesis

- **Pruebas de Normalidad:** Contrastes de Shapiro-Wilk y D'Agostino-Pearson confirmando que las distribuciones diarias de casos no siguen una distribución normal ($p &lt; 0.0001$).
- **Inferencia Interestatal:** Evaluación no paramétrica de Kruskal-Wallis ($H = 2455.3, \\epsilon^2 = 0.142$) demostrando diferencias estadísticamente significativas en la severidad epidemiológica entre estados.
