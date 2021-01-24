---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Modelo para el analisis del riesgo de credito"
summary: ""
authors: []
tags: []
categories: []
date: 2021-01-24T21:20:55+01:00

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
<script src="{{< relref "es/project/riesgo-credito-modelo/index.markdown" >}}index_files/kePrint-0.0.1/kePrint.js"></script>
<link href="{{< relref "es/project/riesgo-credito-modelo/index.markdown" >}}index_files/lightable-0.0.1/lightable.css" rel="stylesheet" />

Una persona quiere comprar una vivienda que cuesta 500.000 euros, el "BORROWER", quien acude al "LENDER", el banco por lo general, quien le presta el 80% del valor de la vivienda. A esta proporción se le llama "LOAN TO VALUE".

LOAN AMOUNT = 500.000 * 80% = 400.000 USD.

Hasta la fecha el "BORROWER" ha pagado 40.00 euros, 


Importamos Pandas y NumPy...

```python
import numpy as np
import pandas as pd
```

...cargamos los datos descargados de un concurso de Kaggle...Datos de Loan Lending club (un market place de prestamos)...


```
## sys:1: DtypeWarning: Columns (20) have mixed types. Specify dtype option on import or set low_memory=False.
```



...visualizo las 10 primeras lineas...

```
##    Unnamed: 0       id  member_id  ...  inq_fi  total_cu_tl  inq_last_12m
## 0           0  1077501    1296599  ...     NaN          NaN           NaN
## 1           1  1077430    1314167  ...     NaN          NaN           NaN
## 2           2  1077175    1313524  ...     NaN          NaN           NaN
## 3           3  1076863    1277178  ...     NaN          NaN           NaN
## 4           4  1075358    1311748  ...     NaN          NaN           NaN
## 5           5  1075269    1311441  ...     NaN          NaN           NaN
## 6           6  1069639    1304742  ...     NaN          NaN           NaN
## 7           7  1072053    1288686  ...     NaN          NaN           NaN
## 8           8  1071795    1306957  ...     NaN          NaN           NaN
## 9           9  1071570    1306721  ...     NaN          NaN           NaN
## 
## [10 rows x 75 columns]
```

...pero quiero ver todas las columnas del dataset...



<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:right;"> Unnamed: 0 </th>
   <th style="text-align:right;"> id </th>
   <th style="text-align:right;"> member_id </th>
   <th style="text-align:right;"> loan_amnt </th>
   <th style="text-align:right;"> funded_amnt </th>
   <th style="text-align:right;"> funded_amnt_inv </th>
   <th style="text-align:left;"> term </th>
   <th style="text-align:right;"> int_rate </th>
   <th style="text-align:right;"> installment </th>
   <th style="text-align:left;"> grade </th>
   <th style="text-align:left;"> sub_grade </th>
   <th style="text-align:left;"> emp_title </th>
   <th style="text-align:left;"> emp_length </th>
   <th style="text-align:left;"> home_ownership </th>
   <th style="text-align:right;"> annual_inc </th>
   <th style="text-align:left;"> verification_status </th>
   <th style="text-align:left;"> issue_d </th>
   <th style="text-align:left;"> loan_status </th>
   <th style="text-align:left;"> pymnt_plan </th>
   <th style="text-align:left;"> url </th>
   <th style="text-align:left;"> desc </th>
   <th style="text-align:left;"> purpose </th>
   <th style="text-align:left;"> title </th>
   <th style="text-align:left;"> zip_code </th>
   <th style="text-align:left;"> addr_state </th>
   <th style="text-align:right;"> dti </th>
   <th style="text-align:right;"> delinq_2yrs </th>
   <th style="text-align:left;"> earliest_cr_line </th>
   <th style="text-align:right;"> inq_last_6mths </th>
   <th style="text-align:right;"> mths_since_last_delinq </th>
   <th style="text-align:right;"> mths_since_last_record </th>
   <th style="text-align:right;"> open_acc </th>
   <th style="text-align:right;"> pub_rec </th>
   <th style="text-align:right;"> revol_bal </th>
   <th style="text-align:right;"> revol_util </th>
   <th style="text-align:right;"> total_acc </th>
   <th style="text-align:left;"> initial_list_status </th>
   <th style="text-align:right;"> out_prncp </th>
   <th style="text-align:right;"> out_prncp_inv </th>
   <th style="text-align:right;"> total_pymnt </th>
   <th style="text-align:right;"> total_pymnt_inv </th>
   <th style="text-align:right;"> total_rec_prncp </th>
   <th style="text-align:right;"> total_rec_int </th>
   <th style="text-align:right;"> total_rec_late_fee </th>
   <th style="text-align:right;"> recoveries </th>
   <th style="text-align:right;"> collection_recovery_fee </th>
   <th style="text-align:left;"> last_pymnt_d </th>
   <th style="text-align:right;"> last_pymnt_amnt </th>
   <th style="text-align:left;"> next_pymnt_d </th>
   <th style="text-align:left;"> last_credit_pull_d </th>
   <th style="text-align:right;"> collections_12_mths_ex_med </th>
   <th style="text-align:right;"> mths_since_last_major_derog </th>
   <th style="text-align:right;"> policy_code </th>
   <th style="text-align:left;"> application_type </th>
   <th style="text-align:right;"> annual_inc_joint </th>
   <th style="text-align:right;"> dti_joint </th>
   <th style="text-align:right;"> verification_status_joint </th>
   <th style="text-align:right;"> acc_now_delinq </th>
   <th style="text-align:right;"> tot_coll_amt </th>
   <th style="text-align:right;"> tot_cur_bal </th>
   <th style="text-align:right;"> open_acc_6m </th>
   <th style="text-align:right;"> open_il_6m </th>
   <th style="text-align:right;"> open_il_12m </th>
   <th style="text-align:right;"> open_il_24m </th>
   <th style="text-align:right;"> mths_since_rcnt_il </th>
   <th style="text-align:right;"> total_bal_il </th>
   <th style="text-align:right;"> il_util </th>
   <th style="text-align:right;"> open_rv_12m </th>
   <th style="text-align:right;"> open_rv_24m </th>
   <th style="text-align:right;"> max_bal_bc </th>
   <th style="text-align:right;"> all_util </th>
   <th style="text-align:right;"> total_rev_hi_lim </th>
   <th style="text-align:right;"> inq_fi </th>
   <th style="text-align:right;"> total_cu_tl </th>
   <th style="text-align:right;"> inq_last_12m </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1077501 </td>
   <td style="text-align:right;"> 1296599 </td>
   <td style="text-align:right;"> 5000 </td>
   <td style="text-align:right;"> 5000 </td>
   <td style="text-align:right;"> 4975 </td>
   <td style="text-align:left;"> 36 months </td>
   <td style="text-align:right;"> 10.65 </td>
   <td style="text-align:right;"> 162.87 </td>
   <td style="text-align:left;"> B </td>
   <td style="text-align:left;"> B2 </td>
   <td style="text-align:left;"> NaN </td>
   <td style="text-align:left;"> 10+ years </td>
   <td style="text-align:left;"> RENT </td>
   <td style="text-align:right;"> 24000 </td>
   <td style="text-align:left;"> Verified </td>
   <td style="text-align:left;"> Dec-11 </td>
   <td style="text-align:left;"> Fully Paid </td>
   <td style="text-align:left;"> n </td>
   <td style="text-align:left;"> https://www.lendingclub.com/browse/loanDetail.action?loan_id=1077501 </td>
   <td style="text-align:left;"> Borrower added on 12/22/11 &gt; I need to upgrade my business technologies.&lt;br&gt; </td>
   <td style="text-align:left;"> credit_card </td>
   <td style="text-align:left;"> Computer </td>
   <td style="text-align:left;"> 860xx </td>
   <td style="text-align:left;"> AZ </td>
   <td style="text-align:right;"> 27.65 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> Jan-85 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 13648 </td>
   <td style="text-align:right;"> 83.7 </td>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:left;"> f </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 5861.071 </td>
   <td style="text-align:right;"> 5831.78 </td>
   <td style="text-align:right;"> 5000.00 </td>
   <td style="text-align:right;"> 861.07 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:left;"> Jan-15 </td>
   <td style="text-align:right;"> 171.62 </td>
   <td style="text-align:left;"> NaN </td>
   <td style="text-align:left;"> Jan-16 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:left;"> INDIVIDUAL </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 1077430 </td>
   <td style="text-align:right;"> 1314167 </td>
   <td style="text-align:right;"> 2500 </td>
   <td style="text-align:right;"> 2500 </td>
   <td style="text-align:right;"> 2500 </td>
   <td style="text-align:left;"> 60 months </td>
   <td style="text-align:right;"> 15.27 </td>
   <td style="text-align:right;"> 59.83 </td>
   <td style="text-align:left;"> C </td>
   <td style="text-align:left;"> C4 </td>
   <td style="text-align:left;"> Ryder </td>
   <td style="text-align:left;"> &lt; 1 year </td>
   <td style="text-align:left;"> RENT </td>
   <td style="text-align:right;"> 30000 </td>
   <td style="text-align:left;"> Source Verified </td>
   <td style="text-align:left;"> Dec-11 </td>
   <td style="text-align:left;"> Charged Off </td>
   <td style="text-align:left;"> n </td>
   <td style="text-align:left;"> https://www.lendingclub.com/browse/loanDetail.action?loan_id=1077430 </td>
   <td style="text-align:left;"> Borrower added on 12/22/11 &gt; I plan to use this money to finance the motorcycle i am looking at. I plan to have it paid off as soon as possible/when i sell my old bike. I only need this money because the deal im looking at is to good to pass up.&lt;br&gt;&lt;br&gt;  Borrower added on 12/22/11 &gt; I plan to use this money to finance the motorcycle i am looking at. I plan to have it paid off as soon as possible/when i sell my old bike.I only need this money because the deal im looking at is to good to pass up. I have finished college with an associates degree in business and its takingmeplaces&lt;br&gt; </td>
   <td style="text-align:left;"> car </td>
   <td style="text-align:left;"> bike </td>
   <td style="text-align:left;"> 309xx </td>
   <td style="text-align:left;"> GA </td>
   <td style="text-align:right;"> 1.00 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> Apr-99 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1687 </td>
   <td style="text-align:right;"> 9.4 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> f </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1008.710 </td>
   <td style="text-align:right;"> 1008.71 </td>
   <td style="text-align:right;"> 456.46 </td>
   <td style="text-align:right;"> 435.17 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 117.08 </td>
   <td style="text-align:right;"> 1.11 </td>
   <td style="text-align:left;"> Apr-13 </td>
   <td style="text-align:right;"> 119.66 </td>
   <td style="text-align:left;"> NaN </td>
   <td style="text-align:left;"> Sep-13 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:left;"> INDIVIDUAL </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
   <td style="text-align:right;"> NaN </td>
  </tr>
</tbody>
</table>
