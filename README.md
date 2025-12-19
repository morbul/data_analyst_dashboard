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
1. Identificación y manejo de valores nulos: De la totalidad de los registros, solo faltaban 21 datos; 20 de estos corresponden a la descripción de las series y el restante a un país de origen para un registro, ninguno de estos registros es eliminado lass descripciones faltantes no son datos relevantes para el analisis realizado, el pais que falta se imputa manualmente con el correspondiente.
2. Normalización de géneros: Dado que cada serie puede tener múltiples géneros, se establece un algoritmo de jerarquía de géneros para determinar un género principal para cada una de las series analizadas. Esto se establece a través de la frecuencia de estos géneros de esta manera, el género principal queda de la forma: Kids > Animation > Family > Sci-Fi & Fantasy > Comedy > Crime > Drama. Aquellos valores que no se encuentran en los mencionado en el punto 2 se clasifican como "other".
```python
priority_list = ['Kids', 'Animation', 'Family', 'Sci-Fi & Fantasy', 'Comedy', 'Crime', 'Drama'].
```
4. Eliminación duplicados: Se realizó una limpieza de seguridad eliminando registros repetidos mediante la columna id para asegurar que cada serie sea contabilizada una sola vez.
5. Generación dataset final: Tras la limpieza, el dataset consolidado ([`tv_series_clean.csv`](https://github.com/morbul/data_analyst_dashboard/blob/main/tv_series_clean.csv)) cuenta con 1.999 registros de los 2.000 iniciales, garantizando una base de datos íntegra y optimizada para el Dashboard.


## Dashboard 
[Ver Dashboard en Tiempo Real](https://app.powerbi.com/view?r=eyJrIjoiNWZkODYzMDAtM2RiOC00NGM1LWJmOWEtZmJjM2YzN2FjYjZkIiwidCI6IjM2YjZkNDEzLTNiNmYtNDgxYS1iYzlkLTY2ODliNTExY2FmYSIsImMiOjR9)
---
Resumen Ejecutivo (KPI Cards): Se ubicaron métricas globales (Puntaje, Votos y Popularidad) en la parte superior para dar contexto inmediato antes de entrar al detalle visual.
Filtros Dinámicos: El uso de segmentadores por Año y Trimestre (Q1-Q4) permite al usuario realizar una segmentación temporal, facilitando el análisis de estacionalidad o tendencias específicas por periodos cortos.
Treemap de Países (Cantidad por País): Se eligió este visual para representar la distribución geográfica debido a la alta disparidad de volúmenes entre países. Permite visualizar rápidamente que paises dominan el mercado.
Gráfico de Líneas (Promedio de rating por Año y Género): Utilizado para identificar la consistencia de calidad. Las líneas permiten comparar cómo géneros específicos (como Animation o Comedy) mantienen valoraciones superiores a lo largo del tiempo frente a otros más volátiles.
Gráfico de Barras 100% Apiladas (Recuento por Año y Género): Al normalizar las barras al 100%, se puede observar el porcentaje de mercado relativo de cada género por año, eliminando el ruido que genera el crecimiento total del volumen de series y enfocándose en la relevancia de cada categoría.
![Requerimientos del Desafío](pbi_req.png)

## Insights del proyecto
* EE.UU., Japón, Corea y países de habla hispana lideran la producción de las mejores series de televisión.
* La distribución de géneros en los últimos años se ha mantenido relativamente constante en un horizonte de 10 a 20 años.
* La animación es el género que obtiene la mayor valoración a lo largo del tiempo.

## Conclusión
Si el objetivo es incursionar en plataformas de streaming para series, el grupo objetivo de mayor tamaño sería el de series de animación, tanto de producción estadounidense como asiática (Japón, Corea). También existe una gran presencia de series de habla hispana, pero el primer grupo es 7 veces más grande, por lo cual sería un mercado al cual apuntar en un primer modelo de negocio.
