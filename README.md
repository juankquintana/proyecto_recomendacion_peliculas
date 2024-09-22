# proyecto_recomendacion_peliculas

<img src="data/PF.gif" width="700" alt="">

## Contenidos
- [Introducción](#introducción)
- [Data](#data)
- [Contenidos](#contenidos)
- [Alcance](#alcance)
- [Literatura](#literatura)
- [Recomendador](#recomendador)

## Introducción
*¿Qué películas me recomienda un sistema de aprendizaje no supervisado sabiendo que he calificado ciertas películas con un puntaje  entre 1 y 5?*


La clave del éxito de las plataformas de streaming, sobre todo Netflix la precursora de estas, es la capacidad para conocer y adaptarse a las preferencias y gustos de diferentes mercados y audiencias. La inversión que hace Netflix en contenido original ha permitido que el mundo del streaming se haya expandido tanto, pero más que tener un montón de películas para ver sin parar, Netflix sabe en cuáles películas invertir que les genere mayor retorno. Esta pregunta es interesante porque plantea que, al saber qué películas les gustan a los clientes, es posible predecir qué otras películas podrían disfrutar dada su predilección por  las primeras. Este es un problema de agrupamiento, donde buscamos crear clústeres de películas infiriendo que la similitud entre las mismas implica que si a una persona le gustó una película dentro de ese cluster podría también gustarle otra película del mismo y por ello recomendaremos en base a ello.



## Data
Todo lo que se encuentra en la carpeta data:
Contiene las bases de datos originales usadas y unos datos con las transformaciones necesarias para poder hacer el algoritmo recomendador de manera eficiente y autocontenida.
   - *base_usuarios.csv*: Una base de que pelicula vio cada usuario y el rating despues de hacer una limpieza de usuario que no tenian rating a algunas peliculas (sacada a partir de la base ratings_sample.csv)
   - *df_clusters.csv*: Contiene el user id y el cluster al que fue asignado segun el analisis por clusters hecho
   - *df_final.csv*: Es el join entre ratings y metadata para inluir el nombre de la pelicula usado para la recomendacion clusters
   - *df_inner.csv*: Integra los dos csv anteriores en uno, es decir, tiene usuario, ratings, pelicula, cluster usado para la recomendacion por clusters
   - *keywords.csv*: Contiene las palabras clave de la trama de las películas de nuestro conjunto de datos MovieLens. Está disponible en forma de un objeto JSON convertido a cadena.
   - *movies_metada.csv*: El archivo principal de metadatos de películas. Contiene información sobre 45,000 películas incluidas en el conjunto de datos completo de MovieLens. Las características incluyen pósters, fondos, presupuesto, ingresos, fechas de lanzamiento, idiomas, países y compañías de producción.
   - *ratings_sample.csv*: Una parte de la base total de rating que tenia suficientes ratings para varios usuarios para poder realizar el modelo de recomendacion.
   - *ratings_small.csv*: El subconjunto de 100,000 calificaciones de 700 usuarios en 9,000 películas. Una base pequeña de ratings, fue tan pequeña que se decidio no usar y tomar un sample de la base original que es la que se menciono anteriomente.
   - *user_gener_c.csv*: Una base que facilita saber las peliculas que vio cada usuario y a que genero pertenecia (util para recomendar en base a generos en caso de no tener informacion de un usuario pero si el genero que le gusta)
 

## Contenidos
Se puede ver que hay otras dos carpetas en el repositorio:
- **ModelosNLP**
  
Se encuentra todas las pruebas para el modelo de NLP, en este se probo tanto CountVectorizer, TF-IDF y LDA. Finalmente se decidio utilizar CountVectorizer debido a que el modelo de NLP contenia los generos en el analisis y estos debian mantener su peso para asi recomendar peliculas del mismo genero.

Tambien se encuentran dos archivos comprimidos numnpy: cosine_sim_sparse_matrixCOUNT.npz y cosine_sim_sparse_matrixTFIDF.npz, estos son las matrices despues de sacar similitud de coseno tanto para el Count Vectorizer y el TD-IDF Vectorizer respectivamente. Al guardarlas asi es mas facil llamarlas desde el notebook recomendador final.

El ultimo archivo en la carpeta es df_keywords_title.pkl el cual tiene la base usada para el recomendador, esta tiene id de peliculas, titulo original de la pelicula, los keywords originales y las keywords despues de hacer limpieza junto con el genero.

- **OtrosModelos**


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

## Recomendador
Finalmente se define un recomendador 
