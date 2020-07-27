---
title: "Importing Data into R"
teaching: 15
exercises: 15
questions:
- "How to import data into R?"
objectives:
- "Successfully import data into R"
keypoints:
- "There are many ways to get data into R. You can import data from a .csv file using the read.csv(...) function."
---

## Importing data into R
In order to use your data in R, you must import it and turn it into an R object. There are many ways to get data into R.

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

> ## Make sure the files you downloaded are organzied correctly before continuing on.
>
> Create three folders on your computer and name them `data`, `anderson_naive`, and `search_results`
>  
> Add the following files you downloaded at the beginning of the lesson to the `data `folder. 
> * anderson_refs.csv
> * anderson_refs.rda
> * andersosn_studies.rda
>
> Add the three downloaded files from the anderson_naive zip folder to the `anderson_naive` folder.
> * MEDLINE_1-500
> * MEDLINE_501-603
> * PsycINFO
>
> Add the three downloaded files from the search_results zip folder to the `search_results` folder. 
> * savedrecs(1)
> * savedrecs(2)
> * savedrecs(3)
>
> If you need to download the files they can be found in [Data](https://ameliakallaher.github.io/lc-litsearchr/index.html) 
>
{: .callout}

## Opening a .csv file
To open a .csv file we will use the built in `read.csv(...)` function, which reads the data in as a data frame, and assigns the data frame to a variable using the `<-` so that it is stored in R’s memory. 

~~~
## import the data and look at the first six rows
## use the tab key to get the file option
anderson_refs <- read.csv(file = 'data/anderson_refs.csv')
head(anderson_refs)
##
~~~
{: .language-r}

> ## The header Argument
> The default for `read.csv(...)` is to set the header argument to `TRUE`. This means that the first row of values in the .csv is set as header information (column names). 
> If your data set does not have a header, set the header argument to `FALSE`.
>
{: .callout}


