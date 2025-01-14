---
title: "HW02: Exploring and visualizing data"
date: 2019-04-08T13:30:00-06:00  # Schedule page publish date
publishdate: 2019-03-01

draft: false
type: post
aliases: ["/hw02-explore-data.html"]

summary: "Transform and explore a cleaned dataset on gun deaths in the United States."
url_code: "https://github.com/cfss-su19/hw02"
---



# Overview

Due before class on Monday July 1st.

Now that you've demonstrated your software is setup, the goal of this assignment is to practice transforming and exploring data.

# Fork the `hw02` repository

Go [here](https://github.com/cfss-su19/hw02) to fork the repo.

# Exploring clean data

[FiveThirtyEight](http://fivethirtyeight.com/), a data journalism site devoted to politics, sports, science, economics, and culture, recently published a series of articles on [gun deaths in America](http://fivethirtyeight.com/features/gun-deaths-introduction/). Gun violence in the United States is a significant political issue, and while reducing gun deaths is a noble goal, we must first understand the causes and patterns in gun violence in order to craft appropriate policies. As part of the project, FiveThirtyEight collected data from the Centers for Disease Control and Prevention, as well as other governmental agencies and non-profits, on all gun deaths in the United States from 2012-2014.

## Obtain the data

I have included this dataset in the [`rcfss`](https://github.com/uc-cfss/rcfss) library on GitHub. To install the package, use the command `devtools::install_github("uc-cfss/rcfss")` in R. If you don't already have the `devtools` library installed, you will get an error. Go back and install this first using `install.packages()`, then install `rcfss`. The gun deaths dataset can be loaded using `data("gun_deaths")`. Use the help function in R (`?gun_deaths`) to get detailed information on the variables and coding information.

## Explore the data

### Very specific prompts

1. Generate a data frame that summarizes the number of gun deaths per month.
    1. Print the data frame as [a formatted `kable()` table](#formatting-tables).
    1. Generate a bar chart with human-readable labels on the x-axis. That is, each month should be labeled "Jan", "Feb", "Mar" (full or abbreviated month names are fine), not `1`, `2`, `3`.
1. Generate a bar chart that identifies the number of gun deaths associated with each type of intent cause of death. The bars should be sorted from highest to lowest values.
1. Generate a boxplot visualizing the age of gun death victims, by sex. Print the average age of female gun death victims.

### More open-ended questions

Answer the following questions. Generate appropriate figures/tables to support your conclusions.

1. How many white males with at least a high school education were killed by guns in 2012?
1. Which season of the year has the most gun deaths? Assume that
    * Winter = January-March
    * Spring = April-June
    * Summer = July-September
    * Fall = October-December
    * **Hint**: you need to convert a continuous variable into a categorical variable. [Find a function that does that.](https://www.google.com)
1. Are whites who are killed by guns more likely to die because of suicide or homicide? How does this compare to blacks and hispanics?

### Very open-ended

1. Are police-involved gun deaths significantly different from other gun deaths? Assess the relationship between police involvement and age, police involvement and race, and the intersection of all three variables.

### Formatting graphs

While you are practicing exploratory data analysis, your final graphs should be appropriate for sharing with outsiders. That means your graphs should have:

* [A title](http://r4ds.had.co.nz/graphics-for-communication.html#label)
* Labels on the axes (see `?labs` for details)

This is just a starting point. Consider adopting your own color scales, [taking control of your legends (if any)](http://www.cookbook-r.com/Graphs/Legends_(ggplot2)/), playing around with [themes](https://ggplot2.tidyverse.org/reference/index.html#section-themes), etc.

### Formatting tables

When presenting tabular data (aka `dplyr::summarize()`), make sure you format it correctly. Use the `kable()` function from the `knitr` package to format the table for the final document. For instance, this is a poorly presented table summarizing where gun deaths occurred:




```
## # A tibble: 11 x 2
##    place                       n
##    <chr>                   <int>
##  1 <NA>                     1384
##  2 Farm                      470
##  3 Home                    60486
##  4 Industrial/construction   248
##  5 Other specified         13751
##  6 Other unspecified        8867
##  7 Residential institution   203
##  8 School/instiution         671
##  9 Sports                    128
## 10 Street                  11151
## 11 Trade/service area       3439
```

Instead, use `kable()` to format the table, add a caption, and label the columns:


|Location                | Number of deaths|
|:-----------------------|----------------:|
|NA                      |             1384|
|Farm                    |              470|
|Home                    |            60486|
|Industrial/construction |              248|
|Other specified         |            13751|
|Other unspecified       |             8867|
|Residential institution |              203|
|School/instiution       |              671|
|Sports                  |              128|
|Street                  |            11151|
|Trade/service area      |             3439|

Run `?kable` in the console to see how additional options.

> Note that when viewed on GitHub, table captions will not show up. Just a (missing) feature of Markdown on GitHub 😩

# Submit the assignment

Your assignment should be submitted as an R Markdown document. **Don't know what an R Markdown document is? [Read this!](http://rmarkdown.rstudio.com/lesson-1.html) Or [this!](http://r4ds.had.co.nz/r-markdown.html)** I have included starter files for you to modify to complete the assignment, so you are not beginning completely from scratch.

Follow instructions on [homework workflow](/faq/homework-guidelines/#homework-workflow). As part of the pull request, you're encouraged to reflect on what was hard/easy, problems you solved, helpful tutorials you read, etc.

# Rubric

Check minus: Displays minimal effort. Doesn't complete all components. Code is poorly written and not documented. Uses the same type of plot for each graph, or doesn't use plots appropriate for the variables being analyzed. No record of commits other than the final push to GitHub.

Check: Solid effort. Hits all the elements. No clear mistakes. Easy to follow (both the code and the output). Nothing spectacular, either bad or good.

Check plus: Finished all components of the assignment correctly. Code is well-documented (both self-documented and with additional comments as necessary). Graphs and tables are properly labeled. Uses multiple commits to back up and show a progression in the work. Analysis is clear and easy to follow, either because graphs are labeled clearly or you've written additional text to describe how you interpret the output.
