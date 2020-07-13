---
title: "Interacting with R"
teaching: 15
exercises: 10
questions:
- "How to program in R?"
objectives:
- "Successfully run multiple lines of R code"
keypoints:
- "..."
- 
---

## R Scripting
R is primarily a scripting language, and written line-by-line. This can be quite useful; scripts can be assembled and built upon as you go into more substantial programs or compilations for analysis, but still editable at each line. There is no need to rerun the whole script in order to change a line of code. 

## R Packages
Many useful R code is written by the community through a variety of R packages available through CRAN (the Comprehensive R Archive Network), and other repositories. The ease with which packages can be developed, released, and shared has played a large role in R's popularity. R packages can be thought of as libraries for other languages, as they contain related functions designed to work together. Packages are often created to streamline a common workflow.

## R Workflows
The strength of R is in it's interactive data analysis. A related strength, with packages like *knitr* and *R Markdown*, is in making the process and results easy to reproduce and share with others. 

## Data Structures
Data in R are stored in variables and each variable is a container for data in a particular structure. There are four data structures most commonly used in R: vectors, matrices, data frames, and lists.

# Interacting with R
You can use R like a calculator when you type *expressions* into the prompt, and press the Crtl + Enter keys (Windows & Linux) or Cmd+Return keys (Mac) to *evaluate* those expressions. Whenever you see the word `Enter` in the following steps of this lesson use the keys that work for your operating system in its place. 

~~~
2 + 2
## [1] 4
~~~
{: .language-r}

You can use R to *assign values*, such as a numeric value like 5, and *create objects*. We will use the assingment operator to do this.This is the angle bracket (AKA the "less than"" symbol): `<`, which you'll get by pressing **Shift + comma** and the hyphen `-` which is located next to the zero key. There is no space between them, and it is designed to look like a left pointing arrow `<-`.   

~~~
# assign 5 to y by typing this in the console and pressing Enter
y <- 5
~~~
{: .language-r}

You have now created a symbol called `y` and *assigned* the numeric value 5 to it. When you assign something to a symbol, nothing happens in the console, but in the Enviroment pane in the upper right, you will notice a new *object*, y. 

You can use R to evaluate expressions. Try typing `y` into the console, and press Enter on your keyboard, R will *evaluate* the expressions. In this case, R will *print* the elements that are assigned to `y`. 

~~~
# evaluate y
y
## [1] 5

# you can alos use the print() function
print(y)
## [1] 5
~~~
{: .language-r}

We can do this easily since `y` only has one element, but if you do this with a large dataset loaded into R, it will obliterate your console because it will print the entire dataset. 

You can use R to type *commands* into your code by using the hash symbol `#`. Anything following the hash symbol will not be evaluated. Adding notes, comments, and directions along the way helps to explain your code to someone else as well as document your own steps like a manual you can refer back to. Commenting code, along with documenting how data is collected and explaining what each variable represents, is essential to [reproducibile research](https://ropensci.github.io/reproducibility-guide/sections/introduction/).

# Challenge
> If you need some data to play with, type data() in the console for a list of data sets. To load a dataset, type it like this: `data(mtcars)`. Type `help(mtcars)` to learn more about it. You can then perform operations, e.g. 
> > ## Solution 
> >
~~~
head(mtcars)
nrow(mtcars)
mean(mtcars$mpg)
sixCylinder <- mtcars[mtcars$cyl == 6, ]
~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

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








