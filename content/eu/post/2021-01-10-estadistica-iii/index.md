---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Estadistica: Distribuciones de Probabilidad"
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

En esta publicación exploraremos la idea de distribuciones de probabilidad discretas y continuas.

Todo lo que vamos hablar lo pueden encontrar en:

https://www.countbayesie.com/blog/2015/3/17/interrogating-probability-distributions

**Discrete Probability Distributions**

El primer tipo de distribución que podemos analizar es el tipo de distribución que se obtiene al lanzar monedas.

Si lanza 30 monedas, puede tener de 0 a 30 caras, pero no puede obtener 1,5 caras

La distribución que describe el numero de caras despues de lanzar 30 veces una moneda es una distribución de probabilidad discreta. **Distribución Binomial**

Cuando usamos la Distribución Binomial conocemos la "p" y la "n" y la distribución describe las probabilidades para todas las "k" que podemos tener. Ver el grafico del ejemplo de moneda justa en el enlace: p = 0.5 y n = 30

Tipo de preguntas puede responder nuestra **Probability Mass Function**

¿Cual es la probabilidad de obtener exactamente 5 caras?
¿Cual es la probabilidad de obtener de 18 a 24 caras?
¿Cual es la probabilidad de de que el numero de caras termine en 3?

No podemos preguntar

¿Cual es la probabilidad de obtener 1,5 caras?

**Continuous Probability Distributions**

Supongamos que tenemos una moneda y no sabemos si es justa...queremos poder lanzar una moneda repetidamente y hacer una buena suposición...es decir...conocemos "k" y "n", pero no desconocemos "p"...

...despues de 30 lanzamientos, tenemos 11 caras...cual es nuestra mejor suposición para "p"?

Una de las cosas que podemos hacer es mirar la distribución Binomial. Si asumimos que "p" es igual a 0,5, la distrobución binomial dice que solo hay una probabilidad de 0,05 de obtener 11 caras en 30 lanzamientos. Dada una distribución Binomial donde p = 0,5, este resultado no parece muy probable.

Lo que podemos hacer a continuación es observar un montón de distribuciones Binomiales diferentes definidad por diferentes "p" y comparar como de bien explica cada una de ella los datos. Podemos ver en el enlace el grafico de multiples distribuciones binomiales:

En el grafico podemos ver que el pico es en realidad un poco menos de 0,4. 

Si no nos hubiéramos centrado tanto en las ditribuciones de probabilidad, nuestra primera suposición para la "p" mas probable hubiéra sido 11/30 = 0,366. Podríamos continuar dividiendo en partes cada vez mas pequeñas, pero nunca llegaremos a una distribución que contenga 11/30 por que es un decimal que se repite. Por lo tanto, necesitamos una distribución que sea verdaderamente continua para modelar incluso todos los numeros racionales que podrían interesarnos.

Hay otro problema con nuestra distribución que es menos obvio... nuestras probabilidades discretas no suman 1! Significa que necesitamos algún tipo de constante de normalización para forzar que nuestros valores se resuman correctamente.

La distribución que resuelve este problema es la: 

**Beta Distribution**

Nos referimos a esta función como **Probability Density Function** en lugar de **Probability Mass Function**

Tipo de preguntas **Continuous Probability Distributions**

¿Cual es la probabilidad de que "p" sea exactamente 0,4?

Si bien podemos ver que la distribución es muy densa cerca de p = 0,4, la respuesta a esta pregunta es en realida 0. Intituivamente esto tiene sentido, es muy probable que la probabilidad de que salga cara sea alrededor de 0,4, pero practicamente no hay manera de que sea exactamente 0,4 y no 0,40000001 o 0,3999999.

Matematicamente, también tiene sentido. Si pensamos en dividir nuestra distribución de probabilidad discreta en partes cada vez mas pequeñas (por ejemplo incialmente dividimos 0-1 en secciones de tamaño 0,1) cada x puede ser tomada como 1/n, que se hace mas pequeño cada vez que n crece. La probabilidad de cualquier "x" dada, es f(x) * 1/n donde f es nuestra función de densidad de probabilidad. A medida que nos acercamos a una función continua "n" tiende a infinito.Da igual cuanto de grande se hace f(x) que siempre va a tener probabilidad 0.

¿Cual es la probabilidad de que "p" este entre 0,2 y 0,5?
¿Cual es la probabilidad de que "p" termine en 3? Esto es un interesante problema por que tenemos que contar todos los numeros como 0,3 0,333 0,13 ...

