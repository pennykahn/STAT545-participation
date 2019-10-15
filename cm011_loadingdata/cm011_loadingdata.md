---
title: "Cm011: Reading and Writing Data"
author: "Penny Kahn"
output: 
  html_document:
    keep_md: TRUE
---


```r
library(tidyverse)
```

```
## ── Attaching packages ───────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──
```

```
## ✔ ggplot2 3.2.1     ✔ purrr   0.3.2
## ✔ tibble  2.1.3     ✔ dplyr   0.8.3
## ✔ tidyr   1.0.0     ✔ stringr 1.4.0
## ✔ readr   1.3.1     ✔ forcats 0.4.0
```

```
## ── Conflicts ──────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(gapminder)
library(here)
```

```
## here() starts at /Users/pcbkahn/Documents/git_docs/STAT545-participation
```

```r
library(readxl)
```

Loading in a file with url. If file was a csv, you can do it directly with read_csv, but since its an xcel file, you need to download it first

```r
data_url <- "http://gattonweb.uky.edu/sheather/book/docs/datasets/GreatestGivers.xls"

download.file(url = data_url, destfile = here("test", "GreatestGivers.xls"))

file_name <- basename(data_url)

philanthropists <- read_excel(here("test", file_name), trim_ws =TRUE)

philanthropists
```

```
## # A tibble: 50 x 8
##    Rank  Name  Background `2003-07 Given … Causes `Estimated lift…
##    <chr> <chr> <chr>      <chr>            <chr>             <dbl>
##  1 1     Warr… Berkshire…  40,650          Healt…            40780
##  2 2     Bill… Microsoft…  3,519           Globa…            28144
##  3 3     Geor… Oil and g…  2,271           Pover…             2522
##  4 4     Geor… Investor    2,109           Open …             6401
##  5 5     Gord… Intel co-…  2,067           Envir…             7404
##  6 6     Walt… Family of…  1,475           Educa…             2015
##  7 7     Herb… Golden We…  1,368           Medic…             1389
##  8 8     Eli … SunAmeric…  1,216           Publi…             2286
##  9 9     Dona… Real esta…  915             Educa…             1326
## 10 10    Jon … Huntsman …  800             Cance…             1233
## # … with 40 more rows, and 2 more variables: `Net Worth` <chr>,
## #   `Giving%` <chr>
```


```r
data_url <- "https://github.com/STAT545-UBC-hw-2019-20/Announcements/files/3703782/Firas-MRI.xlsx"

file_name <- basename(data_url)

download.file(url = data_url, destfile = here("test", file_name))

mri <- read_excel(here("test", file_name), trim_ws =TRUE, range = "A1:L12")

mri
```

```
## # A tibble: 11 x 12
##    `Animal ID` `Slice 1` `Slice 2` `Slice 3` `Slice 4` `Slice 5` `Slice 6`
##    <chr>           <dbl>     <dbl>     <dbl>     <dbl>     <dbl>     <dbl>
##  1 HerS18Bs01…    11.1       14.7      16.5      14.3     18.9       22.5 
##  2 HerS18Bs02…    10.3        7.90      7.29      6.28    11.8       12.4 
##  3 HerS18Bs03…     8.20       6.49      5.93      7.54     8.51       7.41
##  4 HerS18Bs04…     9.22       5.72      7.23      6.71     6.67       5.52
##  5 HerS18Bs05…     8.07       8.70      7.66      6.51     6.61       6.81
##  6 HerS18Bs06…     1.85       5.80      5.33      3.57     4.40       5.51
##  7 HerS18Bs07…     4.48       3.89      3.35      5.27     5.36       6.12
##  8 HerS18Bs08…    18.0       17.4      17.7      13.9     16.9       15.6 
##  9 HerS18Bs09…     9.53       7.09      7.82      7.15     4.61       6.76
## 10 HerS18Bs11…    20.4       10.2       6.53      5.71     7.80       7.68
## 11 HerS18Bs12…     0.131      2.49      3.75      1.26     0.882      2.46
## # … with 5 more variables: `Slice 7` <dbl>, `Slice 8` <dbl>, `Weighted
## #   Average` <dbl>, Volume <dbl>, `Treatment Group` <chr>
```


```r
mri <- mri[, -10]

mri
```

```
## # A tibble: 11 x 11
##    `Animal ID` `Slice 1` `Slice 2` `Slice 3` `Slice 4` `Slice 5` `Slice 6`
##    <chr>           <dbl>     <dbl>     <dbl>     <dbl>     <dbl>     <dbl>
##  1 HerS18Bs01…    11.1       14.7      16.5      14.3     18.9       22.5 
##  2 HerS18Bs02…    10.3        7.90      7.29      6.28    11.8       12.4 
##  3 HerS18Bs03…     8.20       6.49      5.93      7.54     8.51       7.41
##  4 HerS18Bs04…     9.22       5.72      7.23      6.71     6.67       5.52
##  5 HerS18Bs05…     8.07       8.70      7.66      6.51     6.61       6.81
##  6 HerS18Bs06…     1.85       5.80      5.33      3.57     4.40       5.51
##  7 HerS18Bs07…     4.48       3.89      3.35      5.27     5.36       6.12
##  8 HerS18Bs08…    18.0       17.4      17.7      13.9     16.9       15.6 
##  9 HerS18Bs09…     9.53       7.09      7.82      7.15     4.61       6.76
## 10 HerS18Bs11…    20.4       10.2       6.53      5.71     7.80       7.68
## 11 HerS18Bs12…     0.131      2.49      3.75      1.26     0.882      2.46
## # … with 4 more variables: `Slice 7` <dbl>, `Slice 8` <dbl>, Volume <dbl>,
## #   `Treatment Group` <chr>
```


```r
mri_long <- mri %>% 
  pivot_longer(cols = `Slice 1`:`Slice 8`,
               names_to = "slice_no",
               values_to = "value")

mri_long
```

```
## # A tibble: 88 x 5
##    `Animal ID`      Volume `Treatment Group` slice_no value
##    <chr>             <dbl> <chr>             <chr>    <dbl>
##  1 HerS18Bs01.BS1/8   523. Avastin           Slice 1  11.1 
##  2 HerS18Bs01.BS1/8   523. Avastin           Slice 2  14.7 
##  3 HerS18Bs01.BS1/8   523. Avastin           Slice 3  16.5 
##  4 HerS18Bs01.BS1/8   523. Avastin           Slice 4  14.3 
##  5 HerS18Bs01.BS1/8   523. Avastin           Slice 5  18.9 
##  6 HerS18Bs01.BS1/8   523. Avastin           Slice 6  22.5 
##  7 HerS18Bs01.BS1/8   523. Avastin           Slice 7  19.0 
##  8 HerS18Bs01.BS1/8   523. Avastin           Slice 8  18.8 
##  9 HerS18Bs02.BS1/7   400. Herceptin         Slice 1  10.3 
## 10 HerS18Bs02.BS1/7   400. Herceptin         Slice 2   7.90
## # … with 78 more rows
```








