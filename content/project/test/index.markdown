---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Reporting de ventas con R (Multidivisa)"
summary: ""
authors: []
tags: []
categories: []
date: 2020-11-28T21:20:55+01:00

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: "Top"
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---
<script src="{{< relref "project/test/index.markdown" >}}index_files/kePrint-0.0.1/kePrint.js"></script>
<link href="{{< relref "project/test/index.markdown" >}}index_files/lightable-0.0.1/lightable.css" rel="stylesheet" />
<script src="{{< relref "project/test/index.markdown" >}}index_files/kePrint-0.0.1/kePrint.js"></script>
<link href="{{< relref "project/test/index.markdown" >}}index_files/lightable-0.0.1/lightable.css" rel="stylesheet" />
<script src="{{< relref "project/test/index.markdown" >}}index_files/kePrint-0.0.1/kePrint.js"></script>
<link href="{{< relref "project/test/index.markdown" >}}index_files/lightable-0.0.1/lightable.css" rel="stylesheet" />
<script src="{{< relref "project/test/index.markdown" >}}index_files/kePrint-0.0.1/kePrint.js"></script>
<link href="{{< relref "project/test/index.markdown" >}}index_files/lightable-0.0.1/lightable.css" rel="stylesheet" />
<script src="{{< relref "project/test/index.markdown" >}}index_files/kePrint-0.0.1/kePrint.js"></script>
<link href="{{< relref "project/test/index.markdown" >}}index_files/lightable-0.0.1/lightable.css" rel="stylesheet" />

Para un economista es importante tener acceso a datos economicos de forma rapida y sencilla que permitan tomar decisiones en base a datos analizados. Las librerias de R que permiten hacer este tipo consultas son: **quantmod** y **Quandl**




```r
library(quantmod)
library(Quandl)
```


```r
library(tidyverse)
library(dplyr)
library(kableExtra)
library(reshape)
library(lubridate)
library(ggplot2)
library(scales)
library(tidyquant)
```

La función **getSymbols()** de la libreria **quantmod** permite consultar datos economicos de **distintas fuentes**.

Cada fuente tiene sus particularidades, **Oanda.com** por ejemplo, proporciona datos historicos de 180 días, ¡aunque siempre se puede modificar el argumento de la función (from - to)!

https://finance.yahoo.com/?guccounter=1

https://www.alphavantage.co/

https://fred.stlouisfed.org/

https://www.oanda.com/rw-en/


Vamos a llamar a la API del  **Banco Central Europeo (BCE)** a traves del paquete de R **quandl()** para extraer la cotización del dollar con respecto al euro:




```r
# Import EURUSD data from BCE
eurusd<-Quandl(code="ECB/EURUSD")
```

El resultado que nos proporciona es el siguiente:

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Date </th>
   <th style="text-align:right;"> Value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 2020-12-07 </td>
   <td style="text-align:right;"> 1.2128 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020-12-04 </td>
   <td style="text-align:right;"> 1.2159 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020-12-03 </td>
   <td style="text-align:right;"> 1.2151 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020-12-02 </td>
   <td style="text-align:right;"> 1.2066 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020-12-01 </td>
   <td style="text-align:right;"> 1.1968 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020-11-30 </td>
   <td style="text-align:right;"> 1.1980 </td>
  </tr>
</tbody>
</table>

En empresas internacionales es comun operar con diferentes divisas y consolidar resultados en una moneda unica.

**Objetivo del analisis : analizar las ventas de las empresa en Euros**

Vamos a intentar automatizar este proceso con R y para ello tengo un **ejemplo** con 52.646 transacciones de una empresa que se dedica al transporte de pasajaeros urbanos y que opera en diferentes ciudades del mundo: Con euros, pesos mexicanos, pesos argentinos, chilenos..,




```
## [1] "EUR" "MXN" "BRL" "PEN" "ARS" "CLP" "USD"
```

Los datos que estamos explorando contienen mas variables de las que he seleccionado...

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> journey_id </th>
   <th style="text-align:left;"> created_at </th>
   <th style="text-align:left;"> currency </th>
   <th style="text-align:right;"> price_base </th>
   <th style="text-align:right;"> cost_base </th>
   <th style="text-align:left;"> ciudad </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 3b5ecd53ea384e6dabc8f3861636e9ff </td>
   <td style="text-align:left;"> 2017-12-17 00:20:33 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 1254 </td>
   <td style="text-align:right;"> 991 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 78456c6023f14e629a116e1764e938a8 </td>
   <td style="text-align:left;"> 2017-11-24 06:39:45 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 1179 </td>
   <td style="text-align:right;"> 955 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> aad8fe7a29774e0eb03c93e7271d47a7 </td>
   <td style="text-align:left;"> 2017-11-29 20:57:36 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 1500 </td>
   <td style="text-align:right;"> 1215 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 64bc20e94aa444e4844551cc83605c21 </td>
   <td style="text-align:left;"> 2017-11-10 20:43:56 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 600 </td>
   <td style="text-align:right;"> 486 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 249c56c03bef4c4cb988406f7314bb8c </td>
   <td style="text-align:left;"> 2017-12-14 22:02:20 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 550 </td>
   <td style="text-align:right;"> 434 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 360569767bf24d9bb84495760959eec7 </td>
   <td style="text-align:left;"> 2017-12-22 05:54:54 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 1078 </td>
   <td style="text-align:right;"> 852 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
</tbody>
</table>

Agrupamos las ventas de la compañia por mes...

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:right;"> month </th>
   <th style="text-align:left;"> sales </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:left;"> 2,147,525.0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:left;"> 8,296,543.0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> 12,540,979.0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> 8,920,553.0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:left;"> 12,063,367.0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> 13,269,868.0 </td>
  </tr>
</tbody>
</table>

...pero no es correcto, estamos mezclando diferentes divisas.

Aquí es donde viene lo importante de este proyecto...os detallo lo que vamos hacer paso por paso:

1) Preparamos una tabla de fechas


```r

currDF  <- data.frame(
  date = seq.Date(from = as.Date('2017-01-03 13:20:24'), to = as.Date('2017-12-30 09:54:08'), length = 52645),
  variable = datos$currency,
  amount = datos$price_base,stringsAsFactors=FALSE)


currDF = currDF %>% mutate(aniomes = paste(year(date),month(date)))

currDF$divisaaniomes<-paste(currDF$variable,currDF$aniomes)
```

2) Los datos que tenemos son del 2017, marcamos los limites y el formato de los datos


```r
#tipos de cambio historicos de 2017
startDt = as.Date("2017-01-03 13:20:24")
endDt = as.Date("2017-12-30 09:54:08")
currCombinations = paste(setdiff(unique(currDF$variable),"EUR"),"EUR=X",sep="")
```

3) Extraemos la cotiación de las divisas desde **yahoo** con la función **getSymbols()**. Y alimentamos la tabla.

Asegurarse de tener Internet al ejecutar este codigo.


```r
fxData = do.call(merge.xts,lapply(currCombinations,function(x)
  getSymbols.yahoo(x, src="yahoo", from=startDt,to=endDt,auto.assign=FALSE)[,4])) #make sure you have internet
colnames(fxData) = gsub("EUR.X.Close","",colnames(fxData))
fxData$EUR = 1
```

4) Calculamos la media de la cotización de cada divisa durante cada mez: **tipo de cambio medio de cada mes y de cada divisa**. (¡ojo! si el reporting es **anual**, podemos modificar la formula)


```r
fxData_DF = data.frame(date=index(fxData),coredata(fxData),stringsAsFactors=FALSE)
fxMolten = melt(fxData_DF,id="date",variable.name="currency",value.name="conversionFactor")

#creamos la columna aniomes para poder calcular el tipo de cambio medio de cada mes
fxMolten = fxMolten %>% mutate(aniomes = paste(year(date),month(date)))

fxMolten %>% group_by(aniomes, variable) %>% summarise(amountmedia = mean(value))
## # A tibble: 84 x 3
## # Groups:   aniomes [12]
##    aniomes variable amountmedia
##    <chr>   <fct>          <dbl>
##  1 2017 1  MXN          0.0439 
##  2 2017 1  BRL          0.294  
##  3 2017 1  PEN         NA      
##  4 2017 1  ARS          0.0591 
##  5 2017 1  CLP          0.00144
##  6 2017 1  USD          0.941  
##  7 2017 1  EUR          1      
##  8 2017 10 MXN          0.0452 
##  9 2017 10 BRL          0.266  
## 10 2017 10 PEN          0.266  
## # ... with 74 more rows
#eliminamos NAs
fxMolten<-fxMolten[complete.cases(fxMolten), ] #desaparecen algunas lineas
fxMolten %>% group_by(aniomes, variable) %>% summarise(amountmedia = mean(value))
## # A tibble: 79 x 3
## # Groups:   aniomes [12]
##    aniomes variable amountmedia
##    <chr>   <fct>          <dbl>
##  1 2017 1  MXN          0.0439 
##  2 2017 1  BRL          0.294  
##  3 2017 1  ARS          0.0591 
##  4 2017 1  CLP          0.00144
##  5 2017 1  USD          0.941  
##  6 2017 1  EUR          1      
##  7 2017 10 MXN          0.0452 
##  8 2017 10 BRL          0.266  
##  9 2017 10 PEN          0.266  
## 10 2017 10 ARS          0.0487 
## # ... with 69 more rows
#creamos la columna divisaaniomes para poder calcular el tipo de cambio medio de cada mes
fxMolten$divisaaniomes<-paste(fxMolten$variable,fxMolten$aniomes)
tipocamiomedio= fxMolten %>% group_by(divisaaniomes, variable) %>% summarise(amountmedia = mean(value))
#mergeamos con datoscabify
datos = datos %>% mutate(aniomes = paste(year(created_at),month(created_at)))
datos$divisaaniomes<-paste(datos$currency,datos$aniomes)
datosdivisa = merge(datos,tipocamiomedio, by= "divisaaniomes")
#hacemos la conversion de nuestras variables economicas
datosdivisa$price_base_EUR<-datosdivisa$price_base*datosdivisa$amountmedia
datosdivisa$cost_base_EUR<-datosdivisa$cost_base*datosdivisa$amountmedia

datos1 <- inner_join(datos,datosdivisa, by= "journey_id")
```

5) Incorporamos las columnas de coste y facturación en euros

<table class="table table-striped" style="font-size: 12px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> journey_id </th>
   <th style="text-align:left;"> created_at.x </th>
   <th style="text-align:left;"> currency.x </th>
   <th style="text-align:right;"> price_base.x </th>
   <th style="text-align:right;"> cost_base.x </th>
   <th style="text-align:right;"> price_base_EUR </th>
   <th style="text-align:right;"> cost_base_EUR </th>
   <th style="text-align:left;"> ciudad.x </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 3b5ecd53ea384e6dabc8f3861636e9ff </td>
   <td style="text-align:left;"> 2017-12-17 00:20:33 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 1254 </td>
   <td style="text-align:right;"> 991 </td>
   <td style="text-align:right;"> 1254 </td>
   <td style="text-align:right;"> 991 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 78456c6023f14e629a116e1764e938a8 </td>
   <td style="text-align:left;"> 2017-11-24 06:39:45 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 1179 </td>
   <td style="text-align:right;"> 955 </td>
   <td style="text-align:right;"> 1179 </td>
   <td style="text-align:right;"> 955 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> aad8fe7a29774e0eb03c93e7271d47a7 </td>
   <td style="text-align:left;"> 2017-11-29 20:57:36 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 1500 </td>
   <td style="text-align:right;"> 1215 </td>
   <td style="text-align:right;"> 1500 </td>
   <td style="text-align:right;"> 1215 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 64bc20e94aa444e4844551cc83605c21 </td>
   <td style="text-align:left;"> 2017-11-10 20:43:56 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 600 </td>
   <td style="text-align:right;"> 486 </td>
   <td style="text-align:right;"> 600 </td>
   <td style="text-align:right;"> 486 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 249c56c03bef4c4cb988406f7314bb8c </td>
   <td style="text-align:left;"> 2017-12-14 22:02:20 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 550 </td>
   <td style="text-align:right;"> 434 </td>
   <td style="text-align:right;"> 550 </td>
   <td style="text-align:right;"> 434 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 360569767bf24d9bb84495760959eec7 </td>
   <td style="text-align:left;"> 2017-12-22 05:54:54 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 1078 </td>
   <td style="text-align:right;"> 852 </td>
   <td style="text-align:right;"> 1078 </td>
   <td style="text-align:right;"> 852 </td>
   <td style="text-align:left;"> Madrid </td>
  </tr>
</tbody>
</table>

Ahora que tenemos los datos en euros, vuelvo agrupar los resultados de las ventas por mes


```r
#str(datosdivisa$created_at)

datos1$price_base_EUR[is.na(datos1$price_base_EUR)] <- 0

datos1$month <- month(datos1$created_at.x)


datos2 <- datos1 %>%
    # group by year and summarizing sales
    group_by(month) %>%
    summarize(sales = sum(price_base_EUR)) %>%
    ungroup()

datos2$sales <- format(round(as.numeric(datos2$sales), 1), nsmall=1, big.mark=",")

datos2%>%
    knitr::kable()%>%
    kable_styling(bootstrap_options = "striped", font_size = 14)
```

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:right;"> month </th>
   <th style="text-align:left;"> sales </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:left;"> 1,996,251.7 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:left;"> 6,946,050.0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> 9,241,637.4 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> 6,656,708.0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:left;"> 9,011,863.8 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> 10,326,851.0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:left;"> 10,132,739.2 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:left;"> 4,160,307.1 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:left;"> 9,956,338.7 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:left;"> 11,966,307.2 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:left;"> 11,838,035.0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 12 </td>
   <td style="text-align:left;"> 9,258,994.3 </td>
  </tr>
</tbody>
</table>

Estan facturando alrededor de 91 millones de euros anuales. Quiero ver las cifras por ciudades...



Parece que Madrid es una ciudad muy importante para la compañia...

![](images/proyectoVV-1.png)

Quiero ver como vende la empresa en Madrid semana a semana...



![](images/proyectoVVI-1.png)
