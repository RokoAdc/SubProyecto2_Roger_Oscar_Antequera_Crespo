# SubProyecto2_Roger_Oscar_Antequera_Crespo

# NLP - Clasificación Automática de Tickets

## Índice

- [Descripcion del Problema](#Descripcion del Problema)
- [Setup e Importacion de Librerias](#Setup e Importacion de Librerias)
- [Data Loading](#Data Loading)
- [Data Visualization](## Data Visualization)
- [Prepare the text for topic modeling](#Prepare the text for topic modeling)
- [Feature Extraction](#Feature Extraction)
- [Manual Topic Modeling](#Manual Topic Modeling)
- [Supervised model to predict any new complaints to the relevant Topics](#Supervised model to predict any new complaints to the relevant Topics.)
- [Model training and evaluation](#Model training and evaluation)
- [Decision de Mejor Modelo](#Decision de Mejor Modelo)

## Descripcion del Problema

Crear un modelo que pueda clasificar las quejas (complaints) de los clientes en función de los productos/servicios. Al hacerlo, segregar estos tickets en sus categorías relevantes y, por lo tanto, ayudar en la resolución rápida del problema.

Se realizo el modelado de temas en los datos .json proporcionados por la empresa. Dado que estos datos no están etiquetados, se aplico NMF para analizar patrones y clasificar los tickets en los siguientes cinco grupos según sus productos/servicios:

Tarjetas de Credito / Tarjetas Prepagadas (Credit card / Prepaid Card)

Servicios de Cuentas de Banco (Bank account services)

Reportes de Robos (Theft/Dispute reporting)

Prestamos Hipotecarios y Otros Prestamos (Mortgages/loans)

Otros

Con la ayuda del modelado de temas, se asigno cada ticket a su respectivo departamento/categoría. Luego se usaron los datos para entrenar cualquier modelo supervisado, como regresión logística, árbol de decisión o bosque aleatorio. Usando este modelo entrenado, se pudo clasificar cualquier nuevo ticket de soporte de quejas de clientes en su departamento correspondiente.

## Setup e Importacion de Librerias

En este punto extraemos todas las librerias necesarias del proyecto entre las cuales encontramos las mas importantes para NLP:

1. NLTK
2. panda
3. numpy
4. sklearn


Este proyecto necesita que Anaconda esté instalado en la computadora.

Para más detalles sobre la instalación, visite: https://docs.anaconda.com/anaconda/install/index.html


## Data Loading

Dentro de este punto debemos extraer el archivo JSON "complaints.json" y posteriormente se debe transformar en un Dataframe para poder analizar la informacion
Tomar en cuenta que este Archivo JSON es anidado por lo que se debe normalizar.

## Data Visualization

Dentro de la informacion que obtuvimos podemos ver las siguientes caracteristicas:

1. Encontramos valores numericos y categoricos
2. Encontramos valores NULL
3. Las columnas contienen una barra baja "_" la cual se debe eliminar ademas de la palabra "source" dentro de los datros anidados
4. Contamos con 21072 registros con un total de 22 variables
5. La columna en la cual se debe prestar atencion es "complaint_what_happened"

## Prepare the text for topic modeling

En este punto trataremos la informacion y acontinuacion se hace un resumen de los procesos realizados:

* Cambiamos los nombres de las columnas eliminando "_" y "source"
* Modificamos campos vacios por valores NaN
* Eliminamos valores NULL
* Enfoque en la columna "complaint_what_happened"
* Modificamos el texto a minusculas
* Removemos la puntuacion
* Modificamos el texto que tebnga numeros dentro sus palabras
* Lematizamos mediante WorNet posterior a la tokenizacion
* Eliminamos los tags POS
* Visualizamos la columna "complaint_what_happened" aplicando el lenght
* A traves de WordCloud exploramos la variable ya mencionada e identificamos dentro del texto las 40 palabras mas utilizadas
* Identificamos los unigramas, bigramas y trigramas
* Eliminamos el texto xxxx del cuerpo del texto

## Feature Extraction

Para poder modelizar y sacar los topicos debemos vectorizar nuestra informacion
Para tal objetivo convertimos en este paso la matriz con caracteristicas TF-IDF con un max_df de 95% y un min_df de 2

Posteriormente utilizamos NMF

Non-Negative Matrix Factorization (NMF) es una técnica no supervisada, por lo que no hay etiquetas de temas en los que se entrenará el modelo. La forma en que funciona es que NMF descompone (o factoriza) vectores de alta dimensión en una representación de menor dimensión. Estos vectores de menor dimensión no son negativos, lo que también significa que sus coeficientes no son negativos.

En esta tarea realizamos lo siguiente:

Find the best number of clusters
Apply the best number to create word clusters
Inspect & validate the correction of each cluster wrt the complaints
Correct the labels if needed
Map the clusters to topics/cluster names

## Manual Topic Modeling

Adoptamos el enfoque de prueba y error para encontrar la mejor cantidad de topicos para el modelo NMF.

El único parámetro que se requiere es el número de componentes, es decir, el número de topicos que queremos. Este es el paso más crucial en todo el proceso de modelado de topicos y afectará en gran medida la calidad de sus topicos finales.

## Supervised model to predict any new complaints to the relevant Topics
Hasta ahora se ha creado el modelo para crear los temas para cada queja. Entonces, en la siguiente sección, se utilizaran para clasificar cualquier queja nueva.
Dado que utilizará la técnica de aprendizaje supervisado, tenemos que convertir los nombres de los temas en números (las matrices numpy solo entienden los números)

## Model training and evaluation

Se aplicaron 3 modelos para detectar cual de estos es el mejor segun los datos que tenemos :

Logistic regression
Decision Tree
Random Forest

## Decision de Mejor Modelo

Como se puede observar obtenemos los siguientes Scores dentro de los 3 modelos utilizados

LogisticRegression: 95% DecissionTree: 84% Random Forest: 87%

Por lo que el mejor modelo que se puede aplicar entre los 3 es Logistic Regression






