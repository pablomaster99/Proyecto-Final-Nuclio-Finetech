# DOCUMENTO MAESTRO DEL PROYECTO: MARKETING ANALYTICS PARA EMPRESA FINTECH

**Repositorio:** Proyecto-Final-Nuclio-Finetech
**Tipo de documento:** Fuente de verdad para memoria de Trabajo Fin de Máster en Data Analytics

---

## 1. VISIÓN GENERAL DEL REPOSITORIO

### 1.1 Objetivo general del proyecto

El proyecto tiene como finalidad analizar los datos de campañas de marketing de una empresa Fintech para identificar patrones, tendencias y factores que influyen en que un cliente acabe contratando un depósito a plazo fijo. Las campañas de marketing se basan en llamadas telefónicas que tuvieron lugar de mayo de 2018 a noviembre de 2020. Los registros vienen ordenados por fecha, aunque no existe una variable con la fecha completa en el dataset original. En algunos casos se requiere más de un contacto con el mismo cliente para determinar si el depósito acaba siendo contratado.

### 1.2 Tipo de problema analizado

Se trata de un problema de **clasificación binaria supervisada** en el dominio del marketing bancario/fintech. La variable objetivo (`y` / `subscribed_term_deposit`) indica si el cliente suscribió un depósito a plazo fijo (yes/no). El enfoque del repositorio se centra en el análisis exploratorio, la correlación estadística y el análisis multivariable, sin llegar a entrenar modelos predictivos de machine learning dentro del notebook principal.

### 1.3 Flujo general del proyecto (de datos a resultados)

El flujo se estructura en las siguientes fases secuenciales:

1. **Carga de datos:** Lectura automatizada de archivos CSV desde una carpeta configurada vía variables de entorno (`.env`).
2. **Exploración inicial:** Estadísticas descriptivas, tipos de datos, nulos, valores únicos para ambos datasets.
3. **Limpieza y preparación:** Eliminación de duplicados (12 registros), normalización de textos, renombrado de columnas a nombres descriptivos en inglés, creación de variables derivadas (bins/grupos), conversión de variable objetivo a binario.
4. **Análisis EDA:** Análisis univariable de tipología de cliente (edad, trabajo, estado civil, educación) y contexto macroeconómico.
5. **Análisis de correlaciones bivariables:** Correlación de Spearman y test Chi-cuadrado con V de Cramér para cuatro bloques: tipología de cliente, estado financiero, tipología de contacto, variables macroeconómicas.
6. **Análisis multivariable:** Generación de 120 combinaciones de pares de variables categóricas, evaluación mediante Información Mutua (Mutual Information), y heatmaps de las combinaciones relevantes.
7. **Visualización:** Generación de gráficos inline (matplotlib, seaborn, plotly) a lo largo de todo el análisis.

### 1.4 Outputs finales generados

- Gráficos de distribución de variables demográficas del cliente (4 subplots).
- Gráficos de evolución de indicadores macroeconómicos (4 subplots).
- Distribución de la tasa de suscripción al depósito (88.73% No / 11.27% Sí).
- Gráficos de barras de correlación de Spearman (4 bloques, 4 subplots resumen).
- Heatmaps de correlación Chi-cuadrado con V de Cramér (13 heatmaps individuales).
- Gráficos resumen de barras apiladas por bloque de variables (4 paneles resumen).
- Evaluación de Información Mutua para 120 combinaciones de variables, con 10 combinaciones relevantes identificadas.
- Heatmaps multivariable de las combinaciones relevantes (10 heatmaps).

---

## 2. INVENTARIO COMPLETO DE ARCHIVOS

### 2.1 Directorio raíz (`/`)

| Nombre exacto | Tipo | Rol dentro del proyecto | Relación con otros archivos |
|---|---|---|---|
| `README.md` | Documentación | Describe el objetivo, las tareas a realizar y el contexto temporal del proyecto. | Documento de referencia general. |
| `.gitignore` | Configuración | Define archivos excluidos del control de versiones: `.env`, `__pycache__`, `juntandoDatos.ipynb`. | Protege variables de entorno y archivos temporales. |
| `2_marketing_fintech_guía_proyecto.docx` | Documentación | Guía del proyecto proporcionada por Nuclio (enunciado académico). Archivo Word de ~1.9 MB. | Define los requisitos del trabajo. |
| `Grupo_1_Analisis_Fintech.ipynb` | Notebook (análisis principal) | Notebook Jupyter que contiene TODO el flujo analítico: carga, limpieza, EDA, correlaciones y análisis multivariable. 86 celdas. ~2.5 MB. | Importa `funciones_data_analisis.py` y `funciones_fintech.py`. Consume los datasets de `data/`. |
| `funciones_data_analisis.py` | Script Python (módulo) | Módulo de funciones auxiliares genéricas para carga, exploración y visualización de datos. | Importado como `fda` en el notebook principal. |
| `funciones_fintech.py` | Script Python (módulo) | Módulo de funciones específicas del proyecto Fintech para limpieza, transformación y visualización estadística avanzada. | Importado como `ff` en el notebook principal. |

### 2.2 Directorio `data/`

| Nombre exacto | Tipo | Rol dentro del proyecto | Relación con otros archivos |
|---|---|---|---|
| `bank-additional_bank-additional-full.csv` | Dataset principal | Contiene los 41,188 registros de la campaña de marketing bancario. Delimitador: punto y coma (`;`). ~5.6 MB. | Dataset principal consumido por el notebook. |
| `datos_contexto.csv` | Dataset complementario | Contiene 24 registros de indicadores macroeconómicos trimestrales (2008-2013). Delimitador: coma (`,`). ~768 bytes. | Utilizado en el análisis macroeconómico del notebook. |
| `data_info.rtf` | Documentación | Diccionario de datos en formato RTF (Rich Text Format). Contiene la descripción oficial de las 21 columnas del dataset principal. ~18 KB. | Referencia para la interpretación de variables. |

### 2.3 Directorio `funciones_personalizadas/`

| Nombre exacto | Tipo | Rol dentro del proyecto | Relación con otros archivos |
|---|---|---|---|
| `funciones_data_analisis.ipynb` | Notebook (desarrollo de funciones) | Versión notebook del módulo `funciones_data_analisis.py`. Contiene el mismo código organizado en celdas interactivas. Sirve como entorno de desarrollo de las funciones antes de exportarlas a `.py`. | Se exporta a `funciones_data_analisis.py` en la raíz. |
| `funciones_fintech.ipynb` | Notebook (desarrollo de funciones) | Versión notebook del módulo `funciones_fintech.py`. Mismo código organizado en celdas interactivas. | Se exporta a `funciones_fintech.py` en la raíz. |

### 2.4 Archivos excluidos por `.gitignore`

| Nombre | Motivo de exclusión |
|---|---|
| `.env` | Contiene la variable `DATA_PATH` con la ruta local a la carpeta de datos. Información sensible/local. |
| `__pycache__/` | Directorio de caché de Python generado automáticamente. |
| `juntandoDatos.ipynb` | Notebook auxiliar excluido del repositorio (posiblemente usado para unir datos en etapas tempranas). |

---

## 3. DATASETS

### 3.1 Dataset principal: `bank-additional_bank-additional-full.csv`

- **Nombre del archivo:** `bank-additional_bank-additional-full.csv`
- **Ubicación:** `data/`
- **Origen:** Dataset de campañas de marketing bancario. Basado en llamadas telefónicas realizadas de mayo de 2018 a noviembre de 2020, según el README. El formato y las variables son consistentes con el conocido "Bank Marketing Dataset" del UCI Machine Learning Repository, adaptado al contexto del proyecto.
- **Formato:** CSV con delimitador punto y coma (`;`)
- **Número de filas:** 41,188 (41,176 tras eliminar 12 duplicados)
- **Número de columnas:** 21 originales (28 tras feature engineering)
- **Variable objetivo:** `y` (renombrada a `subscribed_term_deposit`)
- **Distribución de la variable objetivo:** 88.73% "no" / 11.27% "yes" (dataset desbalanceado)
- **Uso dentro del proyecto:** Dataset central utilizado en todas las fases del análisis (EDA, correlaciones, multivariable)

#### 3.1.1 Variables originales (21 columnas)

**Bloque 1: Datos del cliente (7 variables)**

| Variable original | Nombre renombrado | Tipo de dato | Descripción |
|---|---|---|---|
| `age` | `age` | Numérico (int) | Edad del cliente en años. |
| `job` | `job` | Categórico nominal | Tipo de empleo del cliente. Valores: housemaid, services, admin (renombrado a administrative_staff), blue-collar (renombrado a blue_collar), self-employed (renombrado a self_employed), technician, entrepreneur, management, student, retired, unemployed, unknown. |
| `marital` | `marital_status` | Categórico nominal | Estado civil del cliente. Valores: married, single, divorced, unknown. |
| `education` | `education` | Categórico ordinal | Nivel de educación del cliente. Valores ordenados: unknown, illiterate, basic.4y (renombrado a basic_4y), basic.6y (renombrado a basic_6y), basic.9y (renombrado a basic_9y), high.school (renombrado a high_school), professional.course (renombrado a professional_course), university.degree (renombrado a university_degree). |
| `default` | `credit_default` | Categórico nominal | Si el cliente tiene crédito en impago. Valores: yes, no, unknown. |
| `housing` | `housing_loan` | Categórico nominal | Si el cliente tiene préstamo hipotecario. Valores: yes, no, unknown. |
| `loan` | `personal_loan` | Categórico nominal | Si el cliente tiene préstamo personal. Valores: yes, no, unknown. |

**Bloque 2: Datos de la campaña de contacto (5 variables)**

| Variable original | Nombre renombrado | Tipo de dato | Descripción |
|---|---|---|---|
| `contact` | `contact_type` | Categórico nominal | Tipo de comunicación del último contacto. Valores: telephone, cellular. |
| `month` | `last_contact_month` | Categórico ordinal | Mes del último contacto. Valores ordenados: mar, apr, may, jun, jul, aug, sep, oct, nov, dec. |
| `day_of_week` | `last_contact_day` | Categórico nominal | Día de la semana del último contacto. Valores: mon, tue, wed, thu, fri. |
| `duration` | `last_contact_duration_secs` | Numérico (int) | Duración del último contacto en segundos. |
| `campaign` | `number_contacts` | Numérico (int) | Número de contactos realizados durante esta campaña para este cliente. |

**Bloque 3: Historial de campañas anteriores (3 variables)**

| Variable original | Nombre renombrado | Tipo de dato | Descripción |
|---|---|---|---|
| `pdays` | `number_days_last_contact` | Numérico (int) | Número de días transcurridos desde que el cliente fue contactado por última vez en una campaña anterior. Valor 999 indica que el cliente no fue contactado previamente. |
| `previous` | `number_of_previous_contacts` | Numérico (int) | Número de contactos realizados antes de esta campaña para este cliente. |
| `poutcome` | `outcome_previous_campaign` | Categórico nominal | Resultado de la campaña de marketing anterior. Valores: success, failure, nonexistent. |

**Bloque 4: Indicadores macroeconómicos (5 variables)**

| Variable original | Nombre renombrado | Tipo de dato | Descripción |
|---|---|---|---|
| `emp.var.rate` | `employement_variation_rate` | Numérico (float) | Tasa de variación del empleo - indicador trimestral. |
| `cons.price.idx` | `consumer_price_index` | Numérico (float) | Índice de precios al consumidor - indicador mensual. |
| `cons.conf.idx` | `consumer_confidence_index` | Numérico (float) | Índice de confianza del consumidor - indicador mensual. |
| `euribor3m` | `euribor_3m` | Numérico (float) | Tasa euríbor a 3 meses - indicador diario. |
| `nr.employed` | `number_employees` | Numérico (float) | Número de empleados - indicador trimestral. |

**Bloque 5: Variable objetivo (1 variable)**

| Variable original | Nombre renombrado | Tipo de dato | Descripción |
|---|---|---|---|
| `y` | `subscribed_term_deposit` | Binario | Si el cliente ha suscrito un depósito a plazo fijo. Valores originales: yes/no. Convertido a 1/0 para el análisis de correlaciones. |

#### 3.1.2 Variables derivadas durante feature engineering (7 columnas adicionales)

| Variable creada | Tipo de dato | Descripción | Método de creación |
|---|---|---|---|
| `age_group` | Categórico ordinal | Grupo de edad del cliente. Intervalos: 18-25, 26-35, 36-45, 46-55, 56-65, 65+. | `pd.cut()` sobre `age` con bins [18, 25, 35, 45, 55, 65, 100]. |
| `last_contact_duration_mins` | Numérico (float) | Duración del último contacto en minutos. | `duration / 60`. |
| `last_contact_duration_mins_group` | Categórico ordinal | Grupo de duración de la última llamada en minutos. Intervalos: 0-1, 1-2, 2-3, 3-5, 5-10, 10-20, 20+. | `pd.cut()` sobre `last_contact_duration_mins`. |
| `employement_variation_rate_group` | Categórico ordinal | Grupo de tasa de variación del empleo. Intervalos: < -0.5, -0.5-0, 0-0.5, > 0.5. | `pd.cut()` sobre `emp.var.rate`. |
| `consumer_price_index_group` | Categórico ordinal | Grupo de índice de precios al consumidor. Intervalos: <90, 90-94, 94-100, 100-104, 104+. | `pd.cut()` sobre `cons.price.idx`. |
| `consumer_confidence_index_group` | Categórico ordinal | Grupo de índice de confianza del consumidor. Intervalos: <=-35, -35-0, 0-35, 35-100, >100. | `pd.cut()` sobre `cons.conf.idx`. |
| `euribor_3m_group` | Categórico ordinal | Grupo de tasa euríbor a 3 meses. Intervalos: <0, 0-1, 1-2, 2-3, 3-4, 4-5, 5+. | `pd.cut()` sobre `euribor3m`. |

### 3.2 Dataset complementario: `datos_contexto.csv`

- **Nombre del archivo:** `datos_contexto.csv`
- **Ubicación:** `data/`
- **Origen:** Datos macroeconómicos trimestrales recopilados para contextualizar el periodo de las campañas.
- **Formato:** CSV con delimitador coma (`,`), codificación UTF-8
- **Número de filas:** 24 (6 años x 4 trimestres)
- **Número de columnas:** 6 originales (7 con la columna derivada `Fecha`)
- **Cobertura temporal:** Q1 2008 a Q4 2013
- **Variable objetivo:** No aplica (dataset de contexto)
- **Uso dentro del proyecto:** Utilizado exclusivamente en la sección de análisis macroeconómico (celdas 25-26 del notebook) para generar gráficos de contexto temporal.

#### 3.2.1 Variables del dataset de contexto

| Variable | Tipo de dato | Descripción |
|---|---|---|
| `Año` | Numérico (int) | Año del registro. Rango: 2008-2013. |
| `Trimestre` | Categórico | Trimestre del año. Valores: Q1, Q2, Q3, Q4. |
| `ConfianzaConsumidor` | Numérico (float) | Índice de confianza del consumidor. Todos los valores son negativos en el rango analizado (de -28.3 a -50.0). |
| `CPI` | Numérico (float) | Índice de precios al consumidor. Rango: 92.4 a 107.4 (tendencia ascendente). |
| `TasaEmpleo(%)` | Numérico (float) | Tasa de empleo en porcentaje. Rango: 52.1% a 61.5% (tendencia descendente). |
| `Euribor3M(%)` | Numérico (float) | Tasa euríbor a 3 meses en porcentaje. Rango: 0.19% a 5.0% (caída pronunciada tras 2008). |

#### 3.2.2 Variable derivada

| Variable | Descripción | Método |
|---|---|---|
| `Fecha` | Concatenación de Año y Trimestre en formato "AAAA-QX" (ej: "2008-Q1"). | Concatenación de strings para su uso como eje X en gráficos. |

---

## 4. NOTEBOOKS Y ANÁLISIS

### 4.1 Notebook principal: `Grupo_1_Analisis_Fintech.ipynb`

- **Ubicación:** Raíz del repositorio
- **Tamaño:** ~2.5 MB (incluye outputs gráficos embebidos)
- **Total de celdas:** 86 (mezcla de celdas de código y celdas markdown)
- **Librerías utilizadas:** pandas, numpy, matplotlib, seaborn, plotly.express, scipy.stats, sklearn.feature_selection (mutual_info_classif), missingno, fuzzywuzzy, dotenv
- **Módulos personalizados importados:** `funciones_data_analisis` (alias `fda`), `funciones_fintech` (alias `ff`)

#### Fase 1: Importación de librerías y configuración (celdas 0-4)

- **Objetivo:** Cargar todas las dependencias y configurar la ruta a los datos.
- **Acciones:**
  - Importación de librerías estándar, de manipulación de datos, visualización, texto y estadística.
  - Importación de los dos módulos personalizados (`fda`, `ff`).
  - Carga de la variable de entorno `DATA_PATH` desde el archivo `.env` mediante `dotenv`.

#### Fase 2: Carga de datos (celdas 5-10)

- **Objetivo:** Localizar, leer y cargar los archivos de datos en DataFrames.
- **Acciones:**
  - Se ejecuta `fda.carga_archivos(path)` que detecta 2 archivos: `bank-additional_bank-additional-full.csv` y `datos_contexto.csv`.
  - Se ejecuta `fda.leer_archivos(files, path)` que transforma ambos archivos en DataFrames almacenados en un diccionario `dict_data`.
  - **Resultado:** `bank-additional_bank-additional-full.csv` cargado como DataFrame de (41188, 21); `datos_contexto.csv` cargado como DataFrame de (24, 6).

#### Fase 3: Exploración inicial de los datos (celdas 11-12)

- **Objetivo:** Realizar una exploración descriptiva completa de ambos datasets.
- **Acciones:**
  - Para cada dataset se ejecuta `fda.exploracion_datos()` que muestra:
    - Número de filas y columnas.
    - 5 primeras, 5 últimas y 5 filas aleatorias.
    - Estadísticos descriptivos (`describe()`).
    - Resumen de tipos de datos, nulos, porcentaje de nulos, valores únicos y porcentaje de valores únicos.
- **Variables clave observadas:** Las 21 columnas originales del dataset bancario; las 6 columnas del dataset de contexto.

#### Fase 4: Limpieza de datos y configuración (celdas 13-20)

- **Objetivo:** Preparar los datos para el análisis.
- **Acciones realizadas:**
  1. **Asignación de variables:** `df_bank` para el dataset principal, `df_contexto` para el dataset complementario.
  2. **Eliminación de duplicados:** Se identifican y eliminan 12 registros duplicados. El DataFrame limpio pasa de 41,188 a 41,176 filas.
  3. **Feature engineering - creación de bins:**
     - `age_group`: 6 grupos de edad.
     - `last_contact_duration_mins`: Conversión de segundos a minutos.
     - `last_contact_duration_mins_group`: 7 grupos de duración de llamada.
     - `employement_variation_rate_group`: 4 grupos de tasa de variación de empleo.
     - `consumer_price_index_group`: 5 grupos de índice de precios.
     - `consumer_confidence_index_group`: 5 grupos de confianza del consumidor.
     - `euribor_3m_group`: 7 grupos de tasa euríbor.
  4. **Normalización de textos:** Conversión a minúsculas, eliminación de espacios, reemplazo de puntos y guiones por guiones bajos (ej: `basic.4y` → `basic_4y`, `admin` → `administrative_staff`).
  5. **Renombrado de columnas:** Las 21 columnas originales + 7 derivadas se renombran a 28 nombres descriptivos en inglés.
  6. **Conversión a categóricas:** 10 columnas se convierten a tipo `pd.Categorical` con órdenes definidos explícitamente.
  7. **Copia binaria:** Se crea `df_binario` donde `subscribed_term_deposit` se convierte de "yes"/"no" a 1/0 para cálculos de correlación.

#### Fase 5: Análisis EDA (celdas 21-28)

- **Objetivo:** Analizar la distribución de las variables clave.

**5a. Análisis tipología de cliente (celda 23):**
- Genera un panel de 4 subplots (2x2) con gráficos de barras:
  - Distribución de edad agrupada (`age_group`).
  - Distribución de ocupación (`job`).
  - Distribución de estado civil (`marital_status`).
  - Distribución de educación (`education`).
- Herramienta: matplotlib.

**5b. Análisis macroeconómico (celdas 25-26):**
- Se visualizan los datos del dataset `df_contexto` con un panel de 4 subplots (2x2):
  - Tasa de ocupación por trimestre (barras).
  - Índice de precios al consumidor normalizado sobre base 100 (barras).
  - Índice de confianza del consumidor (barras).
  - Tasa euríbor 3 meses (línea).
- Herramienta: matplotlib.

**5c. Distribución de la variable objetivo (celda 28):**
- Se calcula la distribución de `subscribed_term_deposit`:
  - **No:** 88.73%
  - **Sí:** 11.27%
- Observación: Dataset significativamente desbalanceado.

#### Fase 6: Correlaciones bivariables (celdas 29-72)

Esta fase se divide en dos metodologías aplicadas en paralelo:

**6a. Correlación de Spearman (celdas 30-44):**

Para cada bloque, las variables categóricas se convierten a numéricas mediante mapeo ordinal, y se calcula la correlación de Spearman respecto a `subscribed_term_deposit`:

- **Bloque Tipología cliente** (celdas 32-33): Variables `age`, `job`, `marital_status`, `education`.
- **Bloque Estado financiero** (celdas 35-36): Variables `credit_default`, `housing_loan`, `personal_loan`.
- **Bloque Tipología contacto** (celdas 38-39): Variables `last_contact_month`, `last_contact_day`, `last_contact_duration_secs`, `number_contacts`, `number_days_last_contact`, `number_of_previous_contacts`.
- **Bloque Macroeconómico** (celdas 41-42): Variables `employement_variation_rate`, `consumer_price_index`, `consumer_confidence_index`, `euribor_3m`.

Cada bloque genera un gráfico de barras de correlación y un **panel resumen** (celda 44) con 4 subplots (2x2).

**6b. Correlación Chi-cuadrado con V de Cramér (celdas 45-72):**

Para cada par de variables (categórica vs. variable objetivo), se genera una tabla de contingencia normalizada y se calculan: estadístico Chi-cuadrado, p-valor, grados de libertad (dof) y V de Cramér.

- **Bloque Tipología cliente** (celdas 47-54):
  - `age_group` vs `subscribed_term_deposit` (heatmap + estadísticos).
  - `job` vs `subscribed_term_deposit` (heatmap + estadísticos).
  - `marital_status` vs `subscribed_term_deposit` (heatmap + estadísticos).
  - `education` vs `subscribed_term_deposit` (heatmap + estadísticos).
  - Panel resumen de barras apiladas (celda 54): 4 subplots.

- **Bloque Estado financiero** (celdas 55-60):
  - `credit_default` vs `subscribed_term_deposit`.
  - `housing_loan` vs `subscribed_term_deposit`.
  - `personal_loan` vs `subscribed_term_deposit`.
  - Panel resumen de barras apiladas (celda 60): 3 subplots en fila.

- **Bloque Tipología contacto** (celdas 61-65):
  - `number_of_previous_contacts` vs `subscribed_term_deposit`.
  - `last_contact_duration_mins_group` vs `subscribed_term_deposit`.
  - Panel resumen de barras apiladas (celda 65): 2 subplots.

- **Bloque Macroeconómico** (celdas 66-72):
  - `employement_variation_rate_group` vs `subscribed_term_deposit`.
  - `consumer_price_index_group` vs `subscribed_term_deposit`.
  - `consumer_confidence_index_group` vs `subscribed_term_deposit`.
  - `euribor_3m_group` vs `subscribed_term_deposit`.
  - Panel resumen de barras apiladas (celda 72): 4 subplots (2x2).

#### Fase 7: Análisis multivariable (celdas 73-85)

- **Objetivo:** Identificar combinaciones de pares de variables categóricas que, en interacción, aportan información predictiva relevante sobre la variable objetivo.

**Acciones:**
1. **Generación de combinaciones** (celdas 76-77): Se obtienen las 16 columnas de tipo categórico y se generan todas las combinaciones de 2 elementos: **120 combinaciones** en total.
2. **Diccionario de nombres** (celda 79): Se crea un diccionario que mapea los nombres técnicos de las variables a nombres descriptivos en español (ej: `age_group` → "Edad", `euribor_3m_group` → "Euribor").
3. **Conversión de variable objetivo** (celda 80): `subscribed_term_deposit` se mapea de "no"/"yes" a 0/1 directamente sobre `df_bank_clean`.
4. **Tabla de referencia de Información Mutua** (celda 82 - markdown): Se documenta la interpretación de los valores de MI:
   - 0.000: Sin información
   - 0.001-0.01: Muy débil
   - 0.01-0.05: Débil/moderado
   - 0.05-0.1: Moderado
   - 0.1-0.3: Fuerte
   - 0.3+: Muy fuerte
   - Se indica que dada la baja entropía base, incluso un MI moderado puede ser relevante. Se usa threshold de 0.03.
5. **Evaluación de Información Mutua** (celda 83): Se ejecuta `ff.evaluar_informacion_mutua()` con threshold=0.03. **10 combinaciones relevantes identificadas:**
   - Impago × Variación Empleo (MI: 0.0416)
   - Impago × Euríbor (MI: 0.0403)
   - Préstamo × Euríbor (MI: 0.0336)
   - Contacto × Variación Empleo (MI: 0.0362)
   - Contacto × Euríbor (MI: 0.0402)
   - Resultado Prev. × Variación Empleo (MI: 0.0311)
   - Resultado Prev. × Euríbor (MI: 0.0370)
   - Variación Empleo × Confianza Consumidor (MI: 0.0311)
   - Variación Empleo × Euríbor (MI: 0.0418 y 0.0311)
   - Confianza Consumidor × Euríbor (MI: 0.0398)
6. **Heatmaps multivariable** (celda 85): Se generan heatmaps para cada una de las 10 combinaciones relevantes usando `ff.heatmap_multivariable()`. Cada heatmap muestra la tasa media de suscripción al depósito en la intersección de dos variables categóricas, excluyendo valores "unknown".

### 4.2 Notebooks auxiliares

#### 4.2.1 `funciones_personalizadas/funciones_data_analisis.ipynb`

- **Objetivo:** Entorno de desarrollo interactivo para las funciones del módulo `funciones_data_analisis.py`.
- **Contenido:** Mismo código que `funciones_data_analisis.py` organizado en celdas Jupyter.
- **Uso:** Desarrollo y prueba de funciones antes de exportarlas al archivo `.py`.
- **No contiene análisis propios ni outputs.**

#### 4.2.2 `funciones_personalizadas/funciones_fintech.ipynb`

- **Objetivo:** Entorno de desarrollo interactivo para las funciones del módulo `funciones_fintech.py`.
- **Contenido:** Mismo código que `funciones_fintech.py` organizado en celdas Jupyter.
- **Uso:** Desarrollo y prueba de funciones antes de exportarlas al archivo `.py`.
- **No contiene análisis propios ni outputs.**

---

## 5. FUNCIONES Y SCRIPTS

### 5.1 Módulo `funciones_data_analisis.py`

Módulo de funciones auxiliares genéricas reutilizables para análisis de datos. Se importa en el notebook como `fda`.

**Librerías requeridas:** os, sys, warnings, dotenv, pandas, numpy, missingno, matplotlib, seaborn, plotly, unicodedata, fuzzywuzzy, re, scipy.stats

#### 5.1.1 Funciones de lectura de datos

| Función | Inputs | Outputs | Descripción | Uso en el flujo |
|---|---|---|---|---|
| `carga_archivos(path)` | `path` (str): ruta al directorio | `list[str]`: lista de nombres de archivos .csv, .xlsx, .xls | Obtiene los nombres de archivos de datos presentes en una carpeta. Filtra por extensiones .csv, .xlsx y .xls. | Fase 2 (celda 7): Detecta los 2 archivos en la carpeta `data/`. |
| `leer_archivo(ruta_completa)` | `ruta_completa` (str): ruta completa al archivo | `pd.DataFrame` o `None` | Lee un archivo individual (CSV o Excel) y lo transforma en DataFrame. Soporta múltiples encodings para CSV (utf-8, latin-1, iso-8859-1, cp1252). Usa detección automática de delimitador (`sep=None, engine='python'`). | Llamada internamente por `leer_archivos()`. |
| `leer_archivos(files, path)` | `files` (list[str]): nombres de archivos; `path` (str): ruta a la carpeta | `dict{str: pd.DataFrame}`: diccionario nombre→DataFrame | Itera sobre la lista de archivos, invoca `leer_archivo()` para cada uno y los almacena en un diccionario. Imprime las dimensiones de cada DataFrame cargado. | Fase 2 (celda 9): Carga ambos datasets en `dict_data`. |

#### 5.1.2 Funciones de exploración de datos

| Función | Inputs | Outputs | Descripción | Uso en el flujo |
|---|---|---|---|---|
| `exploracion_datos(df)` | `df` (pd.DataFrame) | `pd.DataFrame` (resumen de exploración) | Realiza y muestra una exploración completa: filas/columnas, head, tail, sample, describe, tipos de datos, nulos, porcentaje nulos, valores únicos, número de valores únicos y porcentaje. | Fase 3 (celda 12): Exploración de ambos datasets. |
| `exploracion_varios_dataframes(dict_data)` | `dict_data` (dict) | Ninguno (imprime en pantalla) | Itera sobre un diccionario de DataFrames y ejecuta `exploracion_datos()` para cada uno. | Disponible pero no utilizada directamente en el notebook (se usa un bucle manual equivalente). |

#### 5.1.3 Funciones de limpieza de datos

| Función | Inputs | Outputs | Descripción | Uso en el flujo |
|---|---|---|---|---|
| `normalizar_textos(df)` | `df` (pd.DataFrame) | `pd.DataFrame` (normalizado) | Normaliza columnas de tipo texto: convierte a minúsculas, elimina espacios, reemplaza puntos finales, sustituye puntos y guiones entre palabras por guiones bajos. | No se usa directamente (se usa la versión del módulo `ff` que incluye renombrado de 'admin' a 'administrative_staff'). |
| `normalizar_binario(df, columna_a_normalizar)` | `df` (pd.DataFrame); `columna_a_normalizar` (str) | `pd.DataFrame` | Transforma valores 'yes'/'no' en 1/0 para una columna especificada. Alerta si hay valores no contemplados. | No se usa directamente (se usa la versión del módulo `ff`). |

#### 5.1.4 Funciones de visualización

| Función | Inputs | Outputs | Descripción | Uso en el flujo |
|---|---|---|---|---|
| `plotly_barras_univariable(df, variable)` | `df` (pd.DataFrame); `variable` (str) | Gráfico Plotly interactivo | Genera un gráfico de barras interactivo con Plotly mostrando el porcentaje de cada categoría de una variable. Incluye hover con conteo y porcentaje. | Disponible pero no utilizada en el notebook principal (se usan gráficos matplotlib directamente). |
| `plotly_histograma_univariable(df, variable)` | `df` (pd.DataFrame); `variable` (str) | Gráfico Plotly interactivo | Genera un histograma interactivo con Plotly mostrando la distribución porcentual de una variable numérica. | Disponible pero no utilizada en el notebook principal. |

### 5.2 Módulo `funciones_fintech.py`

Módulo de funciones específicas del proyecto Fintech. Se importa en el notebook como `ff`.

**Librerías requeridas:** os, sys, warnings, pandas, numpy, missingno, matplotlib, seaborn, plotly, unicodedata, fuzzywuzzy, re, scipy.stats, itertools.combinations, sklearn.feature_selection.mutual_info_classif

#### 5.2.1 Funciones de limpieza y preparación

| Función | Inputs | Outputs | Descripción | Uso en el flujo |
|---|---|---|---|---|
| `renombrar_columnas(df)` | `df` (pd.DataFrame) con 28 columnas | `pd.DataFrame` con columnas renombradas | Renombra las 28 columnas (21 originales + 7 derivadas) a nombres descriptivos en inglés (ej: `duration` → `last_contact_duration_secs`, `y` → `subscribed_term_deposit`). | Fase 4 (celda 17). |
| `columnas_categoricas(df)` | `df` (pd.DataFrame) | `pd.DataFrame` con 10 columnas categóricas | Convierte 10 columnas a tipo `pd.Categorical` con categorías y órdenes definidos explícitamente. Incluye listas ordenadas para: job (12 categorías), marital_status (4), education (8, ordinal), credit_default (3), housing_loan (3), personal_loan (3), contact_type (2), last_contact_month (10, ordinal), last_contact_day (5), outcome_previous_campaign (3). | Fase 4 (celda 17). |
| `normalizar_textos(df)` | `df` (pd.DataFrame) | `pd.DataFrame` | Misma lógica que la versión en `fda` pero con una adición específica: si la columna es 'job', renombra 'admin' a 'administrative_staff'. | Fase 4 (celda 17). |
| `normalizar_binario(df)` | `df` (pd.DataFrame) con columna `subscribed_term_deposit` | Ninguno (modifica in-place) | Convierte la columna `subscribed_term_deposit` de 'yes'/'no' a 1/0 (int64). Versión simplificada específica para esta columna. | Fase 4 (celda 20): Aplicada sobre `df_binario`. |

#### 5.2.2 Funciones de correlación y visualización estadística

| Función | Inputs | Outputs | Descripción | Uso en el flujo |
|---|---|---|---|---|
| `cramers_v(df)` | `df` (pd.DataFrame): tabla de contingencia | `float`: valor V de Cramér | Calcula la V de Cramér a partir de una tabla de contingencia. Usa chi2_contingency de scipy. Fórmula: sqrt(chi2 / (n × k)) donde k = min(dimensiones) - 1. | Llamada internamente por `heatmap_correlation()`. |
| `heatmap_correlation(df, df_2, columna, title, ylable)` | `df`: tabla de contingencia; `df_2`: DataFrame original; `columna` (str): nombre de la columna; `title` (str); `ylable` (str) | Heatmap matplotlib + estadísticos impresos | Genera un heatmap de correlación normalizado por filas (porcentajes), calcula e imprime chi2, p-valor, dof, V de Cramér. Muestra conteos y porcentajes de la variable. Colormap: YlGnBu. | Fase 6b: Generación de los 13 heatmaps individuales de correlación (celdas 49-70). |
| `grafico_correlacion_spearman(df, df_2, title)` | `df` (pd.DataFrame): correlaciones Spearman; `df_2` (pd.DataFrame): datos originales; `title` (str) | Gráfico de barras matplotlib + tablas de conteo | Genera un gráfico de barras horizontales con los valores de correlación de Spearman respecto a `subscribed_term_deposit`. Para cada variable, imprime la tabla de conteos y porcentajes. Color: coral. | Fase 6a: Gráficos de correlación Spearman (celdas 33, 36, 39, 42). |
| `generar_combinaciones_de_dos(elementos)` | `elementos` (iterable) | `list[tuple]`: lista de pares | Genera todas las combinaciones de 2 elementos a partir de una lista. Usa `itertools.combinations`. | Fase 7 (celda 77): Genera las 120 combinaciones de variables categóricas. |
| `evaluar_informacion_mutua(df, variables_a_combinar, nombres_variables, threshold)` | `df` (pd.DataFrame); `variables_a_combinar` (list[tuple]); `nombres_variables` (dict, opcional); `threshold` (float, default 0.05) | `list[tuple]`: combinaciones relevantes | Para cada par de variables, crea una variable de interacción concatenando sus valores, aplica one-hot encoding, y calcula la Información Mutua (`mutual_info_classif` de sklearn) respecto a `subscribed_term_deposit`. Filtra las interacciones cuyo MI supere el threshold. | Fase 7 (celda 83): Evaluación con threshold=0.03, identifica 10 combinaciones relevantes. |
| `heatmap_multivariable(df, combinaciones, nombres_variables)` | `df` (pd.DataFrame); `combinaciones` (list[tuple]); `nombres_variables` (dict) | Múltiples heatmaps matplotlib | Para cada par de variables, genera una tabla pivot con la media de `subscribed_term_deposit`, excluye valores "unknown", y crea un heatmap con formato porcentual. Colormap: Blues. | Fase 7 (celda 85): Generación de 10 heatmaps multivariable. |

---

## 6. MODELOS Y RESULTADOS

### 6.1 Estado del modelado predictivo

El README del proyecto especifica como tarea 3 la "Construcción de un modelo de regresión logística simple para predecir la probabilidad de suscripción a un depósito a plazo". Sin embargo, **en el notebook principal no se implementa ningún modelo de machine learning**. El análisis se detiene en la fase de correlaciones y análisis multivariable.

No se encontraron en el repositorio:
- Archivos de modelos serializados (.pkl, .joblib, .h5, etc.)
- Celdas de entrenamiento de modelos (train/test split, fit, predict)
- Métricas de evaluación de modelos (accuracy, precision, recall, F1, AUC-ROC)
- Matrices de confusión

### 6.2 Técnicas estadísticas aplicadas (en lugar de modelado predictivo)

Aunque no se construyen modelos ML, el proyecto aplica las siguientes técnicas estadísticas cuantitativas:

| Técnica | Librería/Función | Variables analizadas | Propósito |
|---|---|---|---|
| **Correlación de Spearman** | `pd.DataFrame.corr(method='spearman')` | 4 bloques de variables vs. `subscribed_term_deposit` | Medir la relación monótona entre variables ordinales/numéricas y la variable objetivo. |
| **Test Chi-cuadrado de independencia** | `scipy.stats.chi2_contingency()` | 13 pares de variables categóricas | Evaluar la independencia estadística entre variables categóricas y la variable objetivo. |
| **V de Cramér** | Función personalizada `cramers_v()` | Las mismas 13 tablas de contingencia | Medir la fuerza de asociación entre variables categóricas (complemento del chi-cuadrado). |
| **Información Mutua (Mutual Information)** | `sklearn.feature_selection.mutual_info_classif()` | 120 combinaciones de pares de variables categóricas | Detectar relaciones no lineales entre interacciones de variables y la variable objetivo. Threshold: 0.03. |

### 6.3 Resultados cuantitativos clave

**Distribución de la variable objetivo:**
- No suscribió depósito: 88.73%
- Sí suscribió depósito: 11.27%

**Combinaciones multivariable relevantes identificadas (MI > 0.03):**

| Combinación | Interacción específica | Valor MI |
|---|---|---|
| Impago × Variación Empleo | no_< -0.5 | 0.0416 |
| Variación Empleo × Euríbor | < -0.5_0-1 | 0.0419 |
| Impago × Euríbor | no_0-1 | 0.0403 |
| Contacto × Euríbor | cellular_0-1 | 0.0402 |
| Confianza Consumidor × Euríbor | <=-35_4-5 | 0.0398 |
| Resultado Prev. × Euríbor | nonexistent_4-5 | 0.0370 |
| Contacto × Variación Empleo | cellular_< -0.5 | 0.0362 |
| Préstamo × Euríbor | no_0-1 | 0.0336 |
| Variación Empleo × Confianza Consumidor | > 0.5_<=-35 | 0.0311 |
| Resultado Prev. × Variación Empleo | nonexistent_> 0.5 | 0.0311 |

---

## 7. DASHBOARDS / VISUALIZACIONES

### 7.1 Herramientas de visualización utilizadas

| Herramienta | Versión/Uso | Tipo de gráficos |
|---|---|---|
| **matplotlib** | Librería principal de visualización | Gráficos de barras, barras apiladas, líneas, subplots. |
| **seaborn** | Complemento de matplotlib | Heatmaps de correlación. |
| **plotly.express** | Disponible pero no utilizado en el output final | Funciones definidas (`plotly_barras_univariable`, `plotly_histograma_univariable`) pero no invocadas en el notebook. |

### 7.2 Inventario completo de visualizaciones generadas

#### Panel 1: Distribución de tipología de cliente (celda 23)
- **Tipo:** 4 subplots (2x2) de gráficos de barras.
- **Métricas/KPIs:** Distribución porcentual de edad agrupada, ocupación, estado civil y educación.
- **Dataset fuente:** `df_bank_clean` (41,176 registros).

#### Panel 2: Indicadores macroeconómicos (celda 26)
- **Tipo:** 4 subplots (2x2): 3 gráficos de barras + 1 gráfico de línea.
- **Métricas/KPIs:** Tasa de ocupación (%), Índice de precios normalizado base 100, Índice de confianza del consumidor, Euríbor 3M (%).
- **Dataset fuente:** `df_contexto` (24 registros trimestrales).

#### Gráficos de correlación Spearman (celdas 33, 36, 39, 42)
- **Tipo:** 4 gráficos de barras individuales.
- **Métricas/KPIs:** Coeficiente de correlación de Spearman por variable respecto a `subscribed_term_deposit`.
- **Dataset fuente:** `df_binario` (con variable objetivo codificada como 0/1).

#### Panel 3: Resumen correlaciones Spearman (celda 44)
- **Tipo:** 4 subplots (2x2) de gráficos de barras.
- **Métricas/KPIs:** Resumen visual de todas las correlaciones Spearman por bloque.
- **Dataset fuente:** DataFrames de correlación calculados.

#### Heatmaps Chi-cuadrado individuales (celdas 49-70)
- **Tipo:** 13 heatmaps individuales.
- **Métricas/KPIs:** Porcentaje de suscripción por categoría, chi2, p-valor, dof, V de Cramér.
- **Dataset fuente:** Tablas de contingencia derivadas de `df_bank_clean`.
- **Detalle por heatmap:**
  1. Grupo de edad vs Suscripción depósito
  2. Trabajo vs Suscripción depósito
  3. Estado civil vs Suscripción depósito
  4. Educación vs Suscripción depósito
  5. Impago de crédito vs Suscripción depósito
  6. Hipoteca vs Suscripción depósito
  7. Préstamo personal vs Suscripción depósito
  8. Número de contactos previos vs Suscripción depósito
  9. Duración última llamada vs Suscripción depósito
  10. Tasa variación empleo vs Suscripción depósito
  11. Índice precios consumidor vs Suscripción depósito
  12. Confianza consumidor vs Suscripción depósito
  13. Euríbor 3M vs Suscripción depósito

#### Panel 4: Resumen correlaciones tipo cliente (celda 54)
- **Tipo:** 4 subplots (2x2) de barras apiladas.
- **Métricas/KPIs:** Proporción de suscripción/no suscripción por grupo de edad, trabajo, estado civil y educación.

#### Panel 5: Resumen correlaciones estado financiero (celda 60)
- **Tipo:** 3 subplots (1x3) de barras apiladas.
- **Métricas/KPIs:** Proporción de suscripción por impago, hipoteca y préstamo personal.

#### Panel 6: Resumen correlaciones tipo contacto (celda 65)
- **Tipo:** 2 subplots (1x2) de barras apiladas.
- **Métricas/KPIs:** Proporción de suscripción por número de contactos previos y duración de la última llamada.

#### Panel 7: Resumen correlaciones macroeconómicas (celda 72)
- **Tipo:** 4 subplots (2x2) de barras apiladas.
- **Métricas/KPIs:** Proporción de suscripción por variación empleo, índice precios, confianza consumidor y euríbor.

#### Heatmaps multivariable (celda 85)
- **Tipo:** 10 heatmaps individuales.
- **Métricas/KPIs:** Tasa media de suscripción al depósito en la intersección de dos variables categóricas.
- **Dataset fuente:** `df_bank_clean` con variable objetivo binaria.
- **Combinaciones graficadas:** Las 10 combinaciones relevantes identificadas por Información Mutua (listadas en sección 6.3).

### 7.3 Dashboard externo

El README menciona como tarea 4 el "Diseño e implementación de un dashboard interactivo utilizando la herramienta de visualización que se desee (Looker, Tableau, etc.)". **No se encontró ningún archivo de dashboard externo en el repositorio** (ni archivos .twbx de Tableau, ni configuraciones de Looker, ni archivos de Power BI). Las visualizaciones del proyecto se limitan a los gráficos inline generados dentro del notebook Jupyter.

### 7.4 Total de visualizaciones

| Categoría | Cantidad |
|---|---|
| Paneles multi-subplot | 7 |
| Heatmaps individuales chi-cuadrado | 13 |
| Gráficos Spearman individuales | 4 |
| Heatmaps multivariable | 10 |
| **Total de figuras generadas** | **34** |
| **Total de subplots individuales** | **~53** |
