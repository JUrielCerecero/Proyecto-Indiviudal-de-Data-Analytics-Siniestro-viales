# Proyecto Indiviudal de Data Analytics Siniestro viales
 
 ## Introducción
El Observatorio de Movilidad y Seguridad Vial (OMSV), centro de estudios que se encuentra bajo la órbita de la Secretaría de Transporte del Gobierno de la Ciudad Autónoma de Buenos Aires, nos solicita la elaboración de un proyecto de anális de datos, con el fin de generar información que le permita a las autoridades locales tomar medidas para disminuir la cantidad de víctimas fatales de los siniestros viales. Para ello, nos disponibilizan un dataset sobre homicidios en siniestros viales acaecidos en la Ciudad de Buenos Aires durante el periodo 2016-2021. Este dataset [homicidios.xlsx](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/Datasets/homicidios.xlsx) se encuentra en formato xlsx y contiene dos hojas llamadas: hechos y víctimas. Asimismo, observarán que incluye otras dos hojas adicionales de diccionarios de datos, que les podrá servir de guía para un mayor entendimiento de la data compartida.

## ETL
- Enlace:[ETL.ipynb](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/ETL.ipynb)

Se hizo una limpieza de la hoja de hechos y vçitimas por separado.
Se quitaron duplicados, se seleccionaron columnas que contuvieran información relevante para el análisis o que nos aportaron algún dato útil en algún punto.

Los valores que venían por default con SD se checó si se podían tomar de alguna columna como en algunos casos se puedieron sacar de la columna LUGAR DEL HECHO, en las coordenadas si no había alguna se tomaba como referencia la coordenada de la comuna perteneciete y se pusó solo como un punto de referencia, no como un valor exacto.

Los cruces faltantes o alturas se sacaron de lugar del hecho.

De la hoja víctimas  se hizo el mismo proeceso de duplicados, nulos, valores anormales.

Al final se hizo la unión de las dos tablas, y si había algún valor nulo porque faltaba en una de las hojas al hacer la unión se le puso como valor Sd.

Se cambiaron los valores de Sd por NA para facilitar el proceso de graficar en el EDA.

También se realizó una tabla con el conteo de víctimas agrupado por comuna y con webscrapping se obtuvo el dato de las coordenadas de referencia de las 15 comunas, todo esto para hacer una gráfica de mapa en el Dashboard.


## EDA
- Enlace: [EDA.ipynb](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/EDA.ipynb)

Primero encontramos una visualización general del total de datos del datset a trabajar con los nulos de cada columna:

# Outliers

Se buscaron outliers en las columnas Edad, Días de muerte post accidente y No víctimas, pero no se encontraron valores atípicos, todos estaban dentro de rangos normales para cada tipo de dato.

![outliers edad](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/outlier%edad.png)

![outliers dias muerte](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/outliers%dias%muerte.png)

![outliers no victimas](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/outliers%no%victimas.png)

### Fecha
Se analizaron la columna de fechas con el año, para visualizar los accidnetes por año, donde podemos observar que el año con más accidentes fué el 2018, despúes vimos una disminución drástica para lo siguientes años, esto puede deberse a que a principios de 2020 se expandió a nivel mundial la pandemia del COVID 19, lo cual repercutió en que la gente se aislará en sus casa el primer año de pandemia, y en los años posteriores empezó a disminuir este aislamiento.

![grafica 1](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%201.png)


### Rol de la víctima en el medio de transporte que ocupaba
Dentro de la columna rol nos indica cual era el rol en el medio de transporte qe ocupaba la persona que murió a causa del accidente, donde observamos que encabezan el conductor como las personas que más tienden a fallecer al momento de un acciendte dominando con un 46.1% del total, seguido por los peatones con un 37.2%, se suamn los pasajeros acompañantes con un 11.2% y siguen los ciclistas con un 4.1%, cabe destacar que en la mayoría de caso que ocurre un accidente donde involucra un ciclista, la víctima suele ser el ciclista cuando también está involucrado un automóvil. del total de datos, desconocemos el rol del 1.5% del total de datos.

![grafica 2](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%202.png)

### Víctima
Aqui podemos notar que los medios de transporte que más predominan son las motocicletas seguido de los peatones, dando a entender que cualquier persona que sufra un accidnete donde sea la víctima y vaya en este medio de transporte es más propenso a morir, dado a que se esta más expuesto a sufrir lesiones graves al no portar con medidas mas reforzadas de seguridad comparado con un vehículo

![grafica 3](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%203.png)

### Sexo
Aquí observamos que la mayoría de casos con un 76% predominan los hombres, y un 23.2% las mujeres, 0.8% se desconoce su sexo.

![grafica 4](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%204.png)

### Días de muerte post accidente
Aqui podemos observar que el 69.9% de las muertes sucedieron el mismo día del accidente, desconocemos cuanto tiempo pasó después del accidente hasta la hora de su muerte, el 20.9% murierondías después del accidente y desconocemos el 9.5% de los casos registrados.
El hecho que 69.9% murieran el mismo día nos puede dar un indicio de que los accientes fueron de índole grave, reduciendo drásticamete la posibilidad de que sobrevivieran.

![grafica 5](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%205.png)

### Edades de los muertos
Del total de accidentes solo tenemos el 93.2% registrados por edad, de esos registros se tiene que el grupo donde hubo más muertes fue el que se encuentra en el rango de edad de 20 a 39 años, seguiod del rango de 40 a 57 años

![grafica 6](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%206.png)

### Número de víctimas
En el siguiente gráfico observamos que en la mayor parte de accidentes con el 94.3% fueron de 1 víctima, lo caul es relativamente alentador, considerando que en la mayor parte de muertes por accidentes viales si llega a haber una defunción 1 persona es la que llega  a morir, y en menor proporción dos o más personas, sin quitar de vista el objetivo de reducir en cualquier aspecto los accidentes viales.

![grafica 7](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%207.png)

### Hora del suceso
En la siguiente gráfica tenemos contabilizados el rango de horario en el que sucedieron los accidentes, donde durante el día que se considera una franja horaria de 6 hrs. a 18 hrs.y la noche de 19 hrs. a 5 hrs. se puedes observar que al haber una mayor cantidad de gente transitando en el día vemos mayor cantidad de accidetes que en la noche, aunque la difenrecia no estan tan grande entre una y otra categoría

![grafica 8](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%208.png)

### Tipo de calle
En este gráfico observamos que en donde ocurren mas accidentes mortales son las avenidas, y las calles y autopistas estpan en menor rango pero con valores similares. 

![grafica 9](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%209.png)

### Comuna
En la siguiente gráfica podemos observar la frecuencia por comuna donde los accidentes sucedieron.

![grafica 10](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%2010.png)


### Acusado
En esta gráfica encontramos que los acusados de causar el accidente encabezan con más frecuencia los autos, seguidos de las motos, y en tercer puesto los transportes de carga.

![grafica 11](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%2011.png)

### Determinación de cruce o altura del incidente
Según la ubicación de donde fue el incidente, se encuentra que la mayoría de muertes se han dado en los accidentes sucedidos en los cruces con un 75.5 % de frecuencia, dándonos a notar que en los cruces donde mayor atención se debe poner para tomar medidas para disminuir estos sucesos. 

![grafica 12](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%2012.png)

### Correalción de variables numéricas
Se verifica con una gráfica de correlaciones para ver si existe algún patrón respecto a las variables númericas entre ellas, pero se observa que no hay una causalidad entre una u otra, son variables independientes entre si.

![grafica correlación](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/correlacion.png)

## Víctimas por año

En este gráfico vemos representada la relación de muertes por año, donde del año 2016 a 2018 se veía un aumento en los incidentes con muertes, y de 2019 a 2021 hubo una tendencia a la baja esto correspondiente a la aparaición del COVID-19 y el aislamiento que hubo a nivel mundial, sin embargo en el 2021 aumentó conforme fueron quitando restricciones, lo cual nos indica que debe haber una mayor atención a dismiuir esta clase de incidentes, no solo que deriven en defunciones, sino cualquiere acciednete vial, donde se arriesgue la vida de cualquier persona.

![grafica 13](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%2013.png)

### Tipo de transporte y sexo
Aqui podemos ver la relación entre el tipo de transporte de las víctimas, el número de víctimas y si eran hombres o mujeres, donde en la categoría de auto, moto y bicicleta predominan los hombres, en peatón vemos que la relación se mueve un poco hacia el centro, sin dejar la tendencia a prevalecer los hombres, esto es correspondiente a la relacion global entre hombres y mujeres registrados, donde vemos una diferencia en proporciones es en los transportes de cargas, donde solo existen hombres, donde es un rubro que regularmente son los hombres los que manejan este tipo de vehículo,  y donde en menor escale vemos mas paridad es en el transporte de pasajeros, donde aunque en pequeña escala vemos una proporción similar entre los dos géneros registrados.

![grafica 14](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%2014.png)

### Relación entre tipo de calle, cruce o altura, acusado y número de víctimas
Aquí podemos ver los diferentes tipo de accidentes que han sucedido, relacionándolos por tipo de calle, y si fue un cruce de calles o Altura si fue en medio de dos esquina sobre alguna vialidad, donde en las avenidas y cruces es donde suceden más accidentes, y los cuales, los 3 acusados en mayor proporción son los autos, pasajeros  de algun transporte público y fueron lesionados, y los transportes de carga.

![grafica 15](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%2015.png)


### Relación víctima-Acusado y número de víctimas
Aquí tenemos un conteo, donde se divide por número de víctimas, el medio de transporte del acusado y de la víctima, donde podemos observar que en la mayor parte de grupos de victimas, el acusado es en mayor parte un auto, al igual que los transportes de carga y los pasajeros de trnasportes. las motos junto a los petones son de los que mas accidentes mortales sufren.

![grafica 16](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%2016.png)

### Relación víctima-Sexo
Aquí estamos analizando que relación hay entre el medio de trnasporte que utilizaban las víctimas y su género registrado, donde vemos que las mujeres peatones fueron más propensas a sufrir siniestros viales mortales, en comparación con los hombres que predominan más las víctimas en moto, pero en el caso de los hombres la proporción de peatones es mayor que en la de mujeres. También generalizando se puede decir que los hombres fueron más propenso a sufrir accidentes letales, en comparación de las mujeres.

![grafica 17](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/im%C3%A1genes/grafica%2017.png)


## Dashboard
- Enlace [Dashboard.pbix](https://github.com/JUrielCerecero/Proyecto-Indiviudal-de-Data-Analytics-Siniestro-viales/blob/main/Dashboard.pbix)
En el Dahsboard se edesarrollan 3 tipos de analisis de diferentes puntos de vista, uno por temporalidad, uno categórico y uno geográfico, donde en cada uno se abrodan difernetes puntos de vista, dandónos diferentes panormas de todos los datos, interaxtuando con varios parámetros que nos ayudan a hacer algunos descubirmientos ocultos entre los datos.

Aquí se puede acceder al Dashboard ya publicado:  [link]



## KPI'S

- Enlace: [KPI'S.ipynb]()

Se realizaron 3 kpis, cada uno pididendo evaluar el cumplimiento de un ojetivo para un cierto perido de tiempo, donde se hizo un analisis de cada kpi con los datos que se tenían de los años 2016 a 2021. 
 
# KPI #1

Reducir en un 10% la tasa de homicidios en siniestros viales de los últimos seis meses, en CABA, en comparación con la tasa de homicidios en siniestros viales del semestre anterior.

Definimos a la tasa de homicidios en siniestros viales como el número de víctimas fatales en accidentes de tránsito por cada 100,000 habitantes en un área geográfica durante un período de tiempo específico. Su fórmula es: (Número de homicidios en siniestros viales / Población total) * 100,000

Según el útlimo censo, la población de Buenos Aires para el año 2022 fue de 3,120,612 personas, al no haber datosdel año 2021, se toma este año como referencia.

### Aqui podemos ver graficado, donde vamos evaluando semestre por semestre la tasa y la meta de la tasa, donde solo en el primr semestre del año 2017, los dos semestres del año 2019, el primer semestre del 2020 y el segundo semestre del 2021 se cumlió el objetivo, que era reducir la tasa de homicidios de un semestre a otro en un 10% para la Ciudad de Buenos Aires 

grafica

# KPI 2

Reducir en un 7% la cantidad de accidentes mortales de motociclistas en el último año, en CABA, respecto al año anterior.

Definimos a la cantidad de accidentes mortales de motociclistas en siniestros viales como el número absoluto de accidentes fatales en los que estuvieron involucradas víctimas que viajaban en moto en un determinado periodo temporal. Su fórmula para medir la evolución de los accidentes mortales con víctimas en moto es: (Número de accidentes mortales con víctimas en moto en el año anterior - Número de accidentes mortales con víctimas en moto en el año actual) / (Número de accidentes mortales con víctimas en moto en el año anterior) * 100

### Aquí podemos observar una gráfica con la variación año con año, donde se ve el aumento o disminución del % de cada año con su respectivo año anterior,  en donde vemos que para el año 2017, 2019 y 2020 se cumplió el objetivo, dandonos a entender que se tiene que hacer mas esfuerzos en materia de concientización en conductores de motocicletas sobre la preacaución y mesura al manejar motocicletas, y el siempre estar alerta de otros conductores que puedan causar accidentes, y el hacer enfásis en siempre usar equipo de protección y que sea de calidad.

grafica

# KPI 3

Aquí se plantea reducir el procentaje de muertes por siniestros viales para las personas en un rango de edad de 18 a 35 años en un 10% por año,  ya que representa el grupo con mayor presencia en los registros.

### Para la siguiente gráfica tenemos la diferencia en porcentajes que hubo año contra año anterior, donde para los años 2019 fue cuando se cumplió este objetivo, si embargo esto esta ampliamente relacioado con la pandemia del COVID 19 donde hubo un aislamiento a nivel mundial y se redujo drasticamente la cantidad de personas que salían de sus casa por un largo tiempo.

grafica

## Conclusiones

- Antes de Pandemia los siniestro viales fatales iban en aumento,  solo en el año 2019 se lo reducir estos sin estar relacionado con algún factor externo, en 2020 disminuyeron a su punto mínimo probablemente porque este fue el año donde la pandemia se extendió en todo el mundo. después empezó a repuntar.


- Los hombres son más propensos a fallecer en siniestro fatales, sobre todo cuando manejan motocicletas,  seguido de los peatones, y en tercer lugar los que manejan automóviles.


- Las mujeres suelen fallecer a causa de siniestros viales principalmente cuando van como peatones.


- Entre más aumentan los rangos de edades, la gente es más propensa a morir como peatones por causa de un siniestro vial.


- Los siniestros viales que más prevalecen ocurren en los cruces de avenidas donde la mayoría fallece el mismo día del accidente, se desconoce si murieron al momento del siniestro u horas después del accidente.

- Los conductores de cualquier vehículo son los que más tienden a perder la vida en siniestros viales fatales.

- Los motociclistas son los que más pierden la vida en un siniestro vial fatal, lo que debería de alertarlos a tomar más precauciones al conducir, usar equipo de protección personal.

- Las personas en un rango de 18 a 35 años de edad son las que más mueren en siniestros viales fatales.

- La comuna 1 encabeza la lista de más siniestros viales fatlaes, deguod de la 4 y la 9.

- Los automóviles encabezan el grupo que más fue acusado de causar el siniestro vial.

- En un 75.5% de los casos, los siniestros viales fatales sucedieron en cruces de vialidades.

- Los autos y los trasnportes de carga son los que más fueron acusados de causar los siniestros viales donde la víctima fue una motocicleta
