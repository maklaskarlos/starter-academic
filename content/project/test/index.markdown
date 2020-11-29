---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Tipos de cambio"
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
<script src="{{< relref "project/test/index.markdown" >}}index_files/kePrint-0.0.1/kePrint.js"></script>
<link href="{{< relref "project/test/index.markdown" >}}index_files/lightable-0.0.1/lightable.css" rel="stylesheet" />



En empresas internacionales es muy comun trabajar con divisas, pero cuando consolidas resultados contables lo haces con una moneda unica. Las divisas fluctuan y con el paso del tiempo pueden generar alteraciones en el balance, y por eso es muy importante tener un control sobre ellas.

Con R puedes generar una fuente de datos ecoconómicos donde tener controladas las fluctuaciones diarias, por horas o por minutos de cada una de las monedas con las que operas.

Entre las librerias mas utilizas para consultar datos económicos estan **quantmod** o **Quandl**.


```r
library(quantmod)
library(Quandl)
```



La función **getSymbols()** de la libreria **quantmod** permite capturar datos economicos de **distintas fuentes en internet**. Convierte el simbolo EUR/USD (donde EUR es la divisa base y el USD su cotización) a un simbolo valido para la extracción: **EURUSD**.


https://finance.yahoo.com/?guccounter=1

https://www.alphavantage.co/

https://fred.stlouisfed.org/

https://www.oanda.com/rw-en/

Cada fuente tiene sus particularidades, **Oanda.com** proporciona datos historicos de 180 días, aunque siempre se puede modificar el argumento de la función (from - to) e ir acumulando datos.

Con **quandl()** se puede extraer la cotización del dollar en el **Banco Central Europeo (BCE)** y generar un CSV.




```r
# Import EURUSD data from BCE
eurusd<-Quandl(code="ECB/EURUSD")
```

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Date </th>
   <th style="text-align:right;"> Value </th>
  </tr>
 </thead>
<tbody>
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
  <tr>
   <td style="text-align:left;"> 2020-11-24 </td>
   <td style="text-align:right;"> 1.1865 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020-11-23 </td>
   <td style="text-align:right;"> 1.1901 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020-11-20 </td>
   <td style="text-align:right;"> 1.1863 </td>
  </tr>
</tbody>
</table>

**Ejemplo** con 52.646 transacciones de una empresa que se dedica al transporte de pasajaeros y que opera en diferentes ciudades del mundo: En euros, pesos mexicanos, pesos argentinos, chilenos...

He seleccionado los siguientes campos para continuar en con el ejemplo:

- **journey_id**
- **created_at**
- **currency**
- **price_base**
- **cost_base**



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
   <td style="text-align:left;"> 6891256a326c4c22ba448e9d07dd6982 </td>
   <td style="text-align:left;"> 2017-05-14 09:19:47 </td>
   <td style="text-align:left;"> EUR </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.00 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> aa280d32bf2b4981902c9351eb1e54d0 </td>
   <td style="text-align:left;"> 2017-03-14 06:27:36 </td>
   <td style="text-align:left;"> MXN </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.00 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1e97cb74cfcb4c02938a561fd143e5da </td>
   <td style="text-align:left;"> 2017-03-14 16:34:46 </td>
   <td style="text-align:left;"> MXN </td>
   <td style="text-align:right;"> 45.50 </td>
   <td style="text-align:right;"> 36.40 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ec2bec2ffe46486c89f22d7a0026795f </td>
   <td style="text-align:left;"> 2017-03-15 02:24:57 </td>
   <td style="text-align:left;"> MXN </td>
   <td style="text-align:right;"> 37.45 </td>
   <td style="text-align:right;"> 22.46 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> d8b49fc3a0ce4b67a44e910017e63158 </td>
   <td style="text-align:left;"> 2017-03-15 06:32:41 </td>
   <td style="text-align:left;"> MXN </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.00 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 67d1a13aa7b24024892ffca4585a68e2 </td>
   <td style="text-align:left;"> 2017-04-17 02:13:29 </td>
   <td style="text-align:left;"> MXN </td>
   <td style="text-align:right;"> 40.00 </td>
   <td style="text-align:right;"> 32.00 </td>
  </tr>
</tbody>
</table>

Exploro los datos de las ventas con las divisas


```
##  POSIXct[1:52645], format: "2017-12-17 00:20:33" "2017-11-24 06:39:45" "2017-11-29 20:57:36" ...
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

No estamos calculando correctamente las ventas, se estan mezclando distintas divisas. Nuestro objetivo es tenerlas en €

A traves de **yahoo** y la función **getSymbols()** extraemos las cotizaciones. Asegurarse de tener Internet al ejecutar este codigo.


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


```r
#tipos de cambio historicos de 2017
startDt = as.Date("2017-01-03 13:20:24")
endDt = as.Date("2017-12-30 09:54:08")
currCombinations = paste(setdiff(unique(currDF$variable),"EUR"),"EUR=X",sep="")
```


```r
fxData = do.call(merge.xts,lapply(currCombinations,function(x)
  getSymbols.yahoo(x, src="yahoo", from=startDt,to=endDt,auto.assign=FALSE)[,4])) #make sure you have internet
colnames(fxData) = gsub("EUR.X.Close","",colnames(fxData))
fxData$EUR = 1
```

Para reportar estos resultados mensualmente, vamos a utilizar la media de las cotizaciones de cada divisa **tipo de cambio medio de cada mes y de cada divisa**.


```r
fxData_DF = data.frame(date=index(fxData),coredata(fxData),stringsAsFactors=FALSE)
fxMolten = melt(fxData_DF,id="date",variable.name="currency",value.name="conversionFactor")
```


```r
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


```r
datosdivisa = datosdivisa[,c("journey_id","created_at","currency","price_base","cost_base","price_base_EUR","cost_base_EUR")]
#visualizo nuestra nueva tabla
head(datosdivisa)%>%
  knitr::kable()%>%
  kable_styling(bootstrap_options = "striped", font_size = 14)
```

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
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
   <td style="text-align:left;"> 503495fb4eb5e78b009da9265a2f3cf6 </td>
   <td style="text-align:left;"> 2017-11-27 18:02:10 </td>
   <td style="text-align:left;"> ARS </td>
   <td style="text-align:right;"> 598.18 </td>
   <td style="text-align:right;"> 448.64 </td>
   <td style="text-align:right;"> 29.129463 </td>
   <td style="text-align:right;"> 21.847341 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 9abb868e3e57f04748d889b81b1102b2 </td>
   <td style="text-align:left;"> 2017-11-27 00:46:00 </td>
   <td style="text-align:left;"> ARS </td>
   <td style="text-align:right;"> 120.00 </td>
   <td style="text-align:right;"> 90.00 </td>
   <td style="text-align:right;"> 5.843618 </td>
   <td style="text-align:right;"> 4.382714 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> a575eb6697ea71b51aafd881b91b2068 </td>
   <td style="text-align:left;"> 2017-02-28 16:46:05 </td>
   <td style="text-align:left;"> ARS </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.000000 </td>
   <td style="text-align:right;"> 0.000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 339ed33ab68c455d9500a61e39e7a777 </td>
   <td style="text-align:left;"> 2017-02-28 23:07:12 </td>
   <td style="text-align:left;"> ARS </td>
   <td style="text-align:right;"> 112.92 </td>
   <td style="text-align:right;"> 84.69 </td>
   <td style="text-align:right;"> 6.794283 </td>
   <td style="text-align:right;"> 5.095713 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ca9e6cea8d249a134b812ca3a4d26908 </td>
   <td style="text-align:left;"> 2017-02-28 16:49:00 </td>
   <td style="text-align:left;"> ARS </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.000000 </td>
   <td style="text-align:right;"> 0.000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 740f9cbddb8b6d08f9ee5fbb3a1a631c </td>
   <td style="text-align:left;"> 2017-03-28 10:42:02 </td>
   <td style="text-align:left;"> ARS </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.000000 </td>
   <td style="text-align:right;"> 0.000000 </td>
  </tr>
</tbody>
</table>

Ahora que tenemos los datos en euros, vuelvo agrupar los resultados de las ventas por mes


```r
str(datosdivisa$created_at)
##  POSIXct[1:52260], format: "2017-11-27 18:02:10" "2017-11-27 00:46:00" "2017-02-28 16:46:05" ...

datosdivisa$month <- as.factor(months(as.Date(datosdivisa$created_at, "%Y/%m/%d",tz="UTC")))

datosdivisa$price_base_EUR[is.na(datosdivisa$price_base_EUR)] <- 0

datosdivisa %>%
    # group by year and summarizing sales
    group_by(month) %>%
    summarize(sales = sum(price_base_EUR)) %>%
    ungroup() %>%
    knitr::kable()%>%
    kable_styling(bootstrap_options = "striped", font_size = 14)
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
