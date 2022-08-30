# Introducción

Este framework tiene como fin evaluar el data drift en un dataframe.

Se evalua con de diferentes test estadísticos y a través de los distintos data chuncks en los que se divide automáticamente el dataframe analizado.


# Descripción del framework
Este framework utiliza la siguiente lógica. 


![diagrama_rect](https://user-images.githubusercontent.com/65657909/178510588-c0642d16-e0b6-455d-b919-91b1e2acf91b.PNG)
 
* Es capaz de analizar los datos de entrada tanto de manera univariante como multivariante.
* Es capaz de poder analizar el data drift en variables categóricas, cuantitativas y binarias.
* Puede variar el tamaño de los data chunks en los que se divide el dataframe de analisis
* Cuenta con una lógica que utliliza una serie de test estadísticos y otros dependiendo del dataframe analizado


# Como usar y que esperar

Se requiere de un dataframe de referencia y otro de analisis. Estos deben estar en formato .csv. El primero servirá para conocer la distribución que se espera tengan los datos de entrada a un modelo. El dataframe de referencia
puede ser el que se utilizó para entrenar el modelo primeramente. El de analisis será el dataset evaluado.

Se necesitan dos parametros de entrada.
* Número de data chunks en los que se desea partir el dataframe de analisis
* Un array con información relativa al tipo de variable que contiene cada columna en el dataframe

Una vez todos los parametros de entrada hayan sido cargados, se espera obtener 2 graficas. 

La primera, representa el valor del test estadístico utilizados, a través de los diferenets  data chunks. 
La línea discontínua representa los límites de la hipótesis nula de cada estadístico

![caso2_drift_dinero_prestado](https://user-images.githubusercontent.com/65657909/178513901-3e4e74ef-1b55-491a-953d-66a3bd16858b.png)

También se proporciona un informe con la cantidad de alertas obtenidas en cada variable, tanto en la distribución univariante como en la multivariante. 


![informe_caso2_dinero_prestado](https://user-images.githubusercontent.com/65657909/178514023-db43fb35-f42e-469c-b36b-4101fe1d88a6.png)




# Información extra y precauciones para el correcto uso

* Para el test estadístico de CHi cuadrado y reconstrución por error de PCA se utliliza la librería de [NannyML](https://nannyml.readthedocs.io/en/stable/index.html).
* Se recomienda que el tamaño del dataframe de analisis sea mayor que el de referencia. En ningún caso el dataframe de referencia debe ser mayor que el de analisis.
* El nivel de significación de los test estadísticos está establecido al 5%
* El número de alteras es relativo al número de datachuncks, por lo que eso cambia para cada caso.
* Se puede dar el caso de tener drift univariante pero no multivariante y viceversa
