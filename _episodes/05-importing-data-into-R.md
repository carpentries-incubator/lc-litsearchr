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

> ## Make sure the files you downloaded from the zip folder are organized correctly before continuing on. 
>
> If you need to reorganize your files the instructions are below:
>
> Create three folders on your computer desktop and name them `data`, `anderson_naive`, and `search_results`
>  
> Add the following files you downloaded at the beginning of the lesson to the `data `folder. 
> * anderson_refs.csv
> * anderson_refs.rda
> * andersosn_studies.rda
> * suggested_keywords_grouped
>
> Add the three downloaded files from the anderson_naive zip folder to the `anderson_naive` folder.
> * MEDLINE_1-500
> * MEDLINE_501-603
> * PsycINFO
>
> Add the three downloaded savedrecs files to the `search_results` folder. 
> * savedrecs(1)
> * savedrecs(2)
> * savedrecs(3)
>
> Create a folder on your desktop called `lc_litsearchr`. Add your three new folders, `data`, `anderson_naive`, and `search_results` to the `lc_litsearchr` folder.
>
> If you need to download the files they can be found in [Data](https://ameliakallaher.github.io/lc-litsearchr/index.html) 
>
{: .callout}

## Opening a .csv file
To open a .csv file we will use the built in `read.csv(...)` function, which reads the data in as a data frame, and assigns the data frame to a variable using the `<-` so that it is stored in R’s memory. 

~~~
## import the data and look at the first six rows
## use the tab key to get the file option
anderson_refs <- read.csv(file = "./data/anderson_refs.csv", header = TRUE, sep = ",")

head(anderson_refs)
~~~
{: .language-r}

~~~
## We can see what R thinks of the data in our dataset by using the class() function with $ operator.

# use the column name `year`
class(anderson_refs$year)

# use the column name `source`
class(anderson_refs$source)
~~~
{: .language-r}

> ## The `header` Argument
> The default for `read.csv(...)` is to set the header argument to `TRUE`. This means that the first row of values in the .csv is set as header information (column names). 
> If your data set does not have a header, set the header argument to `FALSE`.
>
{: .callout}

> ## The `na.strings` Argument
> We often need to deal with missing data in our dataset. A useful argument for the `read.csv()` function is `na.strings`, which allows you to specify how you have represented missing values in the dataset you're importing, and recode those values as NA, which is how R recognizes missing values. For example, if our anderson_refs dataset had missing values coded as lowercase 'na', we can recode these to uppercase 'NA' using the na.strings arguments as follows:

```{r na.strings}
write.csv(anderson_refs, file = 'data/anderson_refs_clean.csv', na.strings = "na")
```
>
{: .callout}

> ## The `write.csv` function
> After altering a dataset by replacing columns or updating values you can save the new output with `write.csv(...)`.
> 
{: .callout}

> ## The `row.names` Argument
> This argument for the `write.csv` function allows us to set the names of the rows in the output data file. R’s default for this argument is TRUE, and since it does not know what else to name the rows for the a dataset, it resorts to using row numbers. To correct this, we can set row.names to FALSE:

```{r row.namesFALSE}
write.csv(anderson_refs, file = 'data/anderson_refs_clean.csv', row.names = FALSE)
```
>
{: .callout}

>  ~~~
> ## To export the data use the write.csv() function. It requires a minimum of two arguments for the data to be saved and the name of the output file.
> 
> ## For exmaple, if we had edited the anderson_refs csv file we could use:
> write.csv(anderson_refs, file = "./data/anderson-refs-cleaned.csv")
> ~~~
> {: .language-r}
>
{: .callout}

