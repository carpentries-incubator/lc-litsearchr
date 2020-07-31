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

# Data frames, Matrices, and Lists
Dataframes and matrices represent 'rectangular' data types, meaning that they are used to store tabular data, with rows and columns. The main difference is that matrices can only contain a single class of data, while data frames can consist of many different classes of data.

A data frame is the term in R for a spreadsheet style of data: a grid of rows and columns. The number of columns and rows is virtually unlimited, but each column must be a vector of the same length. A dataframe can comprise heterogeneous data: in other words, each column can be a different data type. However, because a column is a vector, it has to be a single data type. 

Matrices behave as two-dimensional vectors. They are faster to access and index than data frames, but less flexible in that every value in a matrix must be of the same data type (integer, numeric, character, etc.). If one is changed, implicit conversion to the next data type that could contain all values is performed.

Lists are simply vectors of other objects. Lists are the R objects which contain elements of different types like − numbers, strings, vectors and another list inside it. This means that we may have lists of matrices, lists of dataframes, lists of lists, or a mixture of essentially any data type. This flexibility makes lists a popular structure. List is created using the `list()` function.

~~~
## Create a vector containing the numbers 1 through 20 using the `:` operator. Store the result in a variable called my_vector.
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
`dim` attribute (so it is just NULL),
~~~
{: .language-r}

~~~
## Find length of the vector using the length() function. 
length(my_vector)
[1] 20
~~~
{: .language-r}

~~~
## If we give my_vector a `dim` attribute, the first number is the number of rows and the second is the number of columns. Therefore, we just gave my_vector 4 rows and 5 columns.
dim(my_vector) <- c(4, 5)
~~~
{: .language-r}

~~~
## Now it's we have turned the vector into a matrix. View the contents of my_vector now to see what it looks like.

my_vector
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
## We can store it in a new variable that helps us remember what it is. 
my_matrix <- my_vector
~~~
{: .language-r}

A more direct method of creating the same matrix uses the `matrix()` function.

~~~
## Let's create a matrix containing the same numbers (1-20) and dimensions (4 rows, 5 columns) by calling the matrix() function. 
We'll store the result in a variable called my_matrix2.

my_matrix2 <- matrix(1:20, nrow = 4, ncol = 5, byrow = FALSE)
~~~
{: .language-r}

Now, imagine that the numbers in our table represent some measurements from a
a library check out, where each row represents one library patron and each column represents
one variable for how many items they've checked out a particular library item.

~~~
## We may want to label the rows, so that we know which numbers belong to which library patron.
## To do this add a column to the matrix, which contains the names of all four library patrons.

## First, we will create a character vector containing the names of our library patrons -- Erin, Kate, Kelly, and Matt. 
## Remember that double quotes tell R that something is a character string. Store the result in a variable called patients.

library_patrons <- c("Erin", "Kate", "Kelly", "Matt")
~~~
{: .language-r}

~~~
## Use the cbind() function to 'combine columns'. Don't worry about storing the result in a new variable. 
## Just call cbind() with two arguments -- the library patrons vector and my_matrix.
cbind(library_patrons, my_matrix)

    library_patrons                     
[1,] "Erin"   "1" "5" "9"  "13" "17"
[2,] "Kate"   "2" "6" "10" "14" "18"
[3,] "Kelly"  "3" "7" "11" "15" "19"
[4,] "Matt"   "4" "8" "12" "16" "20"
~~~
{: .language-r}

~~~
## Remember, matrices can only contain ONE class of data. When we tried to combine a character vector with a numeric matrix, R was forced to 'coerce' the numbers to characters,
hence the double quotes.

## Instead we will create a data frame.
my_data <- data.frame(library_patrons, my_matrix)
~~~
{: .language-r}

~~~
## View the contents of my_data to see what we've come up with.
my_data

  library_patrons X1 X2 X3 X4 X5
1     Erin  1  5  9 13 17
2     Kate  2  6 10 14 18
3    Kelly  3  7 11 15 19
4     Matt  4  8 12 16 20

## the data.frame() function allowed us to store our character vector of names right alongside our matrix of numbers.
~~~
{: .language-r}

The `data.frame()` function takes any number of arguments and returns a single object of class `data.frame` that is composed of the original objects.

~~~
## confirm this by calling the class() function on our newly created data frame.
class(my_data)
[1] "data.frame"
~~~
{: .language-r}

We can also assign names to the columns of our data frame so that we know what type of library material each column represents.

~~~
## First, we'll create a character vector called cnames that contains the  following values (in order) -- "name", "book", "dvd", "laptop", "article", "reference".

cnames <- c("name", "book", "dvd", "laptop", "article", "reference")
~~~
{: .language-r}

~~~
## Use the colnames() function to set the `colnames` attribute for our data frame.
colnames(my_data) <- cnames
~~~
{: .language-r}

~~~
## Print the contents of my_data to see if all looks right.

my_data

    name  book  dvd laptop article reference
1    Erin   1    5     9     13       17
2    Kate   2    6    10     14       18
3   Kelly   3    7    11     15       19
4    Matt   4    8    12     16       20
~~~
{: .language-r}
