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

# R Scripting
R is primarily a scripting language, and written line-by-line. This can be quite useful; scripts can be assembled and built upon as you go into more substantial programs or compilations for analysis, but still editable at each line. There is no need to rerun the whole script in order to change a line of code. 

# R Packages
Many useful R code is written by the community through a variety of R packages available through CRAN (the Comprehensive R Archive Network), and other repositories. The ease with which packages can be developed, released, and shared has played a large role in R's popularity. R packages can be thought of as libraries for other languages, as they contain related functions designed to work together. Packages are often created to streamline a common workflow.

# R Workflows
The strength of R is in it's interactive data analysis. A related strength, with packages like *knitr* and *R Markdown*, is in making the process and results easy to reproduce and share with others. 

# Data Structures
Data in R are stored in variables and each variable is a container for data in a particular structure. There are four data structures most commonly used in R: vectors, matrices, data frames, and lists.

# A Function
R is a "functional programming language," meaning it contains a number of *functions* you use to do something with your data. *Call* a function on a variable by entering the function into the console, followed by parentheses and the variables. For example, if you want to take the sum of 3 and 4, you can type in `sum(3, 4)`. 

## A Vector
A vector is the most basic data structure in R. It contains elements of the same type. Those elements within a vector are called components. Components can be numbers, logical values, characters, and dates to name a few. Most base functions in R work when given a vector as an arugment. Everything you manipulate in R is called an object and vectors are the most basic type of object.

To create a vector you'll need to name it and have variables to form the vector, in this case dog breeds and level of shedding. Try creating this vector by typing it into the console.
~~~
myDogs <- c("breed" = c("beagle", "pug", "chihuahua")
                       , "shedding" = c("moderate", "high", "low"))
~~~

## The `c()` function
An important function is `c()` which will combine arguments to form a vector. In some programs, such as Excel, this is called *concatenation*. If you read the help files for `c()` by calling `help(c)`, you can see that it takes an unlimited `. . .` number of arguments.

Use the `c()` function to combine three numbers into a vector, called myFives
~~~
myFives <- c(5, 10, 15)
~~~
 
You can use an operator like `+` on each element of vector. Use the `c()` function to add 5 to each element of the vector.
~~~
myFives + 5
## [1] 10 15 20
~~~

## The `View()` function
You can use this function to open a tab in the Script Pane (upper left) to view your data. You can also click on the variable name in the Environment Pane (upper right) to do the same thing. (More on data frames below).

~~~
myDogs <- data.frame("breed" = c("beagle", "pug", "chihuahua")
                   , "shedding" = c("moderate", "high", "low"))
View(myDogs)
~~~

## The `str()` function
When working with a dataset, many functions have alternative paths for variables of different types. The easiest way to query the structure of an R variable is using `str()`. The `str()` function will return the type of structure (data frame, list, vector, matrix, etc.), and its dimensions, including the number of columns (variables) and the number of rows (observations). Along with the Environment tab in RStudio, the `str()` function is a convenient way to keep track of changes as variables are processed.

Try typing in `?str` into the console to read the full description of the `str` function.

~~~
# using str on a function will tell you what arguments it takes
str(sum)

# using str on an R object will give you information about that object
~~~
## Subsetting vectors
You can use the brackets to subset a vector. Brackets can take either numeric values (which will correspond to the element in the order it exists in the vector) or logical (T/F) values. You can also use functions such as `which()`, that return numeric values.

```{r function4, comment=NA, eval = F}
# state.name is a built in vector in R of all U.S. states
state.name

state.name[1]
## [1] "Alabama"

state.name[1:5]
## [1] "Alabama"    "Alaska"     "Arizona"    "Arkansas"   "California"

# You must use the `c()` function if you have more than one value
state.name[1, 10, 20]
## Error in state.name[1, 10, 20] : incorrect number of dimensions

state.name[c(1, 10, 20)]
## [1] "Alabama"  "Georgia"  "Maryland"

# There's only one state called Alabama
table(state.name == "Alabama")
## FALSE  TRUE 
##    49     1 

# create a logical vector of state names where "Alabama" == TRUE. Notice you have to use two equals signs.
myAlabamaIndex <- state.name == "Alabama"
myAlabamaIndex
## TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE

# subset state.name using that T/F index (will return the only value where myAlabamaIndex == TRUE)
state.name[myAlabamaIndex]
## [1] "Alabama"

# create a logical vector of state names with more than 10 character names
ten_characters <- nchar(state.name) > 10

# you can find out which elements are TRUE values by using the `which()` function
which(ten_characters)

# subset state.names using `which()`
ten_character_state.names <- state.name[ten_characters]

ten_character_state.names
## [1] "Connecticut"    "Massachusetts"  "Mississippi"    "New Hampshire"  "North Carolina" "North Dakota"   "Pennsylvania"  
## [8] "Rhode Island"   "South Carolina" "South Dakota"   "West Virginia" 
```
---

# Matrices
Matrices behave as two-dimensional vectors. They are faster to access and index than data frames (described below), but less flexible in that every value in a matrix must be of the same data type (integer, numeric, character, etc.). If one is changed, implicit conversion to the next data type that could contain all values is performed.

```
mat = matrix(1:100, nrow=10, ncol=10)

rowMeans(mat)

## [1] 46 47 48 49 50 51 52 53 54 55

colMeans(mat)

## [1] 5.5 15.5 25.5 35.5 45.5 55.5 65.5 75.5 85.5 95.5
```
Matrices are indexed by row, then column. Indexes can include numeric sequences or TRUE/FALSE values.

```
mat[1:3, 1:3]

##    [,1] [,2] [,3]
## [1,]   1   11    21
## [2,]   2   12    22
## [3,}   3   13    23
```


# Data frames
A data frame is the term in R for a spreadsheet style of data: a grid of rows and columns. The number of columns and rows is virtually unlimited, but each column must be a vector of the same length. A dataframe can comprise heterogeneous data: in other words, each column can be a different data type. However, because a column is a vector, it has to be a single data type. 

## Lists
Lists are simply vectors of other objects. This means that we may have lists of matrices, lists of dataframes, lists of lists, or a mixture of essentially any data type. This flexibility makes lists a popular structure.

## Create a data frame
You will likely be importing datasets, but it is easy to create a data frame on your own. 

Let's create a data frame. First let's define three vectors using book titles, author names, number of library checkouts, and if the book is available to be checked out.
~~~
title <- c("Macbeth","Dracula","1984")
author <- c("Shakespeare","Stoker","Orwell")
checkouts <- c(25, 15, 18)
available <- c(TRUE, FALSE, FALSE)
~~~
Now, we'll create a data frame called `ebooks`.
~~~
ebooks <- data.frame(title, author, checkouts, stringsAsFactors = F)
~~~
You can print small data frames like this to the console using `print(ebooks)`
```{r dataframes2, comment=NA, eval = T, echo=F}
title <- c("Macbeth","Dracula","1984")
author <- c("Shakespeare","Stoker","Orwell")
checkouts <- c(25, 15, 18)

# create a data frame using the data.frame() function. Specify stringsAsFactors as FALSE
ebooks <- data.frame(title, author, checkouts, stringsAsFactors = F)
print(ebooks)
```

Excel users might be wondering: how do I click in a cell and edit it?! R doesn't work like that. If you want to manipulate values, it's best to do it with an expression in the R console, and have all modifications documented in your script. 

## Exploring data frames
There are a number of ways to explore a data frame:

~~~
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
~~~

You can use the `$` symbol to work with particular variables.
~~~
print(ebooks$title)

ebooks$title)
## [1] "character"

ebooks$checkouts)
## [1] "numeric"

# use summary() for more detail on a variable
summary(ebooks$checkouts)
##  Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## 15.00   16.50   18.00   19.33   21.50   25.00 
~~~

---

> ##EXCERCISE
>
>...

(edit excercise below)
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
* **Import it from a file** Below is a list of options depending on the file type you're working with
+ Text: TXT (`readLines()` function)
+ Tabular data: CSV, TSV (`read.table()` function or `readr` package)
+ Excel: XLSX (`xlsx` package)
+ Google sheets: (`googlesheets` package)
+ Statistics program: SPSS, SAS (`haven` package)
+ Databases: MySQL (`RMySQL` package)
* **Gather it from the web**: You can connect to webpages, servers, or APIs directly from within R, or you can create a data scraped from HTML webpages using the `rvest` package. 

## `readr`
R has some base functions for reading a local data file into your R session: `read.table()` and `read.csv()`in the `readr` package, which is installed and loaded with `tidyverse`. You can either load `tidyverse`, which will automatically load `readr`, or you can load `readr` individually.

~~~
library(tidyverse)

# or

library(readr)
~~~

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