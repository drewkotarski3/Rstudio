Lab 07 - Grading the professor
================
Group 6
4/13/22

### Load packages and data

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
library(tidymodels)
```

    ## Warning: package 'tidymodels' was built under R version 4.0.5

    ## Warning: package 'broom' was built under R version 4.0.5

    ## Warning: package 'dials' was built under R version 4.0.5

    ## Warning: package 'scales' was built under R version 4.0.5

    ## Warning: package 'infer' was built under R version 4.0.5

    ## Warning: package 'modeldata' was built under R version 4.0.5

    ## Warning: package 'parsnip' was built under R version 4.0.5

    ## Warning: package 'recipes' was built under R version 4.0.5

    ## Warning: package 'rsample' was built under R version 4.0.5

    ## Warning: package 'tune' was built under R version 4.0.5

    ## Warning: package 'workflows' was built under R version 4.0.5

    ## Warning: package 'workflowsets' was built under R version 4.0.5

    ## Warning: package 'yardstick' was built under R version 4.0.5

``` r
evals <- readr::read_rds( "data/evals.RData")
```

### Exercise 1

Visualize the distribution of score. Is the distribution skewed? What
does that tell you about how students rate courses? Is this what you
expected to see? Why, or why not? Include any summary statistics and
visualizations you use in your response.

``` r
ggplot(data = evals, aes(x = score)) +
  geom_histogram()
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](lab_07_grading_the_prof_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

``` r
mean(evals$score)
```

    ## [1] 4.17473

The distribution of scores is skewed left, showing that on average
students rate professors highly. There is a mean score of 4.17473.

### Exercise 2

``` r
ggplot(data = evals, mapping = aes(x = bty_avg , y = score)) +
  geom_point()
```

![](lab_07_grading_the_prof_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

### Exercise 3

``` r
ggplot(data = evals, mapping = aes(x = bty_avg, y = score)) +
  geom_jitter()
```

![](lab_07_grading_the_prof_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
Jitter helps us to see all individual data points even if they would
usually overlap because of random variation that jitter adds to each
point.

## Exercise 4

``` r
score_bty_fit <- linear_reg() %>%
  set_engine("lm") %>%
  fit(score ~ bty_avg, data = evals)
score_bty_fit
```

    ## parsnip model object
    ## 
    ## 
    ## Call:
    ## stats::lm(formula = score ~ bty_avg, data = data)
    ## 
    ## Coefficients:
    ## (Intercept)      bty_avg  
    ##     3.88034      0.06664

# Exercise 5

``` r
ggplot(evals, aes(x = bty_avg , y = score)) +
  geom_point() +
  geom_smooth(method = "lm", color = "#E48957", se = FALSE)
```

    ## `geom_smooth()` using formula 'y ~ x'

![](lab_07_grading_the_prof_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->
