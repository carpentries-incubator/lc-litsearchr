---
title: "Dataframes, Matrices, and Lists"
teaching: 15
exercises: 15
questions:
- "What is a dataframe in R?"
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

# Data frames & Matrices 
Dataframes and matrices represent 'rectangular' data types, meaning that they are used to store tabular data, with rows and columns. The main difference is that matrices can only contain a single class of data, while data frames can consist of many different classes of data.

A data frame is the term in R for a spreadsheet style of data: a grid of rows and columns. The number of columns and rows is virtually unlimited, but each column must be a vector of the same length. A dataframe can comprise heterogeneous data: in other words, each column can be a different data type. However, because a column is a vector, it has to be a single data type. 

Matrices behave as two-dimensional vectors. They are faster to access and index than data frames, but less flexible in that every value in a matrix must be of the same data type (integer, numeric, character, etc.). If one is changed, implicit conversion to the next data type that could contain all values is performed.

~~~
## Create a vector containing the numbers 1 through 20 using the `:` operator.
Store the result in a variable called my_vector.
my_vector <- 1:20
~~~
{: .language-r}

~~~
## View the contents of the vector you just created.
my_vector
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
~~~
{: .language-r}

~~~
## The dim() function tells us the 'dimensions' of an object.
dim(my_vector)
NULL

## Since my_vector is a vector, it doesn't have a
`dim` attribute (so it's just NULL),
~~~
{: .language-r}

~~~
## Find length of the vector using the length() function. 
length(my_vector)
[1] 20
~~~
{: .language-r}

~~~
## If we give my_vector a `dim` attribute, the first number is the number of rows and the second is the number of
columns. Therefore, we just gave my_vector 4 rows and 5 columns.
> dim(my_vector) <- c(4, 5)
~~~
{: .language-r}

~~~
## Now it's we have turned the vector into a matrix. View the contents of my_vector now to see what it looks like.

> my_vector
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    5    9   13   17
[2,]    2    6   10   14   18
[3,]    3    7   11   15   19
[4,]    4    8   12   16   20
~~~
{: .language-r}

~~~
## We confirm it's actually a matrix by using the class() function. 
class(my_vector)
[1] "matrix"
~~~
{: .language-r}

~~~
We will store it in a new variable that
helps us remember what it is. 
my_matrix <- my_vector
~~~
{: .language-r}

A more direct method of creating the same matrix uses the `matrix()` function.


## Lists
Lists are simply vectors of other objects. Lists are the R objects which contain elements of different types like − numbers, strings, vectors and another list inside it. This means that we may have lists of matrices, lists of dataframes, lists of lists, or a mixture of essentially any data type. This flexibility makes lists a popular structure. List is created using the `list()` function.

~~~

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


