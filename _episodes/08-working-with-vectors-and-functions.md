---
title: "Working with Vectors and Functions"
teaching: 15
exercises: 20
questions:
- "What are functions in R?"
objectives:
- "Successfully use multiple functions in R"
keypoints:
- "You call a function on a variable by entering the function into the console, followed by parentheses and the variables"
- "A vector is the most basic data structure in R. It contains elements of the same type"
- "You can use the brackets to subset a vector"
---


# Functions in R
R is a "functional programming language," meaning it contains a number of *functions* you use to do something with your data. *Call* a function on a variable by entering the function into the console, followed by parentheses and the variables. For example, if you want to take the sum of 3 and 4, you can type in `sum(3, 4)`. 

## Vectors
A vector is the most basic data structure in R. It contains elements of the same type. Those elements within a vector are called components. Components can be numbers, logical values, characters, and dates to name a few. Most base functions in R work when given a vector as an arugment. Everything you manipulate in R is called an object and vectors are the most basic type of object.

To create a vector you'll need to name it and have variables to form the vector, in this case dog breeds and level of shedding. 

>## Exercise
> 1. Try creating this vector `myDogs` by typing it into the console. Our components will be breeds of dog and levels or shedding.
>
~~~
myDogs <- c("breed" = c("beagle", "pug", "chihuahua")
                       , "shedding" = c("moderate", "high", "low"))
~~~
> {: .language-r}
>
{: .checklist}

## The `c()` function
An important function is `c()` which will combine arguments to form a vector. In some programs, such as Excel, this is called *concatenation*. If you read the help files for `c()` by calling `help(c)`, you can see that it takes an unlimited `. . .` number of arguments.

>## Exercise
> 1. Use the `c()` function to combine three numbers into a vector, called myFives
>
~~~
myFives <- c(5, 10, 15)
~~~
> {: .language-r}
>
{: .checklist}
 
You can use an operator like `+` on each element of vector. 

>## Excercise
> 1. Use the `c()` function to add 5 to each element of the vector.
>
~~~
myFives + 5
## [1] 10 15 20
~~~
> {: .language-r}
>
{: .checklist}

## The `View()` function
You can use this function to open a tab in the Script Pane (upper left) to view your data. You can also click on the variable name in the Environment Pane (upper right) to do the same thing. (More on data frames below).

> ##Exercise
>1. Practice using `View()` to open a tab in the Script Pane (upper left) to view your data.
> 
~~~
myDogs <- data.frame("breed" = c("beagle", "pug", "chihuahua")
                   , "shedding" = c("moderate", "high", "low"))
View(myDogs)
~~~
> {: .language-r}
>
{: .checklist}


## The `str()` function
When working with a dataset, many functions have alternative paths for variables of different types. The easiest way to query the structure of an R variable is using `str()`. The `str()` function will return the type of structure (data frame, list, vector, matrix, etc.), and its dimensions, including the number of columns (variables) and the number of rows (observations). Along with the Environment tab in RStudio, the `str()` function is a convenient way to keep track of changes as variables are processed.

Exercise
1. Practice typing in `?str` into the console to read the full description of the `str` function.

~~~
# using str on a function will tell you what arguments it takes
str(sum)

# using str on an R object will give you information about that object
~~~
{: .language-r}


## Subsetting vectors
You can use the brackets to subset a vector. Brackets can take either numeric values (which will correspond to the element in the order it exists in the vector) or logical (T/F) values. You can also use functions such as `which()`, that return numeric values.

Practice using functions you've just learned with the built in dataset `state.name`.


~~~
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
~~~
{: .language-r}

