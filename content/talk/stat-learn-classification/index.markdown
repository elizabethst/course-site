---
title: "Statistical learning: classification and cross-validation"
date: 2019-07-16T10:00:00
publishDate: 2019-03-01T13:30:00
draft: true
type: "talk"

aliases: ["/cm012.html"]

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
time_end: 2019-07-16T12:00:00
all_day: false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors: []

# Abstract and optional shortened version.
abstract: ""
summary: "Introduce tree-based classification and demonstrate cross-validation."

# Location of event.
location: "Room 315, Haskell Hall, Chicago, IL"

# Is this a selected talk? (true/false)
selected: false

# Tags (optional).
#   Set `tags: []` for no tags, or use the form `tags: ["A Tag", "Another Tag"]` for one or more tags.
tags: []

# Links (optional).
url_pdf: ""
url_slides: "/slides/statistical-learning-classification-and-cross-validation/"
url_video: ""
url_code: ""

# Does the content use math formatting?
math: false
---



## Overview

* Define a decision tree
* Demonstrate how to estimate a decision tree
* Define and estimate a random forest
* Introduce the `caret` package for statistical learning in R
* Define resampling method
* Compare and contrast the validation set approach with leave-one-out and `\(k\)`-fold cross-validation
* Demonstrate how to conduct cross-validation using `rsample`

## Before class

This is not a math/stats class. In class we will **briefly** summarize how these methods work and spend the bulk of our time on estimating and interpreting these models. That said, you should have some understanding of the mathematical underpinnings of statistical learning methods prior to implementing them yourselves. See below for some recommended readings:

* Chapters 8.1, 8.2.2, and 5.1 in [*An Introduction to Statistical Learning*](http://link.springer.com.proxy.uchicago.edu/book/10.1007%2F978-1-4614-7138-7)

## Class materials

* [Decision trees and random forests](/notes/decision-trees/)
* [Cross-validation methods](/notes/cross-validation/)

* [The `caret` Package](https://topepo.github.io/caret/) - introductory book for the `caret` package. Tells you what models you can implement and all the nitty-gritty details to customize `train` for different cross-validation methods.
* [Working with `rset`s](https://tidymodels.github.io/rsample/articles/Working_with_rsets.html) - documentation for `rsample` and demonstration implementing it for resampling and model assessment

## What you need to do

* [Start homework 6](/homework/statistical-learning/)
