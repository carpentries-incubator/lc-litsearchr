---
title: "Dataframes & Matrices"
teaching: 
exercises: 0
questions:
- "What is a dataframe in R?"
- "What is a list in R?"
- "How do you create a dataframe?"
- "What are matrices in R?"
objectives:
- "Successfully create a dataframe"
- "Successfully explore a dataframe"
- "Successfully use matrices in R"
keypoints:
- "A data frame is the term in R for a spreadsheet style of data: a grid of rows and columns."
- "Lists are the R objects which contain elements of different types like − numbers, strings, vectors and another list inside it."
- "Matrices behave as two-dimensional vectors"
---

# Data frames
A data frame is the term in R for a spreadsheet style of data: a grid of rows and columns. The number of columns and rows is virtually unlimited, but each column must be a vector of the same length. A dataframe can comprise heterogeneous data: in other words, each column can be a different data type. However, because a column is a vector, it has to be a single data type. 

~~~
Name          Count
Apples         12
Oranges        14
Pears          10
~~~
{: .language-r}

## Lists
Lists are simply vectors of other objects. Lists are the R objects which contain elements of different types like − numbers, strings, vectors and another list inside it. This means that we may have lists of matrices, lists of dataframes, lists of lists, or a mixture of essentially any data type. This flexibility makes lists a popular structure. List is created using the `list()` function.

~~~
# Create a list containing strings, numbers, vectors and a logical values.
list_data <- list("Blue", "Pink", c(14,39,11), TRUE, 13.78, 153.2)
print(list_data)
~~~
{: .language-r}

## Create a data frame
You will likely be importing datasets for work with systematic reviews, but it is easy to create a data frame on your own if needed. 

Let's create a data frame. 

First let's define three vectors using book titles, author names, number of library checkouts, and if the book is available to be checked out.

~~~
title <- c("Macbeth","Dracula","1984")
author <- c("Shakespeare","Stoker","Orwell")
checkouts <- c(25, 15, 18)
available <- c(TRUE, FALSE, FALSE)
~~~
{: .language-r}

Now, we'll create a data frame called `ebooks`.

~~~
ebooks <- data.frame(title, author, checkouts, stringsAsFactors = F)
~~~
{: .language-r}

You can also `print` small data frames like this to the console using `print(ebooks)`

~~~
title <- c("Macbeth","Dracula","1984")
author <- c("Shakespeare","Stoker","Orwell")
checkouts <- c(25, 15, 18)
~~~
{: .language-r}

~~~
# create a data frame using the data.frame() 
ebooks <- data.frame(title, author, checkouts, stringsAsFactors = F)
print(ebooks)
~~~
{: .language-r}

For larger data frames, it’s best to use the View() function: View(ebooks). You can also use head() to see a preview (in this particular case, the data frame is too small to preview).

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
{: .language-r}

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
{: .language-r}

---

> ## Excercise
>
> 1. Look at the help file for `state.name`
> 2. Manually construct three vectors: `stateName`, `division`, and `area`.
> 
> need to add image here
>
> 3. Use `data.frame()` to create a data frame of these three vectors. Assign it to `myStates`. Remember to set `stringsAsFactors` to `FALSE`
> 4. What is the `)` of each vector?
> 5. Using the `$` character, run `sum()` on the `area` variable. What is the sum area of these five states? What is the median?
>
{: .checklist}

---

# Matrices
Matrices behave as two-dimensional vectors. They are faster to access and index than data frames, but less flexible in that every value in a matrix must be of the same data type (integer, numeric, character, etc.). If one is changed, implicit conversion to the next data type that could contain all values is performed.

~~~
rowMeans(mat)

## [1] 46 47 48 49 50 51 52 53 54 55

colMeans(mat)

## [1] 5.5 15.5 25.5 35.5 45.5 55.5 65.5 75.5 85.5 95.5
~~~
{: .language-r}

Matrices are indexed by row, then column. Indexes can include numeric sequences or TRUE/FALSE values.

~~~
mat[1:3, 1:3]

##    [,1] [,2] [,3]
## [1,]   1   11    21
## [2,]   2   12    22
## [3,}   3   13    23
~~~
{: .language-r}
