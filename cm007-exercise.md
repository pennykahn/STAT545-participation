---
title: "cm007 Exercises: Practice with `dplyr`"
output: 
  html_document:
    keep_md: true
    theme: paper
---

<!---The following chunk allows errors when knitting--->




```r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(gapminder))
suppressPackageStartupMessages(library(tsibble))
library(DT)
```


This worksheet contains exercises aimed for practice with `dplyr`. 


1. (a) What's the minimum life expectancy for each continent and each year? (b) Add the corresponding country to the tibble, too. (c) Arrange by min life expectancy.

1a.

```r
gapminder %>% 
  group_by(continent, year) %>% 
  summarize(min_life = min(lifeExp))
```

```
## # A tibble: 60 x 3
## # Groups:   continent [5]
##    continent  year min_life
##    <fct>     <int>    <dbl>
##  1 Africa     1952     30  
##  2 Africa     1957     31.6
##  3 Africa     1962     32.8
##  4 Africa     1967     34.1
##  5 Africa     1972     35.4
##  6 Africa     1977     36.8
##  7 Africa     1982     38.4
##  8 Africa     1987     39.9
##  9 Africa     1992     23.6
## 10 Africa     1997     36.1
## # … with 50 more rows
```
1b.

```r
gapminder %>% 
  group_by(continent, year) %>% 
  summarize(min_life = min(lifeExp),
            country = country[lifeExp==min_life])
```

```
## # A tibble: 60 x 4
## # Groups:   continent [5]
##    continent  year min_life country     
##    <fct>     <int>    <dbl> <fct>       
##  1 Africa     1952     30   Gambia      
##  2 Africa     1957     31.6 Sierra Leone
##  3 Africa     1962     32.8 Sierra Leone
##  4 Africa     1967     34.1 Sierra Leone
##  5 Africa     1972     35.4 Sierra Leone
##  6 Africa     1977     36.8 Sierra Leone
##  7 Africa     1982     38.4 Sierra Leone
##  8 Africa     1987     39.9 Angola      
##  9 Africa     1992     23.6 Rwanda      
## 10 Africa     1997     36.1 Rwanda      
## # … with 50 more rows
```
1c.

```r
gapminder %>% 
  group_by(continent, year) %>% 
  summarize(min_life = min(lifeExp),
            country = country[lifeExp==min_life]) %>% 
  arrange(min_life)
```

```
## # A tibble: 60 x 4
## # Groups:   continent [5]
##    continent  year min_life country     
##    <fct>     <int>    <dbl> <fct>       
##  1 Africa     1992     23.6 Rwanda      
##  2 Asia       1952     28.8 Afghanistan 
##  3 Africa     1952     30   Gambia      
##  4 Asia       1957     30.3 Afghanistan 
##  5 Asia       1977     31.2 Cambodia    
##  6 Africa     1957     31.6 Sierra Leone
##  7 Asia       1962     32.0 Afghanistan 
##  8 Africa     1962     32.8 Sierra Leone
##  9 Asia       1967     34.0 Afghanistan 
## 10 Africa     1967     34.1 Sierra Leone
## # … with 50 more rows
```


2. Calculate the growth in population since the first year on record _for each country_ by rearranging the following lines, and filling in the `FILL_THIS_IN`. Here's another convenience function for you: `dplyr::first()`. 

```
mutate(rel_growth = FILL_THIS_IN) %>% 
arrange(FILL_THIS_IN) %>% 
gapminder %>% 
DT::datatable()
group_by(country) %>% 
```


```r
gapminder %>%
  group_by(country) %>% 
  arrange(year) %>%
  mutate(rel_growth = pop - first(pop))# %>% 
```

```
## # A tibble: 1,704 x 7
## # Groups:   country [142]
##    country     continent  year lifeExp      pop gdpPercap rel_growth
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>      <int>
##  1 Afghanistan Asia       1952    28.8  8425333      779.          0
##  2 Albania     Europe     1952    55.2  1282697     1601.          0
##  3 Algeria     Africa     1952    43.1  9279525     2449.          0
##  4 Angola      Africa     1952    30.0  4232095     3521.          0
##  5 Argentina   Americas   1952    62.5 17876956     5911.          0
##  6 Australia   Oceania    1952    69.1  8691212    10040.          0
##  7 Austria     Europe     1952    66.8  6927772     6137.          0
##  8 Bahrain     Asia       1952    50.9   120447     9867.          0
##  9 Bangladesh  Asia       1952    37.5 46886859      684.          0
## 10 Belgium     Europe     1952    68    8730405     8343.          0
## # … with 1,694 more rows
```

```r
  #DT::datatable()
```


3. Determine the country that experienced the sharpest 5-year drop in life expectancy, in each continent, sorted by the drop, by rearranging the following lines of code. Ensure there are no `NA`'s. Instead of using `lag()`, use the convenience function provided by the `tsibble` package, `tsibble::difference()`:

```
drop_na() %>% 
ungroup() %>% 
arrange(year) %>% 
filter(inc_life_exp == min(inc_life_exp)) %>% 
gapminder %>% 
mutate(inc_life_exp = FILL_THIS_IN) %>% 
arrange(inc_life_exp) %>% 
group_by(country) %>% 
group_by(continent) %>% 
knitr::kable()
```


```r
gapminder %>% 
  group_by(country) %>%
  arrange(year) %>% 
  mutate(inc_life_exp = difference(lifeExp)) %>%
  drop_na() %>% 
  ungroup() %>% 
  group_by(continent) %>% 
  filter(inc_life_exp == min(inc_life_exp)) %>% 
  arrange(inc_life_exp)# %>% 
```

```
## # A tibble: 5 x 7
## # Groups:   continent [5]
##   country     continent  year lifeExp      pop gdpPercap inc_life_exp
##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>        <dbl>
## 1 Rwanda      Africa     1992    23.6  7290203      737.      -20.4  
## 2 Cambodia    Asia       1977    31.2  6978607      525.       -9.10 
## 3 El Salvador Americas   1977    56.7  4282586     5139.       -1.51 
## 4 Montenegro  Europe     2002    74.0   720230     6557.       -1.46 
## 5 Australia   Oceania    1967    71.1 11872264    14526.        0.170
```

```r
  #knitr::kable()
```
