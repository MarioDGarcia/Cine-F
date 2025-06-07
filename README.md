# Cine-F
Supongamos que se nos pidio sacar las siguientes preguntas:
### Preguntas
Plantearemos las siguientes preguntas que tendremos que responder con nuestros datos, las cuales son:

•¿Cuál es el total de ingresos de boletos vendidos?

•¿Qué días o meses se vendieron más boletos?

•¿Qué tipo de sala genera más ingresos?

•¿Cual es la temporada alta y baja?

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
  • Dato por default -> No había datos por default
	 • Dato aproximado -> Al haber muchos datos con varias diferencias no se tomó en cuenta 
  • Eliminar Fila -> se decidió el eliminar las filas, esto hizo que 199 datos fueron eliminados, de los 10,000 originales
•	Campos duplicados:
  •No había datos duplicados
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

Vemos que si hay ocasiones sonde los boletos vendidos superan a la capacidad de la sala, 
eliminaremos esas filas porque no nos son útiles	y probablemente sean ventas mal registradas

 ![image](https://github.com/user-attachments/assets/3ead897f-9703-40cd-a233-5ff9a8a36475)
 
Esto nos quita 886 filas, nos restan 8723 registros 

Despues de varias consultas y movimientos realizados, tenemos 2 opciones, al ser un data set relativamente pequeño, podríamos unir todo mediante Joins, y quedarnos con la información que queramos o poder seguir con nuestros 3 archivos y trabajar con ellos en power Bi con un modelado de datos correcto.
obte por trabajar con un modelado de datos en Power BI, porque la tabla de películas tiene información que puede ser relevante a analizar

## Visual - Power BI
Como se trabajó con fechas y ventas, se hizo una tabla de fechas para poder trabajar con ellas, de ahí se realizó el modelado de datos para tener las conexiones correctamente

![image](https://github.com/user-attachments/assets/27169886-a732-4d03-bd4f-d7df1946bfc5)

Aún que es un dataset de pocas tablas el modelado es uno de tipo estrella siendo la tablla "Cine Limpio" la principal


### Columnas calculadas:
	$Venta Total = ROUND('Cine limpio'[precio boleto]* 'Cine limpio'[boletosVendios],2)
La columna anterior sera muy util en algunas medidas futuras


### Medidas utilizadas:
Se crearón diferentes medidas para poder establecer los distintos KPI usados en el visual

	Proyecciones Totales = COUNTROWS('Cine limpio')
La medida antereior nos cuenta cuantas proyecciones hubo

	Fecha Actual = 
	VAR Mes = SELECTEDVALUE(Calendario[Date].[Mes])
	VAR Anio = SELECTEDVALUE(Calendario[Date].[Año])
	
	RETURN
	SWITCH(
	    TRUE(),
	    ISBLANK(Mes) && ISBLANK(Anio), "Datos Generales",
	    ISBLANK(Mes), "Año " & Anio,
	    ISBLANK(Anio), UPPER(Mes),
	    UPPER(Mes) & " del Año " & Anio
	)
La anterior medida es para modificar **etiquetas** dependiendo de que este seleccionado

	Mes Actual = 
	IF (
	    ISBLANK(SELECTEDVALUE(Calendario[Date].[Mes])),
	    "Ganancia % Meses",
	    IF (
	        ISBLANK(SELECTEDVALUE(Calendario[Date].[Año])),
	        "Todos los " & UPPER(SELECTEDVALUE(Calendario[Date].[Mes])),
	        "Ganancia % " & UPPER(SELECTEDVALUE(Calendario[Date].[Mes])) & " Año Pasado"
	    )
	)
La anterior Medida nos muestre el mes actual y tambien si seleccionamos el año cambie el *texto* de una **etiqueta** 

	TEXT año anterio vs actual = 
	VAR VentasActuales = SUM('Cine limpio'[$Venta Total])
	VAR VentasAnioPasado = [Ventas LY]  -- Medida previamente creada con SAMEPERIODLASTYEAR
	VAR Variacion = DIVIDE(VentasActuales - VentasAnioPasado, VentasAnioPasado)
	
	VAR AnioActual = SELECTEDVALUE(Calendario[Date].[Año])
	
	RETURN
	IF(ISBLANK(SELECTEDVALUE(Calendario[Date].[Mes])),
		IF(
		    ISBLANK(Variacion) || ISBLANK(AnioActual),
		    "Ganancia % Año Anterior",
		    "Ganancia % " & UPPER(AnioActual - 1) & " VS " & AnioActual
		),"Ganancia % Solo Año Anterior"
	)

La anterior Medida nos muestre un *texto*, deacuerdo con el año seleccionado y el año anterior, pero si no hay año anterior muestra un texto generico para una **etiqueta**

	Ventas LY = 
		CALCULATE(
		sum('Cine limpio'[$Venta Total]),
		PREVIOUSYEAR((Calendario[Date])
		)
	)

	Ventas LM = 
		CALCULATE(
		    sum('Cine limpio'[$Venta Total]),
		    PREVIOUSMONTH((Calendario[Date])
		)
	)
 
Las medidas anteriores son necesarias para posteriores medidas, pero en otras palabras son para usar Time Intelligence y ver ventas con respecto a algo, en este caso el AÑO y MES, respectivamente 


	Variación % Año vs Año = 
	VAR VentasActuales = SUM('Cine limpio'[$Venta Total])
	VAR VentasAnioPasado = [Ventas LY]  -- Esta medida debe estar definida previamente con SAMEPERIODLASTYEAR u otra función
	
	VAR Variacion = DIVIDE(VentasActuales - VentasAnioPasado,VentasAnioPasado)
	
	RETURN 
	IF(
		    ISBLANK(Variacion),
		    "N/A",
		    if(
		        ISBLANK(SELECTEDVALUE(Calendario[Date].[Mes])),
			        IF(
			            Variacion >= 0,
			            "▲ " & FORMAT(Variacion, "0.00%"),
			            "▼ " & FORMAT(Variacion, "0.00%")
			        ),
		        	"N/A"
			)
	)

	
	Variacion % Mes vs Mismo Mes Ano Anterior = 
		VAR VentasActuales = SUM('Cine limpio'[$Venta Total])
		VAR VentasAnoPasado = 
		    CALCULATE(
		        SUM('Cine limpio'[$Venta Total]),
		        SAMEPERIODLASTYEAR('Calendario'[Date])
		    ) //pude ser la misma medida que tenemos como Ventas LY
		
		VAR Variacion = 
		    IF(
		        ISBLANK(VentasAnoPasado) || VentasAnoPasado = 0,
		        BLANK(),
		        DIVIDE(VentasActuales - VentasAnoPasado, VentasAnoPasado)
		    )
		
		RETURN 
		IF(
		    ISBLANK(SELECTEDVALUE('Calendario'[Date].[Mes])), 
		    "Sin Mes", 
		    IF(
		        ISBLANK(Variacion),
		        "Sin Datos",
		        IF(ISBLANK(SELECTEDVALUE(Calendario[Date].[Año])),"Sin Año" ,
				IF(
		            Variacion >= 0,
		            "▲ " & FORMAT(Variacion, "0.00%"),
		            "▼ " & FORMAT(Variacion, "0.00%")
		        	)
		    	)
			)
		)

La medida anterio nos sirve para una **etiqueta** y nos mostrará el % de ganacia o perdida, dependiedo de AÑo o MES selecionado, respectivamente, cabe resaltar que si seleccionamos un mes y un año a la vez, solo mostrará numeros la segunda medida,
si seleccionamos solo el año sin mes, nos dará la ganacia/perdida respecto al año pasado (la primera medida se modifica)

## Dashboard:
![image](https://github.com/user-attachments/assets/2d0d94a2-e9a1-4c43-8307-3d742c6d0402)

(Para una visualizacion dinamica y completa, es recomendable descargar el archivo con extension .pbix para visualizar con mayor comodidad los KPI)


## Respondiendo preguntas iniciales:
Ahora despues de haber hecho este analisis, limpieza y visualizacion de los datos Respoderemos a las preguntas iniciales

### ¿Cuál es el total de ingresos de boletos vendidos?
R: El total de todos los años y meses fueron -> $53,037,579 
si vamos por años, 
	
*2023* -> $22,809,113
 	
*2024* -> $21,982,816
  	
*2025* -> $8,245,651

### ¿Qué días o meses se vendieron más boletos?
Los meses con mas Ventas son:

• Mayo

• Abril

• Enero

y los mejores dias:
	
• 20

• 19 

• 7

### ¿Qué tipo de sala genera más ingresos?
El tipo de sala que genero mas ventas fueron en este orden: 
	
• 4D con 21 millones MXN 

• 2D con 17 millones MXN
	
• 3D con 15 millones MXN
 
### ¿Cual es la temporada alta y baja?

La temporada *alta* es alrededor de los dias *17-23* y los meses *Marzo - Mayo*

La temporada *baja* es alrededor de los dias *6-12* y los meses *Junio - Septiembre*


