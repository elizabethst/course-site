---
title: "Computer programming as a form of problem solving"
date: 2019-03-01

type: docs
toc: true
draft: false
aliases: ["/datawrangle_problem_solve.html"]
categories: ["datawrangle"]

menu:
  notes:
    parent: Data wrangling
    weight: 1
---




```r
library(tidyverse)
```

![Professor X from *X-Men* (the Patrick Stewart version, not James Mcavoy)](/img/xmen_xavier.jpg)

[![*Computer Problems*. XKCD.](/img/xkcd_computer_problems.png)](https://xkcd.com/722/)

Computers are not mind-reading machines. They are very efficient at certain tasks, and can perform calculations thousands of times faster than any human. But they are also very dumb: they can only do what you tell them to do. If you are not explicit about what you want the computer to do, or you misspeak and tell the computer to do the wrong thing, it will not correct you.

In order to translate your goal for the program into clear instructions for the computer, you need to break the problem down into a set of smaller, discrete chunks that can be followed by the computer (and also by yourself/other humans).

## Decomposing problems using `diamonds`


```r
library(tidyverse)
glimpse(x = diamonds)
```

```
## Observations: 53,940
## Variables: 10
## $ carat   <dbl> 0.23, 0.21, 0.23, 0.29, 0.31, 0.24, 0.24, 0.26, 0.22, 0.…
## $ cut     <ord> Ideal, Premium, Good, Premium, Good, Very Good, Very Goo…
## $ color   <ord> E, E, E, I, J, J, I, H, E, H, J, J, F, J, E, E, I, J, J,…
## $ clarity <ord> SI2, SI1, VS1, VS2, SI2, VVS2, VVS1, SI1, VS2, VS1, SI1,…
## $ depth   <dbl> 61.5, 59.8, 56.9, 62.4, 63.3, 62.8, 62.3, 61.9, 65.1, 59…
## $ table   <dbl> 55, 61, 65, 58, 58, 57, 57, 55, 61, 61, 55, 56, 61, 54, …
## $ price   <int> 326, 326, 327, 334, 335, 336, 336, 337, 337, 338, 339, 3…
## $ x       <dbl> 3.95, 3.89, 4.05, 4.20, 4.34, 3.94, 3.95, 4.07, 3.87, 4.…
## $ y       <dbl> 3.98, 3.84, 4.07, 4.23, 4.35, 3.96, 3.98, 4.11, 3.78, 4.…
## $ z       <dbl> 2.43, 2.31, 2.31, 2.63, 2.75, 2.48, 2.47, 2.53, 2.49, 2.…
```

The `diamonds` dataset contains prices and other attributes of almost 54,000 diamonds. Let's answer the following questions by **decomposing** the problem into a series of discrete steps we can tell R to follow.

## What is the average price of an ideal cut diamond?

Think about what we need to have the computer do to answer this question:

1. First we need to identify the **input**, or the data we're going to analyze.
1. Next we need to **select** only the observations which are ideal cut diamonds.
1. Finally we need to calculate the average value, or **mean**, of price.

Here's how we tell the computer to do this:


```r
data("diamonds")
diamonds_ideal <- filter(.data = diamonds, cut == "Ideal")
summarize(.data = diamonds_ideal, avg_price = mean(price))
```

```
## # A tibble: 1 x 1
##   avg_price
##       <dbl>
## 1     3458.
```

The first line of code copies the `diamonds` data frame from the hard drive into memory so we can actively work with it. The second line creates a new data frame called `diamonds_ideal` that only contains the observations in `diamonds` which are ideal cut diamonds. The third line summarizes the new data frame and calculates the mean value for the `price` variable.

## What is the average price of a diamond for each cut?

**Exercise: decompose the question into a discrete set of tasks to complete using R.**

<details> 
  <summary>Click for the solution</summary>
  <p>
  
1. First we need to identify the **input**, or the data we're going to analyze.
1. Next we need to **group** the observations together by their value for `cut`, so we can make separate calculations for each category.
1. Finally we need to calculate the average value, or **mean**, of price for each cut of diamond.

Here's how we tell the computer to do this:


```r
data("diamonds")
diamonds_cut <- group_by(.data = diamonds, cut)
summarize(.data = diamonds_cut, avg_price = mean(price))
```

```
## # A tibble: 5 x 2
##   cut       avg_price
##   <ord>         <dbl>
## 1 Fair          4359.
## 2 Good          3929.
## 3 Very Good     3982.
## 4 Premium       4584.
## 5 Ideal         3458.
```

  </p>
</details>

## What is the average carat size and price for each cut of "I" colored diamonds?

**Exercise: decompose the question into a discrete set of tasks to complete using R.**

<details> 
  <summary>Click for the solution</summary>
  <p>
  
1. Use `diamonds` as the input
1. Filter `diamonds` to only keep observations where the color is rated as "I"
1. Group the filtered `diamonds` data frame by cut
1. Summarize the grouped and filtered `diamonds` data frame by calculating the average carat size and price


```r
data("diamonds")
diamonds_i <- filter(.data = diamonds, color == "I")
diamonds_i_group <- group_by(.data = diamonds_i, cut)
summarize(
  .data = diamonds_i_group,
  carat = mean(carat),
  price = mean(price)
)
```

```
## # A tibble: 5 x 3
##   cut       carat price
##   <ord>     <dbl> <dbl>
## 1 Fair      1.20  4685.
## 2 Good      1.06  5079.
## 3 Very Good 1.05  5256.
## 4 Premium   1.14  5946.
## 5 Ideal     0.913 4452.
```

  </p>
</details>

## Session Info



```r
devtools::session_info()
```

```
## ─ Session info ──────────────────────────────────────────────────────────
##  setting  value                       
##  version  R version 3.5.3 (2019-03-11)
##  os       macOS Mojave 10.14.3        
##  system   x86_64, darwin15.6.0        
##  ui       X11                         
##  language (EN)                        
##  collate  en_US.UTF-8                 
##  ctype    en_US.UTF-8                 
##  tz       America/Chicago             
##  date     2019-05-07                  
## 
## ─ Packages ──────────────────────────────────────────────────────────────
##  package     * version date       lib source        
##  assertthat    0.2.1   2019-03-21 [2] CRAN (R 3.5.3)
##  backports     1.1.3   2018-12-14 [2] CRAN (R 3.5.0)
##  blogdown      0.11    2019-03-11 [1] CRAN (R 3.5.2)
##  bookdown      0.9     2018-12-21 [1] CRAN (R 3.5.0)
##  broom         0.5.1   2018-12-05 [2] CRAN (R 3.5.0)
##  callr         3.2.0   2019-03-15 [2] CRAN (R 3.5.2)
##  cellranger    1.1.0   2016-07-27 [2] CRAN (R 3.5.0)
##  cli           1.1.0   2019-03-19 [1] CRAN (R 3.5.2)
##  colorspace    1.4-1   2019-03-18 [2] CRAN (R 3.5.2)
##  crayon        1.3.4   2017-09-16 [2] CRAN (R 3.5.0)
##  desc          1.2.0   2018-05-01 [2] CRAN (R 3.5.0)
##  devtools      2.0.1   2018-10-26 [1] CRAN (R 3.5.1)
##  digest        0.6.18  2018-10-10 [1] CRAN (R 3.5.0)
##  dplyr       * 0.8.0.1 2019-02-15 [1] CRAN (R 3.5.2)
##  evaluate      0.13    2019-02-12 [2] CRAN (R 3.5.2)
##  forcats     * 0.4.0   2019-02-17 [2] CRAN (R 3.5.2)
##  fs            1.2.7   2019-03-19 [1] CRAN (R 3.5.3)
##  generics      0.0.2   2018-11-29 [1] CRAN (R 3.5.0)
##  ggplot2     * 3.1.0   2018-10-25 [1] CRAN (R 3.5.0)
##  glue          1.3.1   2019-03-12 [2] CRAN (R 3.5.2)
##  gtable        0.2.0   2016-02-26 [2] CRAN (R 3.5.0)
##  haven         2.1.0   2019-02-19 [2] CRAN (R 3.5.2)
##  here          0.1     2017-05-28 [2] CRAN (R 3.5.0)
##  hms           0.4.2   2018-03-10 [2] CRAN (R 3.5.0)
##  htmltools     0.3.6   2017-04-28 [1] CRAN (R 3.5.0)
##  httr          1.4.0   2018-12-11 [2] CRAN (R 3.5.0)
##  jsonlite      1.6     2018-12-07 [2] CRAN (R 3.5.0)
##  knitr         1.22    2019-03-08 [2] CRAN (R 3.5.2)
##  lattice       0.20-38 2018-11-04 [2] CRAN (R 3.5.3)
##  lazyeval      0.2.2   2019-03-15 [2] CRAN (R 3.5.2)
##  lubridate     1.7.4   2018-04-11 [2] CRAN (R 3.5.0)
##  magrittr      1.5     2014-11-22 [2] CRAN (R 3.5.0)
##  memoise       1.1.0   2017-04-21 [2] CRAN (R 3.5.0)
##  modelr        0.1.4   2019-02-18 [2] CRAN (R 3.5.2)
##  munsell       0.5.0   2018-06-12 [2] CRAN (R 3.5.0)
##  nlme          3.1-137 2018-04-07 [2] CRAN (R 3.5.3)
##  pillar        1.3.1   2018-12-15 [2] CRAN (R 3.5.0)
##  pkgbuild      1.0.3   2019-03-20 [1] CRAN (R 3.5.3)
##  pkgconfig     2.0.2   2018-08-16 [2] CRAN (R 3.5.1)
##  pkgload       1.0.2   2018-10-29 [1] CRAN (R 3.5.0)
##  plyr          1.8.4   2016-06-08 [2] CRAN (R 3.5.0)
##  prettyunits   1.0.2   2015-07-13 [2] CRAN (R 3.5.0)
##  processx      3.3.0   2019-03-10 [2] CRAN (R 3.5.2)
##  ps            1.3.0   2018-12-21 [2] CRAN (R 3.5.0)
##  purrr       * 0.3.2   2019-03-15 [2] CRAN (R 3.5.2)
##  R6            2.4.0   2019-02-14 [1] CRAN (R 3.5.2)
##  Rcpp          1.0.1   2019-03-17 [1] CRAN (R 3.5.2)
##  readr       * 1.3.1   2018-12-21 [2] CRAN (R 3.5.0)
##  readxl        1.3.1   2019-03-13 [2] CRAN (R 3.5.2)
##  remotes       2.0.2   2018-10-30 [1] CRAN (R 3.5.0)
##  rlang         0.3.4   2019-04-07 [1] CRAN (R 3.5.2)
##  rmarkdown     1.12    2019-03-14 [1] CRAN (R 3.5.2)
##  rprojroot     1.3-2   2018-01-03 [2] CRAN (R 3.5.0)
##  rstudioapi    0.10    2019-03-19 [1] CRAN (R 3.5.3)
##  rvest         0.3.2   2016-06-17 [2] CRAN (R 3.5.0)
##  scales        1.0.0   2018-08-09 [1] CRAN (R 3.5.0)
##  sessioninfo   1.1.1   2018-11-05 [1] CRAN (R 3.5.0)
##  stringi       1.4.3   2019-03-12 [1] CRAN (R 3.5.2)
##  stringr     * 1.4.0   2019-02-10 [1] CRAN (R 3.5.2)
##  testthat      2.0.1   2018-10-13 [2] CRAN (R 3.5.0)
##  tibble      * 2.1.1   2019-03-16 [2] CRAN (R 3.5.2)
##  tidyr       * 0.8.3   2019-03-01 [1] CRAN (R 3.5.2)
##  tidyselect    0.2.5   2018-10-11 [1] CRAN (R 3.5.0)
##  tidyverse   * 1.2.1   2017-11-14 [2] CRAN (R 3.5.0)
##  usethis       1.4.0   2018-08-14 [1] CRAN (R 3.5.0)
##  withr         2.1.2   2018-03-15 [2] CRAN (R 3.5.0)
##  xfun          0.5     2019-02-20 [1] CRAN (R 3.5.2)
##  xml2          1.2.0   2018-01-24 [2] CRAN (R 3.5.0)
##  yaml          2.2.0   2018-07-25 [2] CRAN (R 3.5.0)
## 
## [1] /Users/soltoffbc/Library/R/3.5/library
## [2] /Library/Frameworks/R.framework/Versions/3.5/Resources/library
```
