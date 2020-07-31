---
title: "Interacting with R"
teaching: 15
exercises: 10
questions:
- "How to program in R?"
objectives:
- "Successfully run multiple lines of R code"
keypoints:
- "R is primarily a scripting language, and written line-by-line."
- "There is no need to rerun the whole script in order to change a line of code."
- "The strength of R is in it's interactive data analysis."
- "You can use R to *assign values*, such as a numeric value like 4, and *create objects*."
---

## Interacting with R
R is primarily a scripting language, and written line-by-line. This can be quite useful; scripts can be assembled and built upon as you go into more substantial programs or compilations for analysis, but still editable at each line. There is no need to rerun the whole script in order to change a line of code. Many useful R code is written by the community through a variety of R packages available through CRAN (the Comprehensive R Archive Network), and other repositories. The ease with which packages can be developed, released, and shared has played a large role in R's popularity. R packages can be thought of as libraries for other languages, as they contain related functions designed to work together. Packages are often created to streamline a common workflow.

The strength of R is in it's interactive data analysis. A related strength, with packages like *knitr* and *R Markdown*, is in making the process and results easy to reproduce and share with others. Data in R are stored in variables and each variable is a container for data in a particular structure. There are four data structures most commonly used in R: vectors, matrices, data frames, and lists.

As we saw earlier in the lesson, you can use R like a calculator when you type *expressions* into the prompt, and press the Crtl + Enter keys (Windows & Linux) or Cmd+Return keys (Mac) to *evaluate* those expressions. Whenever you see the word `Enter` in the following steps of this lesson use the keys that work for your operating system in its place. 

~~~
6 + 6
## [1] 12
~~~
{: .language-r}

You can use R to *assign values*, such as a numeric value like 4, and *create objects*. We will use the assingment operator to do this.This is the angle bracket (AKA the "less than"" symbol): `<`, which you'll get by pressing **Shift + comma** and the hyphen `-` which is located next to the zero key. There is no space between them, and it is designed to look like a left pointing arrow `<-`.   

~~~
# assign 4 to y by typing this in the console and pressing Enter
y <- 4
~~~
{: .language-r}

You have now created a symbol called `y` and *assigned* the numeric value 4 to it. When you assign something to a symbol, nothing happens in the console, but in the Enviroment pane in the upper right, you will notice a new *object*, y. 

You can use R to evaluate expressions. Try typing `y` into the console, and press Enter on your keyboard, R will *evaluate* the expressions. In this case, R will *print* the elements that are assigned to `y`. 

~~~
# evaluate y
y
## [1] 4
~~~
{: .language-r}

We can do this easily since `y` only has one element, but if you do this with a large dataset loaded into R, it will obliterate your console because it will print the entire dataset. 

You can use R to type *commands* into your code by using the hash symbol `#`. Anything following the hash symbol will not be evaluated. Adding notes, comments, and directions along the way helps to explain your code to someone else as well as document your own steps like a manual you can refer back to. Commenting code, along with documenting how data is collected and explaining what each variable represents, is essential to [reproducibile research](https://ropensci.github.io/reproducibility-guide/sections/introduction/).

## Vectors
The simplest and most common data structure in R is the vector. It contains elements of exactly one data type. Those elements within a vector are called components. Components can be numbers, logical values, characters, and dates to name a few. Most base functions in R work when given a vector as an arugment. Everything you manipulate in R is called an object and vectors are the most basic type of object. In this episode we'll take a closer look at logical and character vectors.

### The `c()` function
The c() function is used for creating a vector. Read the help files for `c()` by calling `help(c)` or `?c` to learn more. 

~~~
## create a numeric vector num_vect that contains the values 0.5, 55, -10, and 6. 
num_vect <- c(0.5, 55, -10, 6)
~~~
{: .language-r}

~~~
## create a variable called tf that gets the result of num_vect < 1, which is read as 'num_vect is less than 1'.
tf <- (num_vect < 1)
~~~
{: .language-r}

~~~
## Print the contents of tf.
tf
[1]  TRUE FALSE  TRUE FALSE

## tf is a vector of 4 logical values
~~~
{: .language-r}

The statement num_vect < 1 is a condition and tf tells us whether each corresponding element of our numeric vector num_vect satisfies this condition. The first element of num_vect is 0.5, which is less than 1 and therefore the statement 0.5 < 1 is TRUE. The second element of num_vect is 55, which is greater than 1, so the statement 55 <1 is FALSE. The same logic applies for the third and fourth elements.

Character vectors are also very common in R. Double quotes are used to distinguish character objects, as in the following example.

~~~
## Create a character vector that contains the following words: "My", "name", "is". Remember to enclose each word in its own set of double quotes, so that R knows they are character strings. Store the vector in a variable called my_char.

my_char <- c("My", "name", "is")

my_char
[1] "My"   "name" "is" 
~~~
{: .language-r}

Right now, my_char is a character vector of length 3. Let's say we want to join the elements of my_char together into one continuous character string (a character vector of length 1). We can do this using the paste() function.

~~~
## Type paste(my_char, collapse = " "). Make sure there's a space between the double quotes in the `collapse` argument.

paste(my_char, collapse= " ")
[1] "My name is"

## The `collapse` argument to the paste() function tells R that when we join together the elements of the my_char character vector, we would like to separate them with single spaces.
~~~
{: .language-r}

~~~
## To add your name to the end of my_char, use the c() function like this: c(my_char, "your_name_here"). Place your name in double quotes, "your_name_here". Try it and store the result in a new variable called my_name.

my_name <- c(my_char, "Amelia")

## Take a look at the contents of my_name.
my_name
[1] "My"     "name"   "is"     "Amelia"

## Now, use the paste() function once more to join the words in my_name together into a single character string. 

paste(my_name, collapse = " ")
[1] "My name is Amelia"

## We used the paste() function to collapse the elements of a single character vector.
~~~
{: .language-r}

In the simplest case, we can join two character vectors that are each of length 1 (i.e. join two words). paste() can also be used to join the elements of multiple character vectors.

~~~
## Try paste("Hello", "world!", sep = " "), where the `sep` argument tells R that we want to separate the joined elements with a single space.

> paste("Hello", "world!", sep = " ")
[1] "Hello world!"
~~~
{: .language-r}

## Functions
Functions are one of the fundamental building blocks of the R language. They are small pieces of reusable code that can be treated like any other R object. Functions are usually characterized by the name of the function followed by parentheses.

~~~
## The Sys.Date() function returns a string representing today's date. Type Sys.Date() below and see what happens.
Sys.Date()
~~~
{: .language-r}

Most functions in R return a value. Functions like Sys.Date() return a value based on your computer's environment, while other functions manipulate input data in order to compute a return value.

The mean() function takes a vector of numbers as input, and returns the average of all of the numbers in the input vector. Inputs to functions are often called arguments. Providing arguments to a function is also sometimes called passing arguments to that function. 

~~~
## Arguments you want to pass to a function go inside the functions parentheses. Try passing the argument c(2, 4, 5) to the mean() function.

> mean(c(2, 4, 5))
[1] 3.666667
~~~
{: .language-r}

We've used a couple of functions already in this lesson while you were getting familiar with the RStudio environment. Let's revisit some of them more closely. 

We can use `names()` to view the column head names in our csv file.
~~~
## to view the column head names in anderson_refs use the names() function
names(anderson_refs)
~~~
{: .language-r}

Since we're dealing with categorical data in our csv file we can use the `levels()` function to view all the categories within a particular categorical column.
~~~
## to see all of the journals from the search results in anderson_refs use the levels() function
levels(anderson_refs$source)
~~~
{: .language-r}

However, if we try to use the levels() function on a non-categorical column like `volume` R will return a `NULL` 
~~~
## try using levels() with a the volumn number column
levels(anderson_refs$volume)

> levels(anderson_refs$volume)
NULL
~~~
{: .language-r}

We can use the `sort()` function to view all of the publication years sorted from oldest to most recent.
~~~
## to arrange publication years by asending order use the sort() function
sort(anderson_refs$year)
~~~
{: .language-r}

We can use the `table()` function to make a table from one of our categorical columns.
~~~
## to create a table counting how many times a journal appears in our search results
table(anderson_refs$source)
~~~
{: .language-r}

## Learning R
1. `swirl` is a package you can install in R to learn about R and data science interactively. Just type `install.packages("swirl")` into your R console, load the package by typing `library("swirl")`, and then type `swirl()`. Read more at <http://swirlstats.com/>.

2. [Try R](http://tryr.codeschool.com/) is a browser-based interactive tutorial developed by Code School.

3. Anthony Damico's [twotorials](https://www.youtube.com/playlist?list=PLcgz5kNZFCkzSyBG3H-rUaPHoBXgijHfC) are a series of 2 minute videos demonstrating several basic tasks in R.

4. [Cookbook for R](http://www.cookbook-r.com/) by Winston Change provides solutions to common tasks and problems in analyzing data

5. If you're up for a challenge, try the free [R Programming MOOC in Coursera](https://www.coursera.org/learn/r-programming) by Roger Peng.

6. Books:
* [R For Data Science](http://r4ds.had.co.nz/) by Garrett Grolemund & Hadley Wickham [free]
* [An Introduction to Data Cleaning with R](https://cran.r-project.org/doc/contrib/de_Jonge+van_der_Loo-Introduction_to_data_cleaning_with_R.pdf) by Edwin de Jonge & Mark van der Loo [free]
* [YaRrr! The Pirate's Guide to R](https://bookdown.org/ndphillips/YaRrr/) by Nathaniel D. Phillips [free]
* Springer's [Use R!](https://link.springer.com/bookseries/6991) series [not free] is mostly specialized, but it has some excellent introductions including Alain F. Zuur et al.'s [A Beginner's Guide to R](https://link.springer.com/book/10.1007/978-0-387-93837-0) and Phil Spector's [Data Manipulation in R](https://link.springer.com/book/10.1007/978-0-387-74731-6)








