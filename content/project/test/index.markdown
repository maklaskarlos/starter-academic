---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Reporting de ventas con R"
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
library(kableExtra)
library(lubridate)
library(ggplot2)
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
  <tr>
   <td style="text-align:left;"> 2020-11-27 </td>
   <td style="text-align:right;"> 1.1922 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020-11-26 </td>
   <td style="text-align:right;"> 1.1900 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020-11-25 </td>
   <td style="text-align:right;"> 1.1890 </td>
  </tr>
</tbody>
</table>

En empresas internacionales es comun operar con diferentes divisas y consolidar resultados en una moneda unica. 

Vamos a intentar automatizar este proceso con R y para ello tengo un **ejemplo** con 52.646 transacciones de una empresa que se dedica al transporte de pasajaeros urbanos y que opera en diferentes ciudades del mundo: Con euros, pesos mexicanos, pesos argentinos, chilenos..,




```
## [1] "EUR" "MXN" "BRL" "PEN" "ARS" "CLP" "USD"
```

**Objetivo del analisis : analizar las ventas totales de las empresa en Euros y por mes**

Los datos que estamos explorando contienen mas variables de las que he seleccionado...

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> journey_id </th>
   <th style="text-align:left;"> created_at </th>
   <th style="text-align:left;"> currency </th>
   <th style="text-align:right;"> price_base </th>
   <th style="text-align:right;"> cost_base </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 3b5ecd53ea384e6dabc8f3861636e9ff </td>
   <td style="text-align:left;"> 2017-12-17 00:20:33 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 12.54 </td>
   <td style="text-align:right;"> 9.91 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 78456c6023f14e629a116e1764e938a8 </td>
   <td style="text-align:left;"> 2017-11-24 06:39:45 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 11.79 </td>
   <td style="text-align:right;"> 9.55 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> aad8fe7a29774e0eb03c93e7271d47a7 </td>
   <td style="text-align:left;"> 2017-11-29 20:57:36 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 15.00 </td>
   <td style="text-align:right;"> 12.15 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 64bc20e94aa444e4844551cc83605c21 </td>
   <td style="text-align:left;"> 2017-11-10 20:43:56 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 6.00 </td>
   <td style="text-align:right;"> 4.86 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 249c56c03bef4c4cb988406f7314bb8c </td>
   <td style="text-align:left;"> 2017-12-14 22:02:20 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 5.50 </td>
   <td style="text-align:right;"> 4.34 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 360569767bf24d9bb84495760959eec7 </td>
   <td style="text-align:left;"> 2017-12-22 05:54:54 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 10.78 </td>
   <td style="text-align:right;"> 8.52 </td>
  </tr>
</tbody>
</table>

Agrupamos las ventas de la compañia por mes...

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> month </th>
   <th style="text-align:right;"> sales </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> abril </td>
   <td style="text-align:right;"> 403777.04 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> agosto </td>
   <td style="text-align:right;"> 64653.74 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> diciembre </td>
   <td style="text-align:right;"> 98649.10 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> enero </td>
   <td style="text-align:right;"> 21475.25 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> febrero </td>
   <td style="text-align:right;"> 141537.79 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> julio </td>
   <td style="text-align:right;"> 126498.25 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> junio </td>
   <td style="text-align:right;"> 307498.03 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> marzo </td>
   <td style="text-align:right;"> 125409.79 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> mayo </td>
   <td style="text-align:right;"> 404743.87 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> noviembre </td>
   <td style="text-align:right;"> 140369.43 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> octubre </td>
   <td style="text-align:right;"> 185126.07 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> septiembre </td>
   <td style="text-align:right;"> 159458.37 </td>
  </tr>
</tbody>
</table>

... pero no es lo correcto por que estamos mezclando diferentes divisas.

Aquí es donde viene lo importante de este proyecto...os detallo lo que vamos hacer paso por paso: 

1) Preparamos una tabla de fechas


```r
library(lubridate)
library(reshape)

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
```

5) Incorporamos las columnas de coste y facturación en euros

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:left;"> journey_id </th>
   <th style="text-align:left;"> created_at </th>
   <th style="text-align:left;"> currency </th>
   <th style="text-align:right;"> price_base </th>
   <th style="text-align:right;"> cost_base </th>
   <th style="text-align:right;"> price_base_EUR </th>
   <th style="text-align:right;"> cost_base_EUR </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 52255 </td>
   <td style="text-align:left;"> bf9362f0d7b6892e76c69fe098ef1c93 </td>
   <td style="text-align:left;"> 2017-07-21 01:46:20 </td>
   <td style="text-align:left;"> USD </td>
   <td style="text-align:right;"> 5.87 </td>
   <td style="text-align:right;"> 4.40 </td>
   <td style="text-align:right;"> 5.095841 </td>
   <td style="text-align:right;"> 3.819710 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 52256 </td>
   <td style="text-align:left;"> 42f2707ecd5af8179ff0cd6205d82c80 </td>
   <td style="text-align:left;"> 2017-07-25 00:44:49 </td>
   <td style="text-align:left;"> USD </td>
   <td style="text-align:right;"> 2.12 </td>
   <td style="text-align:right;"> 1.59 </td>
   <td style="text-align:right;"> 1.840406 </td>
   <td style="text-align:right;"> 1.380304 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 52257 </td>
   <td style="text-align:left;"> 3053fe92a9f227506566bf9f84c4b018 </td>
   <td style="text-align:left;"> 2017-07-28 13:52:15 </td>
   <td style="text-align:left;"> USD </td>
   <td style="text-align:right;"> 3.06 </td>
   <td style="text-align:right;"> 2.30 </td>
   <td style="text-align:right;"> 2.656435 </td>
   <td style="text-align:right;"> 1.996667 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 52258 </td>
   <td style="text-align:left;"> ba40e1bcd73099db808f1148161613ed </td>
   <td style="text-align:left;"> 2017-07-24 05:17:34 </td>
   <td style="text-align:left;"> USD </td>
   <td style="text-align:right;"> 23.80 </td>
   <td style="text-align:right;"> 17.85 </td>
   <td style="text-align:right;"> 20.661161 </td>
   <td style="text-align:right;"> 15.495871 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 52259 </td>
   <td style="text-align:left;"> bd67e2870da4726d52653d4089b28155 </td>
   <td style="text-align:left;"> 2017-07-28 18:49:07 </td>
   <td style="text-align:left;"> USD </td>
   <td style="text-align:right;"> 2.67 </td>
   <td style="text-align:right;"> 2.00 </td>
   <td style="text-align:right;"> 2.317870 </td>
   <td style="text-align:right;"> 1.736232 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 52260 </td>
   <td style="text-align:left;"> 12028aeaff88f8a3b3a26f58843fd1ce </td>
   <td style="text-align:left;"> 2017-07-21 00:34:38 </td>
   <td style="text-align:left;"> USD </td>
   <td style="text-align:right;"> 2.84 </td>
   <td style="text-align:right;"> 2.13 </td>
   <td style="text-align:right;"> 2.465449 </td>
   <td style="text-align:right;"> 1.849087 </td>
  </tr>
</tbody>
</table>

Ahora que tenemos los datos en euros, vuelvo agrupar los resultados de las ventas por mes


```
##  POSIXct[1:52260], format: "2017-11-27 18:02:10" "2017-11-27 00:46:00" "2017-02-28 16:46:05" ...
```

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> month </th>
   <th style="text-align:right;"> sales </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> abril </td>
   <td style="text-align:right;"> 67016.56 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> agosto </td>
   <td style="text-align:right;"> 41613.92 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> diciembre </td>
   <td style="text-align:right;"> 92589.94 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> enero </td>
   <td style="text-align:right;"> 19962.52 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> febrero </td>
   <td style="text-align:right;"> 69546.10 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> julio </td>
   <td style="text-align:right;"> 101327.39 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> junio </td>
   <td style="text-align:right;"> 103503.54 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> marzo </td>
   <td style="text-align:right;"> 92416.37 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> mayo </td>
   <td style="text-align:right;"> 90503.38 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> noviembre </td>
   <td style="text-align:right;"> 118380.35 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> octubre </td>
   <td style="text-align:right;"> 119723.05 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> septiembre </td>
   <td style="text-align:right;"> 99612.91 </td>
  </tr>
</tbody>
</table>

Y podría dibujar un grafico:

