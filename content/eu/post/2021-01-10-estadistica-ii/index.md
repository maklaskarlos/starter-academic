---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Estatistika: Parametro Estatistiko eta Aldagai Estatistikoa"
subtitle: "Conceptos basicos"
summary: ""
authors: [Karlos Garcia]
tags: [Estadistica, Statistics]
categories: [Estadistica, R]
date: 2021-01-10T13:30:29+01:00
lastmod: 2021-01-10T13:30:29+01:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

La estadistica es muy importante para cualquier cientifico de datos, vengas del ambito que vengas. Es la base para comprender e interpretar los resultados del proceso analítico.

Tenemos una **población** de 1.000.000 de personas 

¿como podemos medir la edad o la estatura de dicha población?
¿como definimos la edad de esa población? 
¿calculamos la medía? 
¿Y si tomamos un elemento ó un conjunto de elementos al azar de esa población y medimos una característica de interés? 
¿es lo suficientemente representativo?

El **Párametro estadístico**

En éstadistica, un **parámetro** es un número que resume la gran cantidad de datos que pueden derivarse del estudio de una **variable estadistica**

El calculo de este número esta bien definido, generalmente mediante una formula aritmetica obtenida a partir de datos de la población.

Los parámetros estadísticos son una consecuencia inevitable del propósito esencial de la estadística: crear un modelo de la realidad.

El estudio de una gran cantidad de datos individuales de una población puede ser farragoso e inoperativo, por lo que se hace necesario realizar un resumen que permita tener una idea global de la población, comparar con otras, comprobar su ajuste a un modelo ideal, realizar estimaciones sobre datos desconocidos de la misma y, en definitiva, tomar decisiones. A estas tareas contribuyen de modo esencial los parámetros estadísticos.

Por ejemplo, suele ofrecerse como resumen de la juventud de una población la media aritmética de las edades de sus miembros.

Principales parametros: 

- De Centralización: Valores que suelen situarse cerca del centro de la distribución de datos: **Media** o promedios (incluyendo **media aritmetica**), **Mediana**, **Moda**...

- De Posisición: Divide un conjunto de datos en grupos con el mismo numéro de individuos: **Cuartil**, **Decil**, **Percentil**...

- De Dispersión: 

(Absolutas) **Recorridos**, **Desviación Media**, **Varianza** y **Desviación Tipica** (Relativas) **Coeficiente de Variación de Person**, **Coeficiente de apertura**, **Recorridos relativos** e **Inidice de desviación respecto a la mediana**

- De Forma: **Medidas de asimetría** y **Medidas de apuntamiento o curtosis**

Un parámetro estadístico es deseable que tenga las siguientes propiedades:

- Se define de una manera objetiva
- No desperdicia, a priori, ninguna de las observaciones
- Es interpretable, significa algo
- Es sencillo de calcular y se presta con facilidad a manipulaciones algebraicas
- Es poco sensible a las fluctuaciones muestrales. Esta propiedad es más interesante en el caso de la estimación de parámetros


**Variable Estadistica**

Una variable estadística es una característica que puede fluctuar y cuya variación es susceptible a adoptar diferentes valores, los cuales pueden medirse u observarse. Las variables adquieren valor cuando se relacionan con otras variables, es decir, si forman parte de una **hipótesis** o de una teoría. En este caso se las denomina constructos o construcciones hipotéticas.

A partir de este concepto se puede mencionar que una variable es la que permite relacionarla con algún problema o fenómeno, el cual vamos a investigar y buscar posible soluciones.

1) Variables categóricas: Dicotómicas, Nominales
y Ordinales

2) Variables numéricas: Continua y Discreta

3) Tipos de variables: Dependientes o independientes, Cualitativa o Cuantitativa,...

4) Segun el nivel de medida: 

Cualitativa - Nominal - No existe criterio de orden, por ejemplo los colores o el lugar de nacimiento
Cualitativa -Ordinal - Criterios de order siguiendo una escala establecida, aunque no es necesario que el intervalo entre mediaciones sea uniforme, por ejemplo: leve, moderado, fuerte.

Cuantitativas - Discreta - Tiene un número finito de valores o un número contable de valores, por ejemplo 0,1,2,3... **Distribución Binomial**, **Distribución Uniforme**. 

Cuantitativas - Continua - La única forma de representar un conjunto infinito de valores es mediante un intervalo [a, b]. En otras palabras, es la variable que puede adquirir cualquier valor dentro un intervalo especificado de valores. Por ejemplo, el peso en kg: 2,3 2,4 2,5…o la altura en metros 1,65 1,66 …o el salario. **Distribución Normal**

5) Según nivel de influencia:

Dependientes - Una variable dependiente es aquella cuyos valores dependen de los que tomen otras variables. **La variable dependiente es una función**. Son las variables de respuesta que se observan en el estudio, y que podrían estar influidas por los valores de las variables independientes.

Independientes -  Una variable independiente es aquella cuyo valor no depende de otra variable. Es aquella característica o propiedad que se supone es la causa del fenómeno estudiado.

Informazio gehiago:

https://www.amarauna.euskadi.eus/baliabidea/aldagai-estatistikoak/be9215aa-8ce0-4c04-9149-d27e0b107adf


**Estadistica Descriptiva**
**Estadistica Inferencial**

Un parámetro estadístico es una medida poblacional y este enfoque es el tradicional de la **estadística descriptiva**

Es la técnica matemática que obtiene, organiza, presenta y describe un conjunto de datos con el propósito de facilitar el uso, generalmente con el apoyo de tablas, medidas numéricas o gráficas.

Estas técnicas son utilizadas en el proceso de investigación, en la etapa donde el investigador necesita procesar y analizar los datos recolectados en dicho estudio.

Sin embargo, la **inferencia estadística** utiliza el concepto de parámetro en su significado matemático más puro, es decir, como variable que define una familia de objetos matemáticos en determinados modelos.

En ocasiones los parámetros de una determinada población no pueden conocerse con certeza. Esto ocurre porque es imposible el estudio de la población completa por diferentes cuestiones. Generalmente, por cuestiones economicas. En tales situaciones se recurre a las técnicas de la inferencia estadística para **realizar estimaciones de tales parámetros a partir de los valores obtenidos de una muestra de la población**.

Se distingue entonces entre parámetros y estadísticos

Mientras que un parámetro es una función de los datos de la población, el estadístico lo es de los datos de una muestra. De este modo pueden definirse la media muestral, la varianza muestral o cualquier otro párametro de los vistos más arriba.

**Estimador**

En estadística, un estimador es un estadístico (esto es, una función de la muestra) usado para estimar un parámetro desconocido de la población. 

Por ejemplo, si se desea conocer el precio medio de un artículo (el parámetro desconocido) se recogerán observaciones del precio de dicho artículo en diversos establecimientos (la muestra) y la media aritmética de las observaciones puede utilizarse como estimador del precio medio.

Para cada parámetro pueden existir varios estimadores diferentes. En general, escogeremos el estimador que posea mejores propiedades que los restantes, como insesgadez, eficiencia, convergencia y robustez (consistencia).

El valor de un estimador proporciona lo que se denomina en estadística una estimación puntual del valor del parámetro en estudio. En general, se suele preferir realizar una estimación mediante un intervalo, esto es, obtener un intervalo [a,b] dentro del cual se espera esté el valor real del parámetro con un cierto **nivel de confianza**. Utilizar un intervalo resulta más informativo, al proporcionar información sobre el posible **error de estimación**, asociado con la amplitud de dicho intervalo. 

El nivel de confianza es la probabilidad de que a priori el verdadero valor del parámetro quede contenido en el intervalo.

**Variable Aleatoria**

Una variable aleatoria es una función que asigna un valor, usualmente numérico, al resultado de un experimento aleatorio. 

Por ejemplo, los posibles resultados de tirar un dado dos veces: (1, 1), (1, 2), etc. o un número real (p.e., la temperatura máxima medida a lo largo del día en una ciudad concreta).

Una variable aleatoria puede concebirse como un valor numérico que está afectado por el azar. Dada una variable aleatoria, no es posible conocer con certeza el valor que tomará al ser medida o determinada. Aunque sí se conoce que existe una **distribución de probabilidad** asociada al conjunto de valores posibles. 

Por ejemplo, en una epidemia de cólera, se sabe que una persona cualquiera puede enfermar o no (suceso), pero no se sabe cuál de los dos sucesos va a ocurrir. Solamente se puede decir que existe una probabilidad de que la persona enferme.

Para trabajar de manera sólida con variables aleatorias en general es necesario considerar un gran número de **experimentos aleatorios**, para su tratamiento estadístico, cuantificar los resultados de modo que se asigne un número real a cada uno de los resultados posibles del experimento. De este modo se establece una relación funcional entre elementos del espacio muestral asociado al experimento y números reales.
