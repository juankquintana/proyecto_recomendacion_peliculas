# proyecto_recomendacion_peliculas

<img src="data/PF.gif" width="700" alt="">

## Contenidos
- [Introducción](#introducción)
- [Data](#Data)
- [Alcance](#Alcance)
- [Literatura](#Literatura)

## Introducción
*¿Qué películas me recomienda un sistema de aprendizaje no supervisado sabiendo que he calificado ciertas películas con un puntaje  entre 1 y 5?*


La clave del éxito de las plataformas de streaming, sobre todo Netflix la precursora de estas, es la capacidad para conocer y adaptarse a las preferencias y gustos de diferentes mercados y audiencias. La inversión que hace Netflix en contenido original ha permitido que el mundo del streaming se haya expandido tanto, pero más que tener un montón de películas para ver sin parar, Netflix sabe en cuáles películas invertir que les genere mayor retorno. Esta pregunta es interesante porque plantea que, al saber qué películas les gustan a los clientes, es posible predecir qué otras películas podrían disfrutar dada su predilección por  las primeras. Este es un problema de agrupamiento, donde buscamos crear clústeres de películas infiriendo que la similitud entre las mismas implica que si a una persona le gustó una película dentro de ese cluster podría también gustarle otra película del mismo y por ello recomendaremos en base a ello.



## Data
Se encuentran los datos en formato CSV:

movies_metadata.csv: El archivo principal de metadatos de películas. Contiene información sobre 45,000 películas incluidas en el conjunto de datos completo de MovieLens. Las características incluyen pósters, fondos, presupuesto, ingresos, fechas de lanzamiento, idiomas, países y compañías de producción.

keywords.csv: Contiene las palabras clave de la trama de las películas de nuestro conjunto de datos MovieLens. Está disponible en forma de un objeto JSON convertido a cadena.

ratings_small.csv: El subconjunto de 100,000 calificaciones de 700 usuarios en 9,000 películas.
 

## Alcance
El alcance inicial definido será un clustering primero usando PCA para determinar las dimensiones más relevantes de las que esta compuestos los datos, aunque inicialmente ya se pudo ver unas variables bastante interesantes que habrá que codificar pues son en su mayoría categóricas para después pasar a usar clustering y determinar grupos de personas o películas que se parecen y recomendarle a las personas según sus calificaciones de otras películas que han visto.

## Literatura
Los sistemas de recomendación (Recommender Systems) son aplicaciones que ofrecen a los usuarios recomendaciones personalizadas de productos y servicios que aún no han adquirido, basadas en sus intereses, con el objeto de incrementar las ventas y mantener la base de clientes satisfecha. Estos sistemas son ampliamente usados en diversas áreas como en plataformas de streaming, redes sociales, planeación de viajes, recomendaciones de música, colocación laboral entre otras [1]

Amazon patentó su primera versión de su sistema de recomendación alrededor del 2004. Esta trajo consigo un incremento del 29% en las ganancias alcanzando los US$12.83 billones en el segundo trimestre fiscal, mientras que Netflix implementó esta herramienta en su aplicación para disminuir el número de suscripciones canceladas y al mismo tiempo aumentar el tiempo promedio que los usuarios interactúan con la aplicación.  [2]

Estos sistemas fueron desarrollados para hacer sugerencias con  base en las preferencias de los usuarios:  su  género favorito, actores, directores, entre otros parámetros,  por ejemplo el sistema de Netflix también agrega una explicación que ayuda al usuario entender por qué esa película esta siendo recomendada,  ayudando a incrementar la credibilidad de la aplicación y la lealtad del usuario. Otro enfoque es la propuesta de películas basada en emociones por ejemplo felicidad, enojo o tristeza.[2]

En el área de diseño e implementación de sistemas de recomendación actualmente existen 4 enfoques: [2]

Sistemas de recomendación basado en contenido
Sistemas de recomendación basado en filtrado colaborativo
Sistemas de recomendación basado en conocimiento
Sistemas de recomendación híbrido

* Profundizaremos en estos enfoques a medida que avancemos en el desarrollo del curso y el proyecto




