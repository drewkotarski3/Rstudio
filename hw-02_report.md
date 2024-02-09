HW 02 - Airbnb listings in Boston
================
Andrew Kotarski
02/16/2022

## Load packages and data

``` r
library(tidyverse) # load in the tidyverse suite of packages
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
library(ggridges)
```

    ## Warning: package 'ggridges' was built under R version 4.0.5

``` r
# below, we load in the data from a subdirectory
# note that when we use `::`, we are telling R to use package::function
# (we are specifying the package to pull this function from)
boston_airBnB <- readr::read_csv(file = "data/boston_airBnB_data.csv") 
```

## Exercises

### Exercise 1

There are 1969 rows of data

### Exercise 2

``` r
view(boston_airBnB)
names(boston_airBnB)
```

The rows of the data represent an observation. id, price, neighborhood,
accommodates, bathrooms, bedrooms, beds, review\_scores\_rating,
number\_of\_reviews, listing\_url \#\#\# Exercise 3 {
glimpse(boston\_airBnB) } Remove this text, and add your answer for
Exercise 3 here.

``` r
# Create a faceted histogram where each facet represents a neighborhood and displays the distribution of Airbnb prices in that neighborhood. Think critically about whether it makes more sense to stack the facets on top of each other in a column, lay them out in a row, or wrap them around. Along with your visualization, include your reasoning for the layout you chose for your facets.
ggplot(data = boston_airBnB, mapping = aes(x = price )) +
  geom_histogram(binwidth = 30) +
  facet_wrap(~neighborhood, scales = "free")
```

![](hw-02_report_files/figure-gfm/prices-neighborhoods-1.png)<!-- -->
Choose free for my scale because it visually represents the best.  
\#\#\# Exercise 4

Remove this text, and add your answer for Exercise 4 here. Use a single
pipeline to identity the neighborhoods with the top five median listing
prices. Then, in another pipeline filter the data for these five
neighborhoods and make ridge plots of the distributions of listing
prices in these five neighborhoods. In a third pipeline calculate the
minimum, mean, median, standard deviation, IQR, and maximum listing
price in each of these neighborhoods.

``` r
top5 <- boston_airBnB %>%
  
  
  
  #count(neighborhood,median(price))%>%   #use count to create freq table fot neighborhood and median prices. 
  #arrange(n)  %>%   #arranges this freq table in ascending order
  #slice(1:5)            #selects top 5 values from freq table
   group_by(neighborhood) %>% 
 summarise(med_price = median(price)) %>% 
  slice_max(order_by = med_price, n  =5)
```

``` r
ggplot(boston_airBnB %>%
         filter(neighborhood %in% top5$neighborhood),
       aes(x = price, y = neighborhood))+
 geom_density_ridges()
```

    ## Picking joint bandwidth of 28.3

![](hw-02_report_files/figure-gfm/top-5-median-plot-1.png)<!-- -->

``` r
boston_airBnB %>%
  group_by(neighborhood)%>%
  summarise(
    min_price  = min(price), 
    med_price = median(price), 
    mean_price = mean(price),
    sd_price = sd(price), 
    IQR_price = IQR(price), 
   )%>%

  filter(med_price > 135)
```

    ## # A tibble: 5 x 6
    ##   neighborhood   min_price med_price mean_price sd_price IQR_price
    ##   <chr>              <dbl>     <dbl>      <dbl>    <dbl>     <dbl>
    ## 1 Beacon Hill           50       140       156.     96.5      51  
    ## 2 Cambridge             50       245       213.    123.      143. 
    ## 3 Charlestown           45       200       198.     68.7     100  
    ## 4 Fenway/Kenmore         0       136       154.     93.5     100  
    ## 5 North End             10       150       161.     67.7      97.5

### Exercise 5

Remove this text, and add your answer for Exercise 5 here.

``` r
ggplot(boston_airBnB, aes(x = review_scores_rating ))+ 
  geom_density(adjust = 5)+
  facet_wrap(~neighborhood, scales = "fixed")+
  labs ( 
    x = "Review out of 5 Stars" ,
    y = " density of reviews", 
    title = "Distribution of reviews per neighberhood ")
```

    ## Warning: Removed 487 rows containing non-finite values (stat_density).

![](hw-02_report_files/figure-gfm/review-scores-rating-1.png)<!-- -->
