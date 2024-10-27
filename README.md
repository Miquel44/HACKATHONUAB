# HACKATHONUAB
Presentación del Proyecto: Reto "Caronte" 📊
Hackathon UAB

Este repositorio contiene nuestro proyecto para el Hackathon UAB, donde aceptamos el Reto Caronte. En este desafío, desarrollamos modelos predictivos y herramientas de análisis diseñadas para mejorar el rendimiento académico de los estudiantes mediante datos extraídos de Moodle.
🎯 Objetivo del Proyecto

Nuestro objetivo en el reto de Caronte es desarrollar modelos que:

-Predigan las notas finales de los estudiantes.
-Recomienden actividades de refuerzo personalizadas.
-Analicen patrones de estudio y rendimiento académico, generando insights que permitan mejorar la experiencia de aprendizaje.

🔍 Datos Utilizados

Para lograr estos objetivos, trabajamos con un conjunto de datos que incluye:

-Actividades de Moodle: Registro de actividades, fechas de inicio y finalización, y notas máximas.
-Notas: Calificaciones parciales, finales y recuperaciones.
-Tramesas: Información sobre entregas, evaluaciones e intentos de los estudiantes.

Todos estos datos están disponibles en el archivo ZIP proporcionado por los organizadores del hackathon.
## data_massage.ipynb

### Descripción
Este archivo Jupyter Notebook contiene el proceso de limpieza y preparación de datos para su posterior análisis y modelado. A continuación, se describen los pasos más importantes realizados en el archivo:

>  [!NOTE]
>  Este archivo se encarga de la limpieza y preparación de los datos antes de su análisis y modelado.

### Pasos Importantes

#### Carga de Datos:
- Se cargan los archivos `activitats.csv`, `notes.csv` y `trameses.csv` utilizando pandas.

#### Renombrado de Columnas:
- Se renombra la primera columna de `notes.csv` a `userid` y la primera columna de `trameses.csv` a `tramesa_id`.

#### Filtrado de Datos:
- Se eliminan registros de actividades de ciertas aulas y aquellos que contienen "PROVA", "PRU" o "OCULT" en la columna `activitat`.
- Se eliminan registros donde `activitat` comienza con "exercici".

> [!IMPORTANT]
>  Utiliza `str.contains` y `str.startswith` para filtrar registros de manera eficiente.

#### Manejo de Valores Nulos:
- Se agrupan los datos por `aula_id` y se cuentan los valores nulos en `F_Grade`.
- Se eliminan registros de aulas que no han realizado exámenes y registros sin nota final.

#### Separación de Datos:
- Se separan los datos en dos conjuntos basados en `aula_id` para crear modelos específicos para cada asignatura.

> **Important:** Separar los datos por `aula_id` permite crear modelos más precisos y específicos para cada asignatura.

#### Creación de DataFrames por Aula:
- Se crea un DataFrame por cada `aula_id`, incluyendo notas parciales (`P_Grade`), finales (`F_Grade`), notas de entregas, fechas de entrega y número de evaluaciones.
- Cada DataFrame se guarda en un archivo CSV separado.

## Modelos

### Descripción
Este archivo contiene el código para entrenar modelos de aprendizaje automático utilizando los datos preparados en `data_massage.ipynb`. A continuación, se describen los pasos más importantes realizados en el archivo:

>  [!NOTE]
>  Este archivo se encarga del entrenamiento de modelos de aprendizaje automático y la generación de recomendaciones.

### Pasos Importantes

#### Carga de Datos:
- Se cargan los archivos CSV generados en `data_massage.ipynb`.

#### Procesamiento de Datos:
- Se define la función `procesar_resultado` para leer y procesar los datos, convirtiendo las columnas de fechas a un formato numérico y combinando las características en un DataFrame.

#### Entrenamiento del Modelo:
- Se define la función `obtener_importancia_features` para entrenar un modelo `RandomForestRegressor` y obtener las importancias de las características.
- Se dividen los datos en conjuntos de entrenamiento y prueba, y se escalan las características utilizando `StandardScaler`.

> **Tip:** Escalar las características mejora el rendimiento del modelo de aprendizaje automático.

#### Selección de Características:
- Se seleccionan las características más importantes y se eliminan aquellas que no siguen el modelo de las actividades, como `P_Grade`.

#### Mapeo de Actividades:
- Se cargan los datos de `activitats.csv` y se filtran las actividades no deseadas.
- Se extrae el número de actividad de las características y se mapean a los nombres de las actividades.

>  [!CAUTION]
>  Hay que asegurarse de adaptar los filtrados correctamente dependiendo de el formato. Si quisieramos usar este metodo a una escala general de la UAB hay cambios que se tendrian que ir haciendo

#### Generación de Recomendaciones:
- Se generan recomendaciones de actividades basadas en las características más importantes y se muestran los resultados.

> **Important:** Las recomendaciones se basan en las características más importantes identificadas por el modelo.
