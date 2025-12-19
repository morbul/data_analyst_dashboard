# Analisis top 2000 series de TV (TMDB)

## Objetivo del proyecto
Identificar si existe una tendencia en los géneros de las series mejor evaluadas por la audiencia históricamente y si existen grupos de series que desempeñan mejor. De esta manera, se pueden recomendar ciertos grupos de series los cuales serían ideales para partir con una nueva plataforma de streaming.

## Dataset utilizado 

* **Dataset Original:** [`top_rated_2000webseries.csv`](https://github.com/morbul/data_analyst_dashboard/blob/main/top_rated_2000webseries.csv) - Contiene los datos crudos extraídos de la fuente original sin modificaciones.
* **Dataset Procesado:** [`tv_series_clean.csv`](https://github.com/morbul/data_analyst_dashboard/blob/main/tv_series_clean.csv) - Es el resultado de la limpieza realizada en Python, el cual incluye la columna `primary_genre` y es el archivo que alimenta directamente el panel de Power BI.

## Preguntas (KPIS) 

* ¿Qué países producen mejores series?.
* ¿Existe un cambio en la proporción de los géneros de las series mejor evaluadas en los últimos años?
* Si deseo partir solo con un género en específico, ¿hay alguno que destaque sobre los demás?

## Proceso de limpieza y transformación de los datos
Este proceso fue realizado en Python
1. Identificación y manejo de valores nulos: De la totalidad de los registros, solo faltaban 21 datos; 20 de estos corresponden a la descripción de las series y el restante a un país de origen para un registro.
2. Normalización de géneros: Dado que cada serie puede tener múltiples géneros, se establece un algoritmo de jerarquía de géneros para determinar un género principal para cada una de las series analizadas. Esto se establece a través de la frecuencia de estos géneros de esta manera, el género principal queda de la forma: Kids > Animation > Family > Sci-Fi & Fantasy > Comedy > Crime > Drama.
   2.1 Aquellos valores que no se encuentran en los mencionado en el punto 2 se clasifican como "other".


## Dashboard 
[Ver Dashboard en Tiempo Real](https://app.powerbi.com/view?r=eyJrIjoiNWZkODYzMDAtM2RiOC00NGM1LWJmOWEtZmJjM2YzN2FjYjZkIiwidCI6IjM2YjZkNDEzLTNiNmYtNDgxYS1iYzlkLTY2ODliNTExY2FmYSIsImMiOjR9)
---
![Requerimientos del Desafío](pbi_req.png)

## Insights del proyecto
* EE.UU., Japón, Corea y países de habla hispana lideran la producción de las mejores series de televisión.
* La distribución de géneros en los últimos años se ha mantenido relativamente constante en un horizonte de 10 a 20 años.
* La animación es el género que obtiene la mayor valoración a lo largo del tiempo.

## Conclusion
Si el objetivo es incursionar en plataformas de streaming para series, el grupo objetivo de mayor tamaño sería el de series de animación, tanto de producción estadounidense como asiática (Japón, Corea). También existe una gran presencia de series de habla hispana, pero el primer grupo es 7 veces más grande, por lo cual sería un mercado al cual apuntar en un primer modelo de negocio.
