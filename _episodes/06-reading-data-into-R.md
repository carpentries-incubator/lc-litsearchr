---
title: "Importing Data into R"
teaching: 15
exercises: 15
questions:
- "How to import data into R?"
objectives:
- "Successfully import data into R"
keypoints:
- "There are many ways to get data into R. You can import data from a .csv file using the read.csv(...) function.
- "Understand some of the key arguments available for importing the data, including header, stringsAsFactors, as.is, and strip.white."
---

## Importing data into R
In order to use your data in R, you must import it and turn it into an R object. There are many ways to get data into R.

## Ways to get data into R
* **Manually**: You can manually create it. To create a data.frame, use the `data.frame()` and specify your variables. 
* **Import it from a file** Below is a very incomplete list
+ Text: TXT (`readLines()` function)
+ Tabular data: CSV, TSV (`read.table()` function or `readr` package)
+ Excel: XLSX (`xlsx` package)
+ Google sheets: (`googlesheets` package)
+ Statistics program: SPSS, SAS (`haven` package)
+ Databases: MySQL (`RMySQL` package)
* **Gather it from the web**: You can connect to webpages, servers, or APIs directly from within R, or you can create a data scraped from HTML webpages using the `rvest` package. 
- For example, connect to the Twitter API with the [`twitteR`](https://sites.google.com/site/miningtwitter/questions/talking-about/wordclouds/wordcloud1) package, or Altmetrics data with [`rAltmetric`](https://cran.r-project.org/web/packages/rAltmetric/vignettes/intro-to-altmetric.html), or World Bank's World Development Indicators with [`WDI`](https://cran.r-project.org/web/packages/WDI/WDI.pdf).

## Opening a .csv file

