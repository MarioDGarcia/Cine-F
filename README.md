# Cine-F

## DataSet:
El dataset fue generado desde 0 con script de Python usando pandas con mas de 10,000 registros

Nuestro dataset consta de 3 archivos CSV, los cuales son:
 ### Películas (peliculas.csv)
Contiene información básica de cada película.
•	idPelicula: Identificador único de la película.
•	titulo: Título de la película.
•	calificacion: Calificación en escala del 1 al 10.
•	genero: Género cinematográfico (ej. Acción, Comedia, etc.).
•	director: Nombre del director.
•	estrellas: Número de estrellas otorgadas (1 a 5).
•	año: Año de estreno de la película.
•	duracion en Minutos: Duración total de la película en minutos.
### Salas (salas.csv)
Describe las características físicas de las salas del cine.
•	sala: Nombre o código de la sala (ej. SALA_1).
•	idSala: Identificador numérico único de la sala.
•	capacidad: Número máximo de asientos disponibles.
•	tipo de sala: Tipo de sala (2D, 3D, 4D – puede incluir variantes sucias como "2D", "2d", etc.).

### Cine (cine.csv)
Historial de funciones proyectadas en el cine.
•	fecha: Fecha de la proyección (con distintos formatos, como YYYY-MM-DD, DD/MM/YYYY, etc.).
•	idsalaUsada: ID de la sala utilizada para la proyección.
•	hora: Hora de inicio de la función (formato puede variar).
•	IdpeliculaProyectada: ID de la película que se proyectó.
•	precio boleto: Precio del boleto en pesos mexicanos.
•	boletosVendios: Número de boletos vendidos (puede incluir errores intencionales o sobreventa).


## Utilizando el principio R.O.C.C.C
### Reliable: conjuntos de datos fueron generados mediante un script en Python utilizando librerías como Faker, NumPy y Pandas. Se introdujo ruido de forma controlada (valores faltantes, errores de formato y etiquetas inconsistentes) para simular condiciones reales en los datos.
### Original: Los datos no fueron copiados de fuentes existentes. Se generaron desde cero, incluyendo nombres ficticios, fechas y características variadas de películas, salas y proyecciones. Esto garantiza que no hay problemas de privacidad o licencias.
### Comprehensive:
Los tres archivos cubren un flujo completo del negocio cinematográfico:
•	Información de películas (contenido, duración, año, etc.).
•	Infraestructura de salas (capacidad y tipo).
•	Historial de proyecciones (fechas, precios y ventas).
Esto permite realizar análisis cruzados como: desempeño por género, rentabilidad por sala, demanda por día/hora, etc.
### Current: 
Las fechas abarcan desde 2023 hasta mayo de 2025, lo cual permite análisis de tendencias recientes y proyecciones a futuro. Esto es especialmente útil para simulaciones en Power BI o modelos predictivos.
### Cited:
Los datos fueron generados artificialmente usando herramientas bien establecidas:
•	Faker para generar nombres y texto.
•	Pandas y NumPy para manipulación y aleatorización de datos.
No se utilizaron fuentes externas reales

Al ser un data set relativamente pequeño, se utilizará SQL para un análisis exploratorio muy rápido, pero antes se usará Excel para la limpieza de los datos


## Limpieza:


## Analisis

## Visual - Power BI
