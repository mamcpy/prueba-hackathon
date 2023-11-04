# prueba-hackathon
Este repositorio contiene mi prueba técnica

## 1. Introducción
Los conjuntos de datos escogidos son el dataset que contiene información sobre el alquiler de viviendas en Barcelona y el que contiene información sobre la exposición al ruido de la población de Barcelona. Las variables utilizadas para unir los datasets son "Codi_Districte", "Nom_Districte", "Codi_Barri" y "Nom_Barri", puesto que son comunes a ambos datasets.

## 2. Depuración de datos
- Eliminación de la columna año que solo tiene un valor posible y no aporta información.
- Eliminación del valor "Lloguer mitjà per superfície (Euros/m2 mes)" dentro de la variable precio y creación de nueva variable "Àrea (m2)". Para realizarlo se ha observado el histograma y las principales estadísticas sobre la distribución de precios, así como el orden de los elementos y valores NaN.
-  Eliminación de los valores NaN. Estudio de en qué distritos y barrios se encuentran estos valores y eliminación de los elementos en cuyos barrios no hay practicamente documentación sobre el precio del alquiler. Si por el contrario hay otros elementos del mismo barrio con información sobre su alquiler, extrapolar para obtener el valor NaN, realizando una ponderación entre la media del alquiler de su barrio y la media del alquiler de su distrito.
- Conversión de datos de tipo categóricos a categórico para optimizar el uso de memoria.
- Identificación del significado de la columna "Concepte" consultando la web del ayuntamiento de Barcelona.
- Eliminación del % de la columna "Valor" y convertir en float para manipularla con mayor facilidad.
- Extra: Análisis exploratorio de datos (desarrollado en el cuaderno)
- Realización de PCA mediante dos enfoques: aplicado a variables numéricas y aplicado a todo el dataset (justificación desarrollada en el notebook).
- Estandarización de los datos numéricos previa a la PCA mediante StandardScaler (media = 0, varianza = 1) para evitar que algunas variables influyan más que otras en las principales componentes de la PCA.
- OneHotEncoding las variables categóricas para realizar PCA sobre todo el dataset.

## 3. Resultados
- PCA aplicado sobre variables numéricas nos indica que las variables con mayor influencia en la primera componente son área y precio y en la segunda componente es la variable valor.
- PCA sobre todo el dataset nos indica que con 75 componentes principales del total de 203 preservamos el 90% de la varianza explicada.

## 4. Conclusiones
Trabajamos con un dataset balanceado puesto que contamos practicamente con el mismo número de elementos para cada tipo de variable categórica. Esto es un buen indicador que nos facilitará el trabajo si más adelante quisiéramos aplicar modelos de machine learning para predecir alguna variable. Por ejemplo, podríamos intentar predecir el precio de una vivienda en función de su área, el distrito al que pertenece y la población total afectada al ruido en ese barrio.

La población de Barcelona está mucho más expuesta a ruidos de intensidad moderada que a ruidos de media intensidad y muy poca parte lo está a ruidos de alta intensidad. No hay grandes diferencias en la exposición al ruido entre los distritos, sin diferenciar las fuentes del ruido. Para un análisis en mayor profundidad se propone separar las fuentes y analizar las diferencias entre distritos por cada fuente.

En cuanto al análisis de componentes principales, como nuestro objetivo es reducir la dimensionalidad, al aplicarlo sobre las variables numéricas podemos deshacernos de la tercera componente principal y mantener el 90% de la varianza explicada. En el caso de todo el dataset, podemos eliminar el 128 dimensiones y mantener solo los 75 componentes principales, que guardan el alrededor del 90% de la varianza.
