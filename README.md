# Cine-F
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
### Reliable:
Los conjuntos de datos fueron generados mediante un script en Python utilizando librerías como Faker, NumPy y Pandas. Se introdujo ruido de forma controlada (valores faltantes, errores de formato y etiquetas inconsistentes) para simular condiciones reales en los datos.
### Original: 
Los datos no fueron copiados de fuentes existentes. Se generaron desde cero, incluyendo nombres ficticios, fechas y características variadas de películas, salas y proyecciones. Esto garantiza que no hay problemas de privacidad o licencias.
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
### Archivo cine.csv
•	Formateo de fechas
•	Campos vacíos:
o	Dato por default -> No había datos por default
o	Dato aproximado -> Al haber muchos datos con varias diferencias no se tomó en cuenta 
o	Eliminar Fila -> se decidió el eliminar las filas, esto hizo que 199 datos fueron eliminados, de los 10,000 originales
•	Campos duplicados:
o	 No había datos duplicados
### Archivo sala.csv
•	Tipo de sala corregido y formateado  
### Archivo Peliculas:
•	Id faltante colocado

## Analisis
Nuestros datos están divididos en 3 archivos como se mencionó anteriormente, se usará SQL para poder hacer una breve análisis exploratorio y familiarizarnos con los datos	
Unificaremos las 3 tablas para poder ver en una sola consulta unos datos mas detallados
![image](https://github.com/user-attachments/assets/7c02a780-ff22-4495-88ef-c03a43babe2a)
La consulta anterior nos da como resultado:
![image](https://github.com/user-attachments/assets/ecc75ec2-ee5e-46f1-8fcd-959c24e3683d)
Aquí podemos ver la fecha, el tipo de sala que se proyectaba, los boletos vendidos, el precio del boleto, película y demás apartados.
En Veremos si hay datos que se salen de sus limites, como boletos vendidos y la capacidad de la sala con un ordenamiento por boletos vendidos
 ![image](https://github.com/user-attachments/assets/a4424da8-524d-4555-9558-3045361cf77d)

Vemos que si hay ocasiones sonde los boletos vendidos superan a la capacidad de la sala, eliminaremos esas filas porque no nos son útiles	y probablemente sean ventas mal registradas
 ![image](https://github.com/user-attachments/assets/3ead897f-9703-40cd-a233-5ff9a8a36475)

Esto nos quita 886 filas, nos restan 8723 registros 

Despues de varias consultas y movimientos realizados, tenemos 2 opciones, al ser un data set relativamente pequeño, podríamos unir todo mediante Joins, y quedarnos con la información que queramos o poder seguir con nuestros 3 archivos y trabajar con ellos en power Bi con un modelado de datos correcto.
obte por trabajar con un modelado de datos en POower Bi, porque la tabla de películas tiene información que puede ser relevante a analiszar

## Visual - Power BI
