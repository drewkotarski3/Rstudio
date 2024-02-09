HW 1, Recreating parts of the 538 Bechdel Analysis
================
Andrew Kotarski

# Introduction

In this mini analysis we work with the data used in the FiveThirtyEight
story titled [“The Dollar-And-Cents Case Against Hollywood’s Exclusion
of
Women”](https://fivethirtyeight.com/features/the-dollar-and-cents-case-against-hollywoods-exclusion-of-women/).
Your task is to fill in the blanks denoted by `___`.

The point of this first homework assignment is not only to complete an
analysis, but also to have you explore running `R` code within the
RMarkdown framework.

I have the .Rmd file set up to generate a markdown file within the
project directory when you `knit`, and you should be able to `knit` as
soon as you install the `FiveThirtyEight` package. Run
`install.packages("fivethirtyeight")` in the console before knitting for
the first time.

## Some tips and reminders:

`R` code is run either within `R` code “chunks”

``` r
# R code goes here. You can run this code chunk by pressing the green arrow in the 
# top-right of the code chunk, or go to Code --> Run... to see various keyboard shortcuts
print("R code within this chunk is evaluated top-to-bottom!")
```

    ## [1] "R code within this chunk is evaluated top-to-bottom!"

or “in-line” when you knit the document with markdown text like this:
Wow I can also run R code in-line\! And like this: 2+2 = 4.

When you `knit` the RMarkdown document (press the `knit` button at the
top of the screen, or click `File` \(\rightarrow\) `Knit Document`) `R`
will compile your text, while also running all of the code, from
top-to-bottom.

Also note that I can add “comments” to RMarkdown text <!-- like this -->
and they do not get evaluated.

# Analyses

## Data and packages

We start with loading the packages we’ll use.

``` r
# remember to run install.packages("fivethirtyeight") in the console 
# before calling library. You only have to install once, but you need to use library()
# every time at the start of an RMarkdown document calling the functions/data from the 
# package
library(fivethirtyeight)
```

    ## Warning: package 'fivethirtyeight' was built under R version 4.0.5

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

The dataset contains information on 1794 movies released between 1970
and 2013. However we’ll focus our analysis on movies released between
1990 and 2013.

``` r
bechdel90_13 <- bechdel %>%  
  filter(between(year, 1990, 2013)) 
# filters the column year between 1990 and 2013
nrow(bechdel90_13)
```

    ## [1] 1615

<!-- (try and answer this one using "in-line" R code). See line 56 above  -->

There are 1615 such movies.

The financial variables we’ll focus on are the following:

  - `budget_2013`: Budget in 2013 inflation adjusted dollars
  - `domgross_2013`: Domestic gross (US) in 2013 inflation adjusted
    dollars
  - `intgross_2013`: Total International (i.e., worldwide) gross in 2013
    inflation adjusted dollars

And we’ll also use the `binary` and `clean_test` variables for
**grouping**.

## Analysis

Let’s take a look at how median budget and gross vary by whether the
movie passed the Bechdel test, which is stored in the `binary` variable.

``` r
bechdel90_13 %>%
  group_by(binary) %>% # groups data by the unique `binary` variables 
  # the code below creates summaries of the various columns called 
  # according to the function used. In this case, `median()`
  summarize(med_budget = median(budget_2013), 
            med_domgross = median(domgross_2013, na.rm = TRUE),
            med_intgross = median(intgross_2013, na.rm = TRUE))
```

    ## # A tibble: 2 x 4
    ##   binary med_budget med_domgross med_intgross
    ##   <chr>       <dbl>        <dbl>        <dbl>
    ## 1 FAIL    48385984.    57318606.    104475669
    ## 2 PASS    31070724     45330446.     80124349

``` r
# Note that many of the functions in the tidyverse follow both American and British
# spelling conventions, so you may see this function as "summarise" online or in 
# some class material 
```

Next, let’s take a look at how median budget and gross vary by a more
detailed indicator of the Bechdel test result. This information is
stored in the `clean_test` variable, which takes on the following
values:

  - `ok` = passes test
  - `dubious`
  - `men` = women only talk about men
  - `notalk` = women don’t talk to each other
  - `nowomen` = fewer than two women

<!-- Fill in the group_by line below and remove the `#` so it is no longer commented out.  -->

<!-- Hint: What were we interested in comparing across in the R chunk above, and  -->

<!-- what did we group_by then? -->

``` r
bechdel90_13 %>%
  group_by(`clean_test`) %>%
  summarize(med_budget = median(budget_2013),
            med_domgross = median(domgross_2013, na.rm = TRUE),
            med_intgross = median(intgross_2013, na.rm = TRUE))
```

    ## # A tibble: 5 x 4
    ##   clean_test med_budget med_domgross med_intgross
    ##   <ord>           <dbl>        <dbl>        <dbl>
    ## 1 nowomen     43373066     44891296.    89509349 
    ## 2 notalk      56570084.    63890455    123102194 
    ## 3 men         39737690.    56392786     99578022.
    ## 4 dubious     35790994     49173429     89883201 
    ## 5 ok          31070724     45330446.    80124349

In order to evaluate how return on investment varies among movies that
pass and fail the Bechdel test, we’ll first create a new variable called
`roi` as the ratio of the gross to budget.

``` r
bechdel90_13 <- bechdel90_13 %>%
  mutate(roi = (intgross_2013 + domgross_2013) / budget_2013)
```

Let’s see which movies have the highest return on investment.

``` r
bechdel90_13 %>%
  arrange(desc(roi)) %>% # arranges data in descending order according to `roi` column
  select(title, roi, year) # selects the columns title, roi, year
```

    ## # A tibble: 1,615 x 3
    ##    title                     roi  year
    ##    <chr>                   <dbl> <int>
    ##  1 Paranormal Activity      671.  2007
    ##  2 The Blair Witch Project  648.  1999
    ##  3 El Mariachi              583.  1992
    ##  4 Clerks.                  258.  1994
    ##  5 In the Company of Men    231.  1997
    ##  6 Napoleon Dynamite        227.  2004
    ##  7 Once                     190.  2006
    ##  8 The Devil Inside         155.  2012
    ##  9 Primer                   142.  2004
    ## 10 Fireproof                134.  2008
    ## # ... with 1,605 more rows

Below is a visualization of the return on investment by test result,
however it’s difficult to see the distributions due to a few extreme
observations.

``` r
# we will cover the various ggplot calls in class soon! 
ggplot(data = bechdel90_13, 
       mapping = aes(x = clean_test, y = roi, color = binary)) +
  geom_boxplot() +
  labs(title = "Return on investment vs. Bechdel test result",
       x = "Detailed Bechdel result",
       y = "Return on investment",
       color = "Binary Bechdel result")
```

![](bechdel_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

What are those movies with *very* high returns on investment?

``` r
bechdel90_13 %>%
  filter(roi > 400) %>% 
  select(title, budget_2013, domgross_2013, year) 
```

    ## # A tibble: 3 x 4
    ##   title                   budget_2013 domgross_2013  year
    ##   <chr>                         <int>         <dbl> <int>
    ## 1 Paranormal Activity          505595     121251476  2007
    ## 2 The Blair Witch Project      839077     196538593  1999
    ## 3 El Mariachi                   11622       3388636  1992

Zooming in on the movies with `roi < 16` provides a better view of how
the medians across the categories compare:

<!-- Hint to answer the above: look at the code chunk below after running it...  -->

<!-- which line do you think controls the limits of the Y axis? -->

``` r
ggplot(data = bechdel90_13, mapping = aes(x = clean_test, y = roi, color = binary)) +
  geom_boxplot() +
  labs(title = "Return on investment vs. Bechdel test result",
       subtitle = "View on medians", # Something about zooming in to a certain level
       x = "Detailed Bechdel result",
       y = "Return on investment",
       color = "Binary Bechdel result") +
  coord_cartesian(ylim = c(0, 15)) 
```

![](bechdel_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

When you have finished filling in all of the `___`’s make sure to knit
the document a final time, commit your changes with git (we will review
this in class and practice more on Wednesday Jan 26) and push your
changes to Github (see Thursday’s lab for more information).
