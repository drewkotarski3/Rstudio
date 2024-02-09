Lab 04 - La Quinta is Spanish for next to Denny’s
================
Group 6
3/2/22

### Load packages and data

``` r
dennys <- readRDS("data/dennys.RData")
laquinta <- readRDS("data/laquinta.RData")
```

``` r
library(tidyverse) 
```

    ## Warning: package 'tidyverse' was built under R version 4.0.5

    ## Warning: package 'ggplot2' was built under R version 4.0.5

    ## Warning: package 'tibble' was built under R version 4.0.5

    ## Warning: package 'tidyr' was built under R version 4.0.5

    ## Warning: package 'readr' was built under R version 4.0.5

    ## Warning: package 'purrr' was built under R version 4.0.5

    ## Warning: package 'dplyr' was built under R version 4.0.5

    ## Warning: package 'stringr' was built under R version 4.0.5

    ## Warning: package 'forcats' was built under R version 4.0.5

``` r
#library(dsbox) 
```

``` r
states <- read_csv("data/states.csv")
```

### Exercise 1

There are 1643 observations and 6 variables in the dataset. Each row
represents a Dennys restaurant. The variables are address, city, state,
zip code, longitude and latitude.

### Exercise 2

There are 909 observations and 6 variables. Each row represents one
hotel location. The variables are address, city, state, zip code,
longitude, and latitude.

### Exercise 3

``` r
glimpse(dennys)
```

    ## Rows: 1,643
    ## Columns: 6
    ## $ address   <chr> "2900 Denali", "3850 Debarr Road", "1929 Airport Way", "230 ~
    ## $ city      <chr> "Anchorage", "Anchorage", "Fairbanks", "Auburn", "Birmingham~
    ## $ state     <chr> "AK", "AK", "AK", "AL", "AL", "AL", "AL", "AL", "AL", "AL", ~
    ## $ zip       <chr> "99503", "99508", "99701", "36849", "35207", "35294", "35056~
    ## $ longitude <dbl> -149.8767, -149.8090, -147.7600, -85.4681, -86.8317, -86.803~
    ## $ latitude  <dbl> 61.1953, 61.2097, 64.8366, 32.6033, 33.5615, 33.5007, 34.206~

There are locations for both Laquinta and Dennys that are not in the us.
La Quinta: Canada, Mexico, China, Turkey, Chile, Honduras, New Zealand,
Arab Emirates Dennys: Canada

### Exercise 4

``` r
glimpse(dennys)
```

    ## Rows: 1,643
    ## Columns: 6
    ## $ address   <chr> "2900 Denali", "3850 Debarr Road", "1929 Airport Way", "230 ~
    ## $ city      <chr> "Anchorage", "Anchorage", "Fairbanks", "Auburn", "Birmingham~
    ## $ state     <chr> "AK", "AK", "AK", "AL", "AL", "AL", "AL", "AL", "AL", "AL", ~
    ## $ zip       <chr> "99503", "99508", "99701", "36849", "35207", "35294", "35056~
    ## $ longitude <dbl> -149.8767, -149.8090, -147.7600, -85.4681, -86.8317, -86.803~
    ## $ latitude  <dbl> 61.1953, 61.2097, 64.8366, 32.6033, 33.5615, 33.5007, 34.206~

``` r
glimpse(laquinta)
```

    ## Rows: 909
    ## Columns: 6
    ## $ address   <chr> "793 W. Bel Air Avenue", "3018 CatClaw Dr", "3501 West Lake ~
    ## $ city      <chr> "\nAberdeen", "\nAbilene", "\nAbilene", "\nAcworth", "\nAda"~
    ## $ state     <chr> "MD", "TX", "TX", "GA", "OK", "TX", "AG", "TX", "NM", "NM", ~
    ## $ zip       <chr> "21001", "79606", "79601", "30102", "74820", "75254", "20345~
    ## $ longitude <dbl> -76.18846, -99.77877, -99.72269, -84.65609, -96.63652, -96.8~
    ## $ latitude  <dbl> 39.52322, 32.41349, 32.49136, 34.08204, 34.78180, 32.95164, ~

We could try looking at states, zip codes, longitudes and latitudes to
determine if the companies are outside of the United States.

### Exercise 5

``` r
dn <- dennys 
lq <- laquinta
```

``` r
dn %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 0 x 6
    ## # ... with 6 variables: address <chr>, city <chr>, state <chr>, zip <chr>,
    ## #   longitude <dbl>, latitude <dbl>

### Exercise 6

…

### Exercise 7

``` r
laquinta %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 14 x 6
    ##    address                     city               state zip   longitude latitude
    ##    <chr>                       <chr>              <chr> <chr>     <dbl>    <dbl>
    ##  1 Carretera Panamericana Sur~ "\nAguascalientes" AG    20345    -102.     21.8 
    ##  2 Av. Tulum Mza. 14 S.M. 4 L~ "\nCancun"         QR    77500     -86.8    21.2 
    ##  3 Ejercito Nacional 8211      "Col\nPartido Igl~ CH    32528    -106.     31.7 
    ##  4 Blvd. Aeropuerto 4001       "Parque Industria~ NL    66600    -100.     25.8 
    ##  5 Carrera 38 # 26-13 Avenida~ "\nMedellin Colom~ ANT   0500~     -75.6     6.22
    ##  6 AV. PINO SUAREZ No. 1001    "Col. Centro\nMon~ NL    64000    -100.     25.7 
    ##  7 Av. Fidel Velazquez #3000 ~ "\nMonterrey"      NL    64190    -100.     25.7 
    ##  8 63 King Street East         "\nOshawa"         ON    L1H1~     -78.9    43.9 
    ##  9 Calle Las Torres-1 Colonia~ "\nPoza Rica"      VE    93210     -97.4    20.6 
    ## 10 Blvd. Audi N. 3 Ciudad Mod~ "\nSan Jose Chiap~ PU    75010     -97.8    19.2 
    ## 11 Ave. Zeta del Cochero No 4~ "Col. ReservaTerr~ PU    72810     -98.2    19.0 
    ## 12 Av. Benito Juarez 1230 B (~ "\nSan Luis Potos~ SL    78399    -101.     22.1 
    ## 13 Blvd. Fuerza Armadas        "contiguo Mall La~ FM    11101     -87.2    14.1 
    ## 14 8640 Alexandra Rd           "\nRichmond"       BC    V6X1~    -123.     49.2
