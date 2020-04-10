---
title: "Introduction to R"
teaching: 0
exercises: 0
questions:
- "How to program in R?"
- "How to use functions in R?"
- "What is a data frame?"
- "What are some basic graphics available in R?"
objectives:
- "Successfully run mutliple lines of r code"
- "Successfully use functions in r"
- "Successfully create graphics in r"
keypoints:
- "..."
- 
---

# Calling a function
R is a "functional programming language," meaning it contains a number of *functions* you use to do something with your data. *Call* a function on a variable by entering the function into the console, followed by parentheses and the variables. For example, if you want to take the sum of 3 and 4, you can type in `sum(3, 4)`. 

## Function arguments
Typing a question mark before a function will pull the help page up in the Navigation Pane in the lower right. Type `?sum` to view the help page for the `sum` function. You can also call `help(sum)`. This will provide the description of the function, how it is to be used, and the arguments. 

In the case of `sum()`, the ellipses `. . .` represent an unlimited number of numeric elements. `sum()` also takes the argument `na.rm`. This is a logical (`TRUE/FALSE`) argument specifying if NA values (missing data) should be removed when the argument is evaluated.

The function `is.function()` will check if an argument is a function in R. If it is a function, it will print `TRUE` to the console.

```{r function1, comment=NA, eval = F}
# confirm that sum is a function
is.function(sum)
## [1] TRUE

# sum takes an unlimited number (. . .) of numeric elements
sum(3, 4, 5, 6, 7)
## [1] 25

# evaluating a sum with missing values will return NA
sum(3, 4, NA)
## [1] NA

# but setting the argument na.rm to TRUE will remove the NA
sum(3, 4, na.rm = TRUE)
## [1] 7
```

Functions can be nested within each other. For example, `sqrt()` takes the square root of the number provided in the function call. Therefore you can run `sum(sqrt(9), 4)` to take the sum of the square root of 9 (3) and add it to 4. Or you could write the quadratic formula: `[(-b) + sqrt((b^2) - 4ac)] / (2*a)`.

## A Vector
A vector is a basic data structure in R. It contains elements of the same type. Those elements within a vector are called components. Components can be numbers, logical values, characters, and dates to name a few. Most base functions in R work when given a vector as an arugment. Everything you manipulate in R is called an object and vectors are the most basic type of object.

Let's create a vector to work with.
~~~
myDogs <- c("breed" = c("beagle", "pug", "chihuahua"), "shedding" = c("moderate", "high", "low"))
~~~

## The `c()` function
Another important function is `c()` which will combine arguments to form a vector. In some programs, such as Excel, this is called *concatenation*. If you read the help files for `c()` by calling `help(c)`, you can see that it takes an unlimited `. . .` number of arguments.

```{r function2, comment=NA, eval = F}
# use c() to combine three numbers into a vector, myFives
myFives <- c(5, 10, 15)
 
# adding 5 will operate on each element of the vector. More on vectors below.
myFives + 5
## [1] 10 15 20
```

## The `View()` function
Use this to open a tab in the Script Pane (upper left) to view your data. You can also click on the variable name in the Environment Pane (upper right) to do the same thing. (More on data frames below).

```{r view, comment=NA, eval = F, tidy=F}
myDogs <- data.frame("breed" = c("beagle", "pug", "chihuahua")
                   , "shedding" = c("moderate", "high", "low"))
View(myDogs)
```

## The `str()` function
Type `?str` into the console to read the description of the `str` function. You can call `str()` on an R object to compactly display information about it, including the data type, the number of elements, and a printout of the first few elements. We are going to use `str` in the following sections to investigate R objects, vectors, and data types.
```{r view2, comment=NA, eval = F}
# using str on a function will tell you what arguments it takes
str(sum)

# using str on an R object will give you information about that object
```

# Data frames
A data frame is the term in R for a spreadsheet style of data: a grid of rows and columns. The number of columns and rows is virtually unlimited, but each column must be a vector of the same length. A dataframe can comprise heterogeneous data: in other words, each column can be a different data type. However, because a column is a vector, it has to be a single data type. 

## Create a data frame
You will likely be importing your dataset, but it is easy to create a data frames on your own:

```{r dataframes, comment=NA, eval = F}
# create three vectors
title <- c("Macbeth","Dracula","1984")
author <- c("Shakespeare","Stoker","Orwell")
checkouts <- c(25, 15, 18)
available <- c(TRUE, FALSE, FALSE)

# create a data frame using the data.frame() function. Specify stringsAsFactors as FALSE
ebooks <- data.frame(title, author, checkouts, stringsAsFactors = F)
```

You can print small data frames like this to the console using `print(ebooks)`
```{r dataframes2, comment=NA, eval = T, echo=F}
title <- c("Macbeth","Dracula","1984")
author <- c("Shakespeare","Stoker","Orwell")
checkouts <- c(25, 15, 18)

# create a data frame using the data.frame() function. Specify stringsAsFactors as FALSE
ebooks <- data.frame(title, author, checkouts, stringsAsFactors = F)
print(ebooks)
```

But for larger data frames, it's best to use the `View()` function: `View(ebooks)`. You can also use `head()` to see a preview (in this particular case, the data frame is too small to preview).

All you Excel users might be wondering: how do I click in a cell and edit it?! R doesn't work like that. If you want to manipulate values, it's best to do it with an expression in the R console, and have all modifications documented in your script. We will be going into how to do these modifications next session. But if you insist, you can pull up a traditional point-and-click spreadsheet by using the `edit()` function: `edit(ebooks)`. 

## Exploring data frames
There are a number of ways to explore your data frame:

```{r dataframes3, comment=NA, eval = F}
#display information about the data frame
str(ebooks)

# dimensions: 3 rows, 3 columns
dim(ebooks)
## [1] 3 3

# number of rows
nrow(ebooks)
## [1] 3

# number of columns
ncol(ebooks)
## [1] 3

# column names
names(ebooks)
## [1] "title"     "author"    "checkouts"

ebooks)
## [1] "data.frame"
```

You can use the `$` symbol to work with particular variables.
```{r dataframes4, comment=NA, eval = F}
print(ebooks$title)

ebooks$title)
## [1] "character"

ebooks$checkouts)
## [1] "numeric"

# use summary() for more detail on a variable
summary(ebooks$checkouts)
##  Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## 15.00   16.50   18.00   19.33   21.50   25.00 
```

---

**TRY IT YOURSELF**

1. Look at the help file for `state.name`
2. Manually construct three vectors: `stateName`, `division`, and `area`.
```{r logical1, comment=NA, results='asis', echo=F}
states <- data.frame("stateName" = state.name[c(2,  3,  5,  6, 26)]
                        , "division" = state.division[c(2,  3,  5,  6, 26)]
                        , "area" = as.integer(10000*ceiling(state.area[c(2,  3,  5,  6, 26)]/10000))
                        ,  stringsAsFactors = F)
states
```
3. Use `data.frame()` to create a data frame of these three vectors. Assign it to `myStates`. Remember to set `stringsAsFactors` to `FALSE`
4. What is the `)` of each vector?
5. Using the `$` character, run `sum()` on the `area` variable. What is the sum area of these five states? What is the median?


---
# Ways to get data into R
In order to use your data in R, you must import it and turn it into an R *object*. There are many ways to get data into R.

* **Manually**: You can manually create it as we did at the end of last session. To create a data.frame, use the `data.frame()` and specify your variables. 
* **Import it from a file** Below is a very incomplete list
+ Text: TXT (`readLines()` function)
+ Tabular data: CSV, TSV (`read.table()` function or `readr` package)
+ Excel: XLSX (`xlsx` package)
+ Google sheets: (`googlesheets` package)
+ Statistics program: SPSS, SAS (`haven` package)
+ Databases: MySQL (`RMySQL` package)
* **Gather it from the web**: You can connect to webpages, servers, or APIs directly from within R, or you can create a data scraped from HTML webpages using the `rvest` package. 
- For example, connect to the Twitter API with the [`twitteR`](https://sites.google.com/site/miningtwitter/questions/talking-about/wordclouds/wordcloud1) package, or Altmetrics data with [`rAltmetric`](https://cran.r-project.org/web/packages/rAltmetric/vignettes/intro-to-altmetric.html), or World Bank's World Development Indicators with [`WDI`](https://cran.r-project.org/web/packages/WDI/WDI.pdf).

## `readr`
R has some base functions for reading a local data file into your R session--namely `read.table()` and `read.csv()`, but these have some idiosyncrasies that were improved upon in the `readr` package, which is installed and loaded with `tidyverse`. You can either load `tidyverse`, which will automatically load `readr`, or you can load `readr` individually.

```{r readr, comment=NA, eval=FALSE}
library(tidyverse)

# or

library(readr)
```

For this session, we will be reading a CSV from...
# Data Exploration
After you read in the data, you want to examine it not only to make sure it was read in correctly, but also to gather some basic information about it.

# Data cleaning & transformation
We are now entering the data cleaning and transforming phase. While it is possible to do much of the following using Base R functions (in other words, without loading an external package) `dplyr` makes it much easier. Like many of the most useful R packages, `dplyr` was developed by [http://hadley.nz/](Hadley Wickham), a data scientist and professor at Rice University. 

## Renaming variables
It is often necessary to rename variables to make them more meaningful. If you print the names of the sample `books` dataset you can see that some of the vector names are not particularly helpful:
```{r renaming1, comment=NA, eval=FALSE}
# print names of the books data frame to the console
names(books)
## [1] "CALL...BIBLIO." "title"          "X245.c"         "LOCATION"       "tot_chkout"     "LOUTDATE"    "SUBJECT"        "ISN"            "CALL...ITEM."   "X008.Date.One"  "BCODE2"         "BCODE1"    
```

There are many ways to rename variables in R, but I find the `rename()` function in the `dplyr` package to be the easiest and most straightforward. The new variable name comes first. See `help(rename)`.
```{r renaming2, comment=NA}
# rename the X245.ab variable. Make sure you return (<-) the output to your 
# variable, otherwise it will just print it to the console
books <- dyplr::rename(books,
                       title = X245.ab)

# rename multiple variables at once
books <- dyplr::rename(books,
                       author = X245.c,
                       callnumber = CALL...BIBLIO.,
                       isbn = ISN,
                       pubyear = X008.Date.One,
                       subCollection = BCODE1,
                       format = BCODE2)
books
```

Side note: where does `X245.ab` come from? That is the MARC field 245|ab. However, because R variables cannot start with a number, R automatically inserted and X, and because pipes | are not allowed in variable names, R replaced it with a period. 

R does this automatically when you use `read_csv`, but sometimes you need to force it. The `clean_names()` function from `janitor` can be used to clean names of data frames. As per the help file, "Resulting names are unique and consist only of the _ character, numbers, and letters."

```{r renaming3, comment=NA}
# clean_names() can be used for data frames
books <- janitor::clean_names(books)
books

# make_clean_names() can be used for vectors
my_messy_names <- c("245|ab", "1.-2", "space bar")
janitor::make_clean_names(my_messy_names)
## [1] "x245_ab"   "x1_2"      "space_bar"
```

# Data visualization
