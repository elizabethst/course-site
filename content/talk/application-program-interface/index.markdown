---
title: "Getting data from the web: API access"
date: 2019-07-17T10:00:00
publishDate: 2019-06-01T10:00:00
draft: false
type: "talk"

aliases: ["/cm015.html"]

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
time_end: 2019-07-17T12:00:00
all_day: false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors: []

# Abstract and optional shortened version.
abstract: ""
summary: "Define an application program interface, write functions to query APIs, and practice tidying JSON objects."

# Location of event.
location: "Room 315, Haskell Hall, Chicago, IL"

# Is this a selected talk? (true/false)
selected: false

# Tags (optional).
#   Set `tags: []` for no tags, or use the form `tags: ["A Tag", "Another Tag"]` for one or more tags.
tags: []

# Links (optional).
url_pdf: ""
url_slides: "/slides/getting-data-from-the-web-api-access/"
url_video: ""
url_code: ""

# Does the content use math formatting?
math: false
---



## Overview

* Identify multiple methods for obtaining data from the internet
* Define application program interface (API)
* Explain authentication keys and demonstrate secure methods for storing these keys
* Demonstrate how to use canned packages in R to access APIs
* Practice gathering data from Twitter API using the `rtweet` package in R
* Identify methods for writing functions to interact with APIs
* Define JSON and XML data structure and how to convert them to data frames
* Practice tidying messy JSON data objects using `purrr::map()`

## Before class

* Read [Getting data from the web: API access](/notes/application-program-interface/)
* Read [Getting data from the web: writing API queries](/notes/write-an-api-function/)

## Class materials

* [Practice getting data from the Twitter API](/notes/twitter-api-practice/)
* [Simplifying lists with `purrr`](/notes/simplify-nested-lists/)

* [More install-and-play API packages for R](https://github.com/ropensci/webservices)
* [Documentation for `httr`](https://cran.r-project.org/web/packages/httr/)
* [Lot's more tutorials and practice with `purrr` and recursive lists](https://jennybc.github.io/purrr-tutorial/index.html)

## What you need to do
