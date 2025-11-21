# Proyecto-2-Andres-Perez

Conclusiones del trabajo realizado en kiva_loans

- Hemos podido realizar la importación y uso de diferentes librerías para visualización y manejo de datos
- Hemos podido cargar los datos csv tanto de manera local como desde drive

1- El primer análisis que hemos realizado es que existen columnas con muchos valores nulos, los cuales no aportan información para nuestro estudio, tales como tags, región or partner_id

Después de ver la visualización de los datos faltantes hemos decidido modificar y eliminar las columnas para ello utilizaremos una copia del dataset de original para modificar los datos

Al borrar las columnas el dataset se vuelve mas leíble y fácil de tratar.

2-Una de las cosas mas importantes para la limpieza de datos es tener unos tipos de datos claros, como se observa tanto fecha como otros datos de tipo string vienen como object así que uno de nuestros objetivos será cambiar los tipos de datos a su correspondientes.

3-El siguiente paso será crear una columna dada a una condición, en nuestro caso será si el préstamo fue desembolsado antes o después de la fecha de publicación.

# Creo una columna con la condicion, si se da le dará el valor pre-disbursed y sino post_disbursed
kiva_loans_df["loan_type"] = np.where(
    kiva_loans_df["disbursed_time"] < kiva_loans_df['posted_time'],
    "pre_disbursed",
    "post_disbursed"
)

4- Creamos una nueva columna loan_amount que tendrá el valor micro, small, medium y large, dependiendo de los rangos que hemos establecidos

Para saber que todo está correcto poder utilizar histogramas y diferentes tipos de gráficos para mostrar los datos como por ejemplo:
- histograma - visualización clara que la mayor cantidad de loan amount <2500

- gráfico de barras - visualización de diferentes distribuciones por loan amount/funded_amount/Months/Lender Count
  Visualización de datos discretos y agrupaciones como por ejemplo ver los 10 países con el sum(funded_amount)(el que más philippines)
  Otro ejemplo que hemos hecho ha sido préstamos por sector(predominando agricultura, food, retail)
  O dividir los datos en dos grupos post_disbursed y pre_disbursed, siendo post_disbursed el que mas predomina

- gráfico de líneas
  Creación de una nueva columna month para poder hacer una agrupación de loan_amount(media) por mes
  En la gráfica se puede observar que hay picos en enero, puede ser debido a que la gente es mas generosa o se incita mas a donar en estas               fechas, habiendo bajadas en el resto de meses y una bajada drástica en 2017 cosa que puede ser digna de estudio exhaustivo para ver que pasó

- piechart gráfico circular, viendo la proporción de préstamos por país, en este caso el top 8. Muy importante para ver el % de cada país al total

5- Por último hemos utilizado choropleth map para poder manejar los datos y verlos en un mapa. Viendo de forma visual cada país y la cantidad de loan que han recibido.

6- Hemos realizado el estudio de outliners, dividiendo nuestra información en q y iqr, realizando gráficos de densidad para visualización de los datos.

micro- cantidad mas prestada entorno a 250
small - densidad mas común entre 500-1000, teniendo una descendencia progresiva hasta 2500
médium - densidad mas común entre 2000-3000, bajando gradualmente hasta 6000, apartir de esa cifra baja significativamente la cantidad
large - densidad mas común entorno a 10000, con muy pocas cantidades superiores a esta, viéndose un pico en 50000

Por último hemos podido exportar el nuevo archivo csv tanto en drive como en local.
