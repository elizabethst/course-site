---
title: "Functions in R"
date: 2019-03-01

type: docs
toc: true
draft: false
aliases: ["/program_functions.html"]
categories: ["programming"]

menu:
  notes:
    parent: Programming elements
    weight: 3
---




```r
library(tidyverse)
```

**Functions** are an important tool in the computational social scientist's toolkit. They enable you to avoid repetition and copy-and-paste and greatly increase the efficiency of your code writing.

* **They are easy to reuse**. If an update to the code is necessary, you revise it in one location and the changes propogate to all over components that implement the function.
* **They are self-documenting**. [Give your function a good name](http://r4ds.had.co.nz/functions.html#functions-are-for-humans-and-computers) and you will easily remember the function and its purpose.
* **They are easy-ier to debug**. There are fewer chances to make mistakes because the code only exists in one location. When copying and pasting, you may forget to copy an important line or fail to update a line in one location.

In fact, you have used functions the entire time you have programmed in R. The only difference is that the functions were written for you. `tidyr`, `dplyr`, `ggplot2`, all of these libraries contain major functions for tidying, transforming, and visualizing data. **You have the power to write your own functions.** Well, if you don't already you soon will.

> Good rule of thumb - [if you have copied and pasted a block of code more than twice, it is time to convert it to a function.](http://r4ds.had.co.nz/functions.html#when-should-you-write-a-function)

## Components of a function

Functions have three key components:

1. A **name**. This should be informative and describe what the function does
1. The **arguments**, or list of inputs, to the function. They go inside the parentheses in `function()`.
1. The **body**. This is the block of code within `{}` that immediately follows `function(...)`, and is the code that you developed to perform the action described in the **name** using the **arguments** you provide.

## The `rescale` function

Here is a user-generated function from [R for Data Science](http://r4ds.had.co.nz/functions.html#when-should-you-write-a-function). Analyze it and identify the three key components.


```r
rescale01 <- function(x) {
  rng <- range(x, na.rm = TRUE)
  (x - rng[1]) / (rng[2] - rng[1])
}
```


```r
rescale01(c(0, 5, 10))
```

```
## [1] 0.0 0.5 1.0
```

```r
rescale01(c(-10, 0, 10))
```

```
## [1] 0.0 0.5 1.0
```

```r
rescale01(c(1, 2, 3, NA, 5))
```

```
## [1] 0.00 0.25 0.50   NA 1.00
```

<details> 
  <summary>Click for the solution</summary>
  <p>

* Name - `rescale01`
    * This is a function that will rescale a variable from 0 to 1
* Arguments
    * This function takes one argument `x` - the variable to be transformed
    * We could call the argument whatever we like, but `x` is a conventional name
    * Multiple inputs would be `x`, `y`, `z`, etc., or take on informative names such as `data`, `formula`, `na.rm`, etc.
    * **You should use what makes sense**
* Body
    * This takes two lines of code
        1. Calculate the range of the variable (its minimum and maximum values) and ignore missing values. Save this as an object called `rng`.
        1. For each value in the variable, subtract the minimum value in the variable and divide by the difference between the maximum and minimum value. Use arthimetic notation to make sure order of operations is followed.
    * By default, whatever is the last thing generated by the function is returned as the *output*

  </p>
</details>

This function can easily be reused for any numeric variable. Rather than writing out the contents of the function every time, we just use the function itself.

## Pythagorean theorem function

Analyze the following function.

* Identify the name, arguments, and body
* What does it do?
* If `a = 3` and `b = 4`, what should we expect the output to be?


```r
pythagorean <- function(a, b){
  hypotenuse <- sqrt(a^2 + b^2)
  return(hypotenuse)
}
```

<details> 
  <summary>Click for the solution</summary>
  <p>

* Name - `pythagorean`
    * Calculates the length of the hypotenuse of a right triangle.
* Arguments
    * These are the inputs of the function. They go inside `function`
    * This function takes two arguments
        * `a` - length of one side of a right triangle
        * `b` - length of another side of a right triangle
* Body
    * Block of code within `{}` that immediately follows `function(...)`
    * Here, I wrote two lines of code
        * The first line creates a new object `hypotenuse` which is the square root of the sum of squares of the two sides of the right triangle (also called the hypotenuse)
        * I then explicitly `return` `hypotenuse` as the output of the function. I could also have written the function as:


```r
pythagorean <- function(a, b){
  hypotenuse <- sqrt(a^2 + b^2)
}
```

or even:


```r
pythagorean <- function(a, b){
  sqrt(a^2 + b^2)
}
```

But I wanted to explicitly identify each step of the code for others to review. Early on in your function writing career, you will want to be more explicit so future you can interpret your own code. As you practice and become more comfortable writing functions, you can be more relaxed in your coding style and documentation.

  </p>
</details>

## How to use a function

When using functions, by default the returned object is merely printed to the screen.


```r
pythagorean(a = 3, b = 4)
```

```
## [1] 5
```

If you want it saved, you need to assign it to an object.


```r
(tri_c <- pythagorean(a = 3, b = 4))
```

```
## [1] 5
```

### Objects created inside functions


```r
pythagorean(a = 3, b = 4)
```

```
## [1] 5
```

```r
hypotenuse
```

```
## Error in eval(expr, envir, enclos): object 'hypotenuse' not found
```

Why does this generate an error? Why can we not see the results of `hypotenuse`? After all, it was generated by `pythagorean`, right?

![](https://i.giphy.com/l1IY5J4Cfw8JLi40M.gif)

Objects created inside a function exist within their own **environment**. Typically you are working in the global environment. You can see all objects that exist in that environment in the top-right panel.

![The environment panel in RStudio](/img/environment.png)

Objects created within a function are destroyed once the function completes its execution, unless you `return` the object as part of the output. This is why you do not see `hypotenuse` listed in the environment - it has already been destroyed.

## Exercise: calculate the sum of squares of two variables

Write a function that calculates the sum of the squared value of two numbers. For instance, it should generate the following output:




```r
my_function(3, 4)
```

```
## [1] 25
```

<details> 
  <summary>Click for the solution</summary>
  <p>


```r
sum_of_squares <- function(x, y){
  x^2 + y^2
}
```


```r
sum_of_squares(3, 4)
```

```
## [1] 25
```

* Name - `sum_of_squares`
    * Calculates the sum of the squared value of two variables
* Arguments
    * `x` - one number
    * `y` - a second number
* Body
    * The first line squares `x` and `y` independently and then adds the results together

> Cool fact - this function also works with vectors of numbers


```r
x <- c(2, 4, 6)
y <- c(1, 3, 5)
sum_of_squares(x, y)
```

```
## [1]  5 25 61
```

  </p>
</details>

## Conditional execution

Sometimes you only want to execute code if a condition is met. To do that, use an **if-else statement**.


```r
if (condition) {
  # code executed when condition is TRUE
} else {
  # code executed when condition is FALSE
}
```

`condition` must always evaluate to either `TRUE` or `FALSE`.^[These are **Boolean logical values** - we used them to [make comparisons](http://r4ds.had.co.nz/transform.html#comparisons) and will talk more next class about [logical vectors](http://r4ds.had.co.nz/vectors.html#logical).] This is similar to `filter()`, except `condition` can only be a single value (i.e. a vector of length 1), whereas `filter()` works for entire vectors (or columns).

You can chain conditional statements together:


```r
if (this) {
  # do that
} else if (that) {
  # do something else
} else {
  # do something completely different
}
```

But this can get tedious if you need to consider many conditions. There are alternatives in R for some of these long conditional statements. For instance, if you want to convert a continuous (or numeric) variable to categories, use `cut()`:


```r
diamonds %>%
  select(carat) %>%
  mutate(carat_autobin = cut(carat, breaks = 5),
         carat_manbin = cut(carat,
                            breaks = c(0, 1, 2, 3, 6),
                            labels = c("Small", "Medium", "Large", "Huge")))
```

```
## # A tibble: 53,940 x 3
##    carat carat_autobin carat_manbin
##    <dbl> <fct>         <fct>       
##  1 0.23  (0.195,1.16]  Small       
##  2 0.21  (0.195,1.16]  Small       
##  3 0.23  (0.195,1.16]  Small       
##  4 0.290 (0.195,1.16]  Small       
##  5 0.31  (0.195,1.16]  Small       
##  6 0.24  (0.195,1.16]  Small       
##  7 0.24  (0.195,1.16]  Small       
##  8 0.26  (0.195,1.16]  Small       
##  9 0.22  (0.195,1.16]  Small       
## 10 0.23  (0.195,1.16]  Small       
## # … with 53,930 more rows
```

## `if` versus `if_else()`

Because if-else conditional statements like the ones outlined above must always resolve to a single `TRUE` or `FALSE`, they cannot be used for **vector operations**. Vector operations are where you make multiple comparisons simultaneously for each value stored inside a vector. Consider the `gun_deaths` data and imagine you wanted to create a new column identifying whether or not an individual had at least a high school education.


```r
library(rcfss)
data("gun_deaths")

(educ <- select(gun_deaths, education))
```

```
## # A tibble: 100,798 x 1
##    education   
##    <fct>       
##  1 BA+         
##  2 Some college
##  3 BA+         
##  4 BA+         
##  5 HS/GED      
##  6 Less than HS
##  7 HS/GED      
##  8 HS/GED      
##  9 Some college
## 10 <NA>        
## # … with 100,788 more rows
```

This sounds like a classic if-else operation. For each individual, if `education` equals "Less than HS", then the value in the new column should be "Less than HS". Otherwise, it should be "HS+". But what happens if we try to implement this using an if-else operation like above?


```r
(educ_if <- educ %>%
   mutate(hsPlus = if(education == "Less than HS"){
     "Less than HS"
   } else {
     "HS+"
   }))
```

```
## Warning in if (education == "Less than HS") {: the condition has length > 1
## and only the first element will be used
```

```
## # A tibble: 100,798 x 2
##    education    hsPlus
##    <fct>        <chr> 
##  1 BA+          HS+   
##  2 Some college HS+   
##  3 BA+          HS+   
##  4 BA+          HS+   
##  5 HS/GED       HS+   
##  6 Less than HS HS+   
##  7 HS/GED       HS+   
##  8 HS/GED       HS+   
##  9 Some college HS+   
## 10 <NA>         HS+   
## # … with 100,788 more rows
```

This did not work correctly. Because `if()` can only handle a single `TRUE`/`FALSE` value, it only checked the first row of the data frame. That row contained "BA+" for the individual, so it generated a vector of length 100798 with each value being "HS+".


```r
count(educ_if, hsPlus)
```

```
## # A tibble: 1 x 2
##   hsPlus      n
##   <chr>   <int>
## 1 HS+    100798
```

Because we in fact want to make this if-else comparison 100798 times, we should instead use `if_else()`. This **vectorizes** the if-else comparison and makes a separate comparison for each row of the data frame. This allows us to correctly generate this new column.^[Notice that is also preserves missing values in the new column. Remember, [any operation performed on a missing value will itself become a missing value.](http://r4ds.had.co.nz/transform.html#missing-values)]


```r
(educ_ifelse <- educ %>%
  mutate(hsPlus = if_else(education == "Less than HS", "Less than HS", "HS+")))
```

```
## # A tibble: 100,798 x 2
##    education    hsPlus      
##    <fct>        <chr>       
##  1 BA+          HS+         
##  2 Some college HS+         
##  3 BA+          HS+         
##  4 BA+          HS+         
##  5 HS/GED       HS+         
##  6 Less than HS Less than HS
##  7 HS/GED       HS+         
##  8 HS/GED       HS+         
##  9 Some college HS+         
## 10 <NA>         <NA>        
## # … with 100,788 more rows
```

```r
count(educ_ifelse, hsPlus)
```

```
## # A tibble: 3 x 2
##   hsPlus           n
##   <chr>        <int>
## 1 <NA>          1422
## 2 HS+          77553
## 3 Less than HS 21823
```

## Exercise: write a `fizzbuzz` function

[**Fizz buzz**](https://en.wikipedia.org/wiki/Fizz_buzz) is a children's game that teaches about division. Players take turns counting incrementally, replacing any number divisible by three with the word "fizz" and any number divisible by five with the word "buzz".

Likewise, a `fizzbuzz` function takes a single number as input. If the number is divisible by three, it returns "fizz". If it’s divisible by five it returns "buzz". If it’s divisible by three and five, it returns "fizzbuzz". Otherwise, it returns the number.

The output of your function should look like this:




```r
my_function(3)
```

```
## [1] "fizz"
```

```r
my_function(5)
```

```
## [1] "buzz"
```

```r
my_function(15)
```

```
## [1] "fizzbuzz"
```

```r
my_function(4)
```

```
## [1] 4
```

### A helpful hint about modular division

`%%` is modular division. It returns the remainder left over after the division, rather than a floating point number.


```r
5 / 3
```

```
## [1] 1.666667
```

```r
5 %% 3
```

```
## [1] 2
```

<details> 
  <summary>Click for the solution</summary>
  <p>


```r
fizzbuzz <- function(x){
  if(x %% 3 == 0 && x %% 5 == 0){
    return("fizzbuzz")
  } else if(x %% 3 == 0){
    return("fizz")
  } else if(x %% 5 == 0){
    return("buzz")
  } else{
    return(x)
  }
}
```


```r
fizzbuzz(3)
```

```
## [1] "fizz"
```

```r
fizzbuzz(5)
```

```
## [1] "buzz"
```

```r
fizzbuzz(15)
```

```
## [1] "fizzbuzz"
```

```r
fizzbuzz(4)
```

```
## [1] 4
```

* Name - `fizzbuzz`
    * Plays a single round of the Fizz Buzz game
* Arguments
    * `x` - a number
* Body
    * Uses modular division and a series of if-else statements to check if `x` is evenly divisible with 3 and/or 5.
    * The first comparison to make checks if `x` is a "fizzbuzz" (evenly divisible by 3 **and** 5). This should be the first comparison because it needs to return "fizzbuzz". If we had this at the end of the comparison chain, the function would prematurely return on "fizz" or "buzz".
        * If `TRUE`, then print "fizzbuzz"
    * If the first condition is not met, check to see if `x` is a "fizz" (divisible by 3).
        * If `TRUE`, then print "fizz"
    * If the first two conditions are not met, check to see if `x` is a "buzz" (divisible by 5).
        * If `TRUE`, then print "buzz"
    * If the first three conditions are all `FALSE`, then print the original number `x`.
    
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
