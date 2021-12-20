---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Estadistica: Estimacion de Parametros"
subtitle: "Conceptos basicos"
summary: ""
authors: [Karlos Garcia]
tags: [Estadistica, Statistics]
categories: [Estadistica, R]
date: 2021-02-10T13:30:29+01:00
lastmod: 2021-02-10T13:30:29+01:00
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

Cuando empezamos a estudiar **probabilidad** a menudo se nos dice cual es la probabilidad de un evento, y a partir de ahí, intentamos estimar la probabilidad de varios resultados (outputs). Aunque, en realidad, el proceso inverso es mucho mas comun: **tenemos datos sobre los resultados, pero desconocemos la probabilidad de que dicho evento ocurra realmente**.

Tratar de entender este parametro que falta se conoce como **estimación de parametros**.

En terminos de Marketing, lograr que un usuario realize un evento deseado se denomina conversión, y la probabilidad de que un usuario realice una conversión es la tasa de conversión.

**Me gustaría conocer cual es la probabilidad de que un usuario acabe suscribiendose al blog de mi web**

Para poder conocer esta probabilidad, tenemos que mencionar la **Distribución de Probabilidad discreta y continua**, sabras que la manera de determinar "p", la probabilidad de que un usuario se suscriba, dado "k", el numero de personas suscritas, y "n", el numero total de visitantes web, es a través de la **distribución Beta**.

**The Probability Density Function** Para los primeros 40000 visitantes obtengo 300 suscriptores. Beta(300,39700), recordar que β es el numero de personas que no se han suscrito, y no el total. Se puede visualizar la PDF para esta distribución Beta en el siguiente enlace:

https://www.countbayesie.com/blog/2015/4/4/parameter-estimation-the-pdf-cdf-and-quantile-function

Con los datos que tenemos podemos **inferir (deducir)** que la conversión media es simplemente 300 / 40000 = 0,0075

Podemos utilizar la PDF para comparar dos extremos: 

La probabilidad que nuestra tasa de conversión sea en realidad mas baja de lo que hemos visualizado =  0,008

Otra pregunta: ¿Cual es la probabilidad de que tengamos mala suerte y nuestra tasa de conversión real sea superior a 0.0085? Respuesta = 0,012

Significa que la probabilidad de que nuestra tasa de conversión sea mucho mas alta de los observamos es, en realidad, un poco más probable, que la probabilidad de que sea mucho menor que la observada! 

Todo integrales...

Una mejor función es la:

**Cumulative Distribution Function!** 

La CDF, para cualquier distribución de probabilidad, me dice como de probable es que un valor este por debajo de x en nuestra distribución

Para poder vislualizar el CDS, mismo enlace:

https://www.countbayesie.com/blog/2015/4/4/parameter-estimation-the-pdf-cdf-and-quantile-function

Podemos visuzalizar la mediana, trazando una linea desde el punto en el que la probabilidad acumulada sea 0.5. El 50% de los puntos estan por debajo de este punto y otro 50% por encima.

La CDF permite estimar la mediana y otros cuantiles de forma rapida y precisa.

Podemos ver como la mediana esta muy cerca de nuestra **expectativa** de 0.0075

Para estimar la probabilidad de que la tasa de conversión esté entre 0,0075 y 0,0085, podemos trazar lineas desde el eje "x" (probabilidad de suscribirse) en estos puntos y luego ver donde se encuentran con el eje "y" (probabilidad acumulada). La distacia entre ellos es la integral aproximada.

Observando la CDF, podemos ver que en el eje "y" estos valores van desde aproximadamente 0.5 a 0.99, lo que siginifica que hay aproximadamente un 49% de probabilidad de que nuestra verdadera tasa de conversión se encuentre en algun lugar entre estos dos valores. 
La razón por la que podemos realizar la integración visual es por que estamos integrando visualmente la PDF, literalmente!

**Confidence Interval**

Ahora que sabemos que hay un rango de posibles valores que poddriamos tener, tiene mucho sentido preguntar:

¿cual es el rango que que cubre el 80% de las posibilidades?

La CDF facilita mas que la PDF estimar la precision de los intervalos de confianza 

Comenzamos en el eje "y" y dibujamos lineas desde 0,1 y 0,9 y luego, simplemente vemos en que parte del eje "x" se cruzan...

Como podemos ver en el siguiente link...

https://www.countbayesie.com/blog/2015/4/4/parameter-estimation-the-pdf-cdf-and-quantile-function

...la interseccion del eje "x" esta aproximadamente en 0.007 y 0.008, lo que siginifica que hay un 80% de probabilidad de que nuestra tasa de conversion real se encuentre en algun lugar entre estos dos valores.


