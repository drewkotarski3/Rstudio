Lab 03 - Nobel laureates
================
Team 6
2/16/22

### Load packages and data

``` r
library(tidyverse) 
```

``` r
nobel <- read_csv("data/nobel.csv")
```

## Exercises

### Exercise 1

There are 935 observations and 26 variables in the dataset. Each row
represents a laureate.

### Exercise 2

``` r
nobel_living <- nobel %>%
  filter(!is.na(country)) %>%
  filter(gender!="org") %>%
  filter(is.na(died_date))
```

The data frame nobel\_living contains 228 observations.

### Modify nobel\_living dataframe

``` r
nobel_living <- nobel_living %>%
  mutate(
    country_us = if_else(country == "USA", "USA", "Other")
  )
```

``` r
nobel_living_science <- nobel_living %>%
  filter(category %in% c("Physics", "Medicine", "Chemistry", "Economics"))
```

The data frame nobel\_living\_science contains Nobel laureates in the
areas of physics, medicine, chemistry and economics classified into “US”
or “other”.

### Exercise 3

Parts of the Buzzfeed headline are supported by the data. There were
more Nobel laureates based inside the USA than outside the USA when they
won their prizes, however, we cannot tell from this visualization
whether or not the laureates immigrated to the USA or were born here.

``` r
ggplot(nobel_living_science, 
       aes(x= country_us)) +
  geom_bar()+
  coord_flip()+
  facet_wrap(~category) +
  labs(y="Count",x="Country of laureate in prize year")
```

![](lab-03_files/figure-gfm/barplot-1.png)<!-- -->

### Exercise 4

``` r
nobel_living_science <- nobel_living_science %>%
  mutate(born_country_us = if_else(born_country == "USA", "USA", "Other"))
```

105 of the living laureates in the categories Physics, Medicine,
Chemistry and Economics were born in the US.

### Exercise 5

…

### Exercise 6

…
