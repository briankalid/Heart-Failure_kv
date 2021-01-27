# Agrupamiento y análisis de grupos en personas con insuficiencia cardiaca

# Información de contacto
- José Vidal Cardona Rosas: vrosas832@gmail.com
- Brian Kalid García Olivo: briankalid2000@gmail.com

# Resumen 
En el presente documento se realizará un análisis de grupos haciendo uso del 
algoritmo de aprendizaje no supervisado, k-medios (k-means en inglés) para
determinar la razón y el por qué unas personas son más propensas al deceso
que otras. 

**keywords:** Data Mining, Clustering, K-means

# Descripción de los datos 
> Puedes interactuar con los datos en: https://share.streamlit.io/briankalid/contagiok_p

Los [datos](https://archive.ics.uci.edu/ml/datasets/Heart+failure+clinical+records#) a utilizar cuentan con 13 columnas
y con un total de 299 registros.

## Fuente
La versión original de los datos fue recopilada por:
  - Tanvir Ahmad
  - Assia Munir
  - Sajjad Haider Bhatti
  - Muhammad Aftab 
  - Muhammad Ali Raza
  
(Government College University, Faisalabad, Pakistán) y fueron puestos a disposición por las mismas personas en FigShare bajo
los derechos de autor *Attribution 4.0 International* (CC BY 4.0: libertad para compartir y adaptar el material)
en julio de 2017.

La versión actual de los datos fue elaborada por:
  - Davide Chicco (Instituto de Investigación Krembil, Toronto, Canadá)
Donada al Repositorio de Aprendizaje Automático de Irvine de la Universidad de California
bajo los mismos derechos de autor *Attribution 4.0 International (CC BY 4.0)*
en enero de 2020.


### Información de atributos
- **age:** edad del paciente (años)
- **anaemia:** disminución glóbulos rojos (booleana) 0=No tiene|1=Si tiene 
- **high blood pressure:** paciente con hipertensión (booleano) 0=No tiene|1=Sí tiene
- **creatinine phosphokinase (CPK):** nivel de la enzima CPK en sangre (mcg/L)
- **diabetes:** paciente con diabetes (booleano) 0=No tiene|1=Sí tiene
- **ejection fraction:** porcentaje de sangre que sale del corazón en cada contracción (porcentaje) 
- **platelets:** plaquetas en la sangre (kiloplaquetas/ml)
- **sex:** Mujer u Hombre 0=Mujer|1=Hombre 
- **serum creatinine:** nivel de creatinina sérica en sangre (mg/dl)
- **serum sodium:** nivel de sodio sérico en sangre (mEq/L)
- **smoking:** si el paciente fuma o no (booleano) 0=No fuma|1=Sí fuma
- **time:** período de seguimiento (días)
- **death event (target):** si el paciente falleció durante el período de seguimiento (booleano) 0=Sobrevivió|1=Murió

# Procesamiento de datos
## Detección de valores nulos
Una vez que los datos fueron analizados mediante un mapa de calor, se corroboró la inexistencia de valores nulos. 
![MapaDeCalor](imagenes/h_f_data.png)
> Mapa de calor para la detección de valores nulos.

## Filtrado de datos 
En un principio se procedió a la aplicación del algoritmo tras observar que no había datos nulos,
pero los resultados no nos dijeron mucho. Hablaremos más a fondo en la sección de
*descripción de experimentos*.
La idea para afrontar este problema surgió al detectar la variable de *diabetes*, es 
decir, estamos estudiando fallas de corazón ¿qué tanta importancia tiene la diabetes aquí? 
¿Y los demás valores? Por lo que se procedió a buscar una manera de evaluar
que parámetros aportaban más valor al análisis y cuales era preferible eliminar. A partir de 
esto, se opto por la obtención de una matriz de correlación, obteniendo los siguientes resultados:

![MatrizDeCorrelacion](imagenes/correlation_matrix.png)
> Cada cuadro contiene la correlación entre variables.
        
Para realizar el filtrado, nos hemos fijado en la correlación de cada variable con el 
*target event* que es DEATH_EVENT. Eligiendo sólo aquellas mayores o iguales
a +- 0.25 y eliminando el resto por debajo de ese valor.
Quedando al final las siguientes variables para trabajar: 
- Age
- Ejection Fraction
- Serum Creatinine
- Time
- DEATH_EVENT
Y la siguiente matriz de correlación para los datos de trabajo: 

![MatrizDeCorrelacionTrabajo](imagenes/correlation_matrix_values_work.png)
> Cada cuadro contiene la correlación entre variables.

# Descripción de la tarea de aprendizaje no supervisado

        
