---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Estadistica I"
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

Un analista de datos o cientifico de datos debería de entender la estadistica, pero no a todo el mundo le gusta estudiar. Diría que el estudio es necesario hasta para los mejores programadores de software que estan intentando convertirse en data scientist! 

Para hacer un buen uso de los datos, tenemos que hacer preguntas que permitan obtener conclusiones de negocio, tenemos que ser curiosos para mejorar continuamente tu empresa y tienes que empezar a aplicar tecnicas de machine learning para automatizar analiticas en tus procesos empresariales. La estadistica te dará una base importante, por que **te ayudará a comprender e interpretar resultados del codigo**. El lenguaje R dicen que esta preparado para la estadistica.

Vamos a empezar repasando los conceptos mas basicos...

¿si tenemos una **población** de 1.000.000 de personas, como podemos medir la edad o la estatura de dicha población?

¿como definimos la edad de esa población? ¿calculamos la medía? 

¿Y si tomamos un elemento ó un conjunto de elementos al azar de esa población y medimos una característica de interés? ¿es lo suficientemente representativo?

Son algunas de las preguntas que nos hacemos cuando utilizamos la estadistica.

El proceso de estimación: Sintetizar mis datos a traves de **parametros estadisticos**. 

Utilizamos el termino **estadístico** para describir una caracteristica de la **muestra** a traves de un valor numérico. El valor de este estadístico depende de la muestra seleccionada en el que es calculado y puede cambiar dependiendo de la muestra que seleccionamos. 

La selección de la muestra es de manera **aleatoria**

Un **estadístico** que se utiliza para **estimar** un **parámetro desconocido** de la **población**, se denomina **estimador**. Y como la base del calculo del valor de dicho estimador es la muestra, también es una valor aleatorio: **Variable Aleatoria**. 

**La distribución** del estimador viene dada por el conjunto de los resultados obtenidos a partir del conjunto de las muestras posibles.

Se puede categorizar las variables segun su nivel de medida e influencia:

**Variables** según nivel de Medida:

- **Cualitativa**: **Nominal**: En esta variable los criterios no pueden ser sometidos a un criterio de orden, por ejemplo los colores o el lugar de nacimiento. **Ordinal**: La variable puede tomar distintos valores ordenados siguiendo una escala establecida, aunque no es necesario que el intervalo entre mediaciones sea uniforme, por ejemplo: leve, moderado, fuerte.

- **Cuantitativas**: Variable aleatoria **discreta**: Tiene un número finito de valores o un número contable de valores. (0,1,2,3, etc.). **Distribución Binomial**, **Distribución Uniforme**. Variable aleatoria **continua**: Tiene un numero infinito de valores representado por un intervalo [a, b]. La única forma de representar un conjunto infinito de valores es mediante un intervalo. En otras palabras, es la variable que puede adquirir cualquier valor dentro un intervalo especificado de valores. Por ejemplo la masa (2,3 kg, 2,4 kg,2,5 kg …) o la altura (1,65 m, 1,66 m, …) o el salario. **Distribución Normal**

**Variables** según nivel de Influencia:

- **Dependientes**: Una variable dependiente es aquella cuyos valores dependen de los que tomen otras variables. **La variable dependiente es una función**. Son las variables de respuesta que se observan en el estudio, y que podrían estar influidas por los valores de las variables independientes.

- **Independientes**: Una variable independiente es aquella cuyo valor no depende de otra variable. Es aquella característica o propiedad que se supone es la causa del fenómeno estudiado.

Para cada parametro pueden existir varios estimadores, pero escogeremos el que posea mejores propiedades: Sesgo, eficiencia, convergencia y robustez.

**Parametros Estadisticos**: 

- Centralización: En torno a que valor se distribuyen los datos: **Media**, **Mediana**, **Moda**

- Posisición: Divide un conjunto de datos en grupos con el mismo numéro de individuos: **Cuartil**, **Decil**, **Percentil**

- Dispersión: **Desviación Media**, **Varianza** y **Desviación Tipica**

