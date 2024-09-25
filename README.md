# proyecto_recomendacion_peliculas

<img src="data/PF.gif" width="700" alt="">

## Contenidos
- [Introducción](#introducción)
- [Data](#data)
- [Contenidos](#contenidos)
- [Alcance](#alcance)
- [Literatura](#literatura)
- [Recomendador](#recomendador)

## Video
https://www.youtube.com/watch?v=3wKMVMFvhZM&t=1s

## Resumen
Todos los servicios por suscripción masivos compiten por mantener y atraer a usuarios que cada vez tienen más opciones para escoger. Aún cuando creemos que este negocio ya está completamente inventado, ¿cuántas veces nos sorprendemos por las recomendaciones que recibimos de estos servicios? 
El propósito de este trabajo es explorar las preferencias de los usuarios de una plataforma de películas y tratar de encontrar oportunidades que conduzcan a recomendaciones de contenido curadas y acertadas para ellos. 
El trabajo presenta varios desafíos:  no contamos con información sobre las características de los usuarios y debemos inferir relaciones entre ellos a través de los ratings que los mismos han dado a las películas.  Existe una gran dimensionalidad en los datos lo que dificulta su manejo y; no somos expertos en este negocio por lo cual se nos dificulta la evaluación de los resultados de los modelos.

Las bases de datos utilizadas corresponden a MovieLens,  un grupo de investigación del Departamento de Ingeniería y Ciencias Computacionales de la  Universidad de Minnesota. 

Luego de tomar una muestra de los datos y limpiarlos se probaron distintos modelos para la creación de un recomendador de películas con las siguientes características: 
- Se utilizan los promedios de ratings ponderados por género para recomendar películas a usuarios nuevos.
- De lo contrario se combina el método de filtrado colaborativo utilizando  descomposición en valores singulares y el método de filtrado en base a contenidos utilizando Natural Language processing (NLP) para identificar películas similares. 


## Introducción
*¿Qué películas me recomienda un sistema basado en técnicas de aprendizaje no supervisado basado en información previa como el puntaje  entre 1 y 5 de los usuarios?*


La clave del éxito de las plataformas de streaming, sobre todo Netflix la precursora de estas, es la capacidad para conocer y adaptarse a las preferencias y gustos de diferentes mercados y audiencias. La inversión que hace Netflix en contenido original ha permitido que el mundo del streaming se haya expandido tanto, pero más que tener un montón de películas para ver sin parar, Netflix sabe en cuáles películas invertir que les genere mayor retorno. Esta pregunta es interesante porque plantea que, al saber qué películas les gustan a los clientes, es posible predecir qué otras películas podrían disfrutar dada su predilección por  las primeras. Este es un problema de agrupamiento, donde buscamos crear clústeres de películas infiriendo que la similitud entre las mismas implica que si a una persona le gustó una película dentro de ese cluster podría también gustarle otra película del mismo y por ello recomendaremos en base a ello.

El problema a resolver es de gran pertinencia. Vivimos en la era del consumo digital y estamos en el medio del auge del uso de datos de los usuarios para anticiparse a sus necesidades, lo que se conoce comúnmente como análisis predictivo o personalización predictiva. 

El cliente potencial de esta solución puede ser cualquier servicio de subscripción de contenidos en su búsqueda por atraer y retener a sus clientes ofreciendo buenas recomendaciones que mantengan a los usuarios involucrados con el servicio.  Al mismo tiempo la solución podría aplicarse a otro contexto donde los usuarios califiquen un producto o servicio y donde se encuentre distintas categorías de los mismos. 
Este tipo de servicios de recomendación puede resultar clave a la hora de adquirir ventaja competitiva frente a otras compañías y alcanzar los ingresos esperados como empresa. 

En este caso puntual la pregunta es: ¿Qué películas me recomienda un sistema de aprendizaje no supervisado sabiendo que he calificado ciertas películas con un puntaje  entre 1 y 5?
La pregunta es sumamente interesante puesto que  al mismo tiempo es relevante evaluar de qué forma la podemos responder siendo eficientes en el uso de los recursos y siendo efectivos en cuanto a los resultados generados. También es importante considerar distintas alternativas de recomendación según si el usuario es nuevo en la plataforma o no, y poder siempre recomendarle una lista de películas. 
Para abordar esta pregunta decidimos probar algunos de los modelos estudiados en el curso ya que los mismos representan los enfoques tradicionales en el ámbito del aprendizaje no supervisado. 
Los mismos serán explicados con mayor detalle en el siguiente punto así como los resultados principales y las limitaciones encontradas.  



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
- **Analisis Visualizaciones Iniciales**
Se tiene el notebook AnalisisVisualizacionesIniciales.ipynb el cual tiene las visualizaciones iniciales de las bases de datos y graficas que ayudaron a entender inicialmente los datos y que fueron usadas para poner en la presentacion y el documento final.

- **Recomendadores**
Se tiene el notebook Recomendadores.ipynb que toma todos los modelos creados y hace el recomendador final que tiene en cuenta SVD y NLP para recomendar 5 peliculas en cada una y si un usuario no existe toma los generos mas populares dado su genero favorito. Para esto se cargan todas las matrices y funciones creadas tanto por *ModelosNLP* y *otrosModelos* como SVD y promedios simple y ponderado. Debido a la limitacion computacional este recomendador final fue hecho en Google Collab despues de comprar mas recursos para poder correr una matriz de gran tamaño, por esta razon para poder correr este recomendador final es necesario contar con una mayor capacidad de RAM, por esta razon recomendamos usar Google Collab o AWS. 

#### **Otras carpetas en el repositorio** :
- ***ModelosNLP***
  
Se encuentra todas las pruebas para el modelo de NLP en el notebook NLPModels.ipynb, en este se probo tanto CountVectorizer, TF-IDF y LDA. Finalmente se decidio utilizar CountVectorizer debido a que el modelo de NLP contenia los generos en el analisis y estos debian mantener su peso para asi recomendar peliculas del mismo genero.

Tambien se encuentran dos archivos comprimidos numnpy: cosine_sim_sparse_matrixCOUNT.npz y cosine_sim_sparse_matrixTFIDF.npz, estos son las matrices despues de sacar similitud de coseno tanto para el Count Vectorizer y el TD-IDF Vectorizer respectivamente. Al guardarlas asi es mas facil llamarlas desde el notebook recomendador final.

El ultimo archivo en la carpeta es df_keywords_title.pkl el cual tiene la base usada para el recomendador, esta tiene id de peliculas, titulo original de la pelicula, los keywords originales y las keywords despues de hacer limpieza junto con el genero.

- ***OtrosModelos***
Se encuentra Proyecto Peliculas Clusters Final.ipynb, el notebook usado para definir los clusters para los usuarios teniendo en cuenta el rating que le dieron a peliculas por genero

 - ***Docs***
Contiene el documento final en formato PDF y la presentacion usada para el video tambien en este mismo formato

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
Finalmente se define un recomendador que se tiene el notebook Recomendadores que toma todos los modelos creados y hace el recomendador final que tiene en cuenta SVD y NLP para recomendar 5 peliculas en cada una. Teniendo en cuenta los resultados observados decidimos descartar el recomendador basado en clustering y similitud del coseno y decidimos mantener los otros tres recomendadores:

1) Para usuarios nuevos se les preguntará qué género es el que más les gusta con el fin de recomendar aquellas películas con el mejor rating utilizando el Recomendador  de Promedios ponderados y sin ponderar, que resulta ser un método simple pero efectivo a la hora de recomendar películas a aquellos usuarios que no cuentan con información previa
2) Para usuarios que ya existen en la base se le sugerirá al usuarios 5 películas utilizando filtrado por contenido basado en NLP  y otras 5 películas usando filtrado colaborativo con SVD

De esta manera nos aseguramos que para usuarios existentes nos guiamos tanto por las películas que ha visto cómo por la potencial similitud con otros usuarios.
