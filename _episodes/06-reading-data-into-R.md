---
title: "Reading Data into R"
teaching: 15
exercises: 15
questions:
- "How to import data into R?"
objectives:
- "Successfully import data into R"
keypoints:
- "There are many ways to get data into R, namely `read.table()` and `read.csv()`"
- "Remember to modify the path name to reflect where the csv file is stored on your computer"
---

# Reading data into R
In order to use your data in R, you must import it and turn it into an R object. There are many ways to get data into R.

## Ways to get data into R
In order to use your data in R, you must import it and turn it into an R *object*. There are many ways to get data into R.

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

## readr
R has some base functions for reading a local data file into your R session--namely `read.table()` and `read.csv()`, but these have some idiosyncrasies that were improved upon in the `readr` package, which is installed and loaded with `tidyverse`. You can either load `tidyverse`, which will automatically load `readr`, or you can load `readr` individually.

~~~
library(tidyverse)

# or

library(readr)
~~~
{: .language-r}

> ## Exercise 
>
> You can import a csv directly into RStudio with this line of script
>
~~~
read.csv("Path where your CSV file is located on your computer\\File Name.csv")
~~~
>
> To try this locate where you downloaded the dataset on your computer. Save the csv file to your desktop. Once saved, locate the file on your desktop and right click on it with your mouse. Select "Properties". To determine the location path you'll need for this script look at "Location". You may want to copy & paste or write this location down to reference later.
>
> Now, try reading in the anderson.refs.csv into RStudio. Remember, my path may look different from yours. Modify the path name to reflect where the csv file is stored on your computer.
>
~~~
read.csv("C:\\Users\\aak98\\Desktop\\anderson_refs.csv", header = TRUE)
~~~
> Notice that I also set the header to ‘TRUE’ as our dataset in the CSV file contains a header.
>
> Also note that the double backslash (‘\\’) within the path name. By adding double backslash you can avoid the following error in R
~~~
Error: ‘\U’ used without hex digits in character string starting “”C:\U”
~~~
> This is one workaround that you may apply in R to bypass this type of error.
>
> What if you want to import a text file into R?
>
> For a text file, you only need to change the file extension from csv to txt (at the end of the path). The path name would look like this
~~~
read.csv("C:\\Users\\aak98\\Desktop\\anderson_refs.txt", header = TRUE)
~~~
> You can also place downloaded files directly in the `search_results_data` folder you just created in your working directory. To do this you would open your computer's downloads folder, locate the file you just downloaded ("`anderson_refs`"), and drag and drop it into your newly created R Project folder ("`search_results_data`"). 
{: .checklist}
