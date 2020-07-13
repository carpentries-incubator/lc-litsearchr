---
title: "Exploring Data in R"
teaching: 15
exercises: 30
questions:
- "How to inspect a list?"
- "How to pull elements out of a list?"
objectives:
- "Successfully install and load the purr, repurrsive, and listviewer packages."
- "Successfully inspect and pull elements out of a list."
- "Successfully use str() to explore lists."
keypoints:
- "Before you can apply a function to every element of a list, you'd better understand the list!"
---

## Load packages

Load `purrr` and `repurrrsive`, which contains recursive list examples we'll use in the following sections.

~~~
install.packages("purr")
install.packages("repurrsive")

library(purrr)
library(repurrrsive)
~~~
{: .language-r}

## Inspect and explore

List inspection is very important. Before you can apply a function to every element of a list, you'd better understand the list!

You need to develop a toolkit for list inspection. Be on the look out for:

  * What is the length of the list?
  * Are the components homogeneous, i.e. do they have the same overall structure, albeit containing different data?
  * Note the length, names, and types of the constituent objects.
  
> I have no idea what's in this list or what its structure is! Please send help.

Understand this is **situation normal**, especially when your list comes from querying a poorly documented API. This is often true even when your list has been created completely within R. How many of us perfectly understand the structure of a fitted linear model object? You just have to embark on a voyage of discovery and figure out what's in there. 

## Indexing

There are 3 ways to pull elements out of a list:

  * The `$` operator. Extracts a single element by name. Name can be unquoted, if syntactic.
    ~~~
    x <- list(a = "a", b = 2)
    x$a
    x$b
    ~~~
    {: .language-r}
    
  * `[[` The double square bracket. Extracts a single element by name or position. Name must be quoted, if provided directly. Name or position can also be stored in a variable.
    ~~~
    x <- list(a = "a", b = 2)
    x[["a"]]
    x[[2]]
    nm <- "a"
    x[[nm]]
    i <- 2
    x[[i]]
    ~~~
    {: .language-r}
    
  * `[` The single square bracket. Regular vector indexing. For a list input, this always returns a list!
    ~~~
    x <- list(a = "a", b = 2)
    x["a"]
    x[c("a", "b")]
    x[c(FALSE, TRUE)]
    ~~~
    {: .language-r}

## `str()`

`str()` can help with basic list inspection. The `max.level` and `list.len` arguments are very helpful to use. You can use them to keep the output of `str()` down to a manageable volume.

Once you begin to suspect or trust that your list is homogeneous, i.e. consists of sub-lists with similar structure, it's often a good idea to do an in-depth study of a single element. In general, remember you can combine list inspection via `str(..., list.len = x, max.level = y)` with single `[` and double `[[` square bracket indexing.

The repurrrsive package provides examples of lists. We explore them below to demonstrate list inspection strategies.

## listviewer and RStudio's Object Explorer

The RStudio IDE (v1.1 and higher) offers an [Object Explorer](https://blog.rstudio.com/2017/08/22/rstudio-v1-1-preview-object-explorer/) that provides interactive inspection and code generation tools for hierarchical objects, such as lists. You can invoke it via the GUI or in code as `View(YOUR_UGLY_LIST)`.
 
However, that won't help you expose list exploration in something like this website. I am using the [listviewer](https://CRAN.R-project.org/package=listviewer) package to do this below. It allows you to expose list exploration in a rendered `.Rmd` document.

~~~
install.packages("listviewer")

library(listviewer)
~~~
{: .language-r}

## Wes Anderson color palettes

`wesanderson` is a simple list containing color palettes from the [wesanderson package](https://cran.r-project.org/package=wesanderson). Each component is a palette, named after a movie, and contains a character vector of colors as hexadecimal triplets.

~~~
str(wesanderson)
~~~
{: .language-r}

### Explore `wesanderson`

~~~
`View(wesanderson)`
~~~
{: .language-r}


## Game of Thrones POV characters

`got_chars` is a list with information on the `r length(got_chars)` point-of-view characters from the first five books in the Song of Ice and Fire series by George R. R. Martin. Retrieved from [An API Of Ice And Fire](https://anapioficeandfire.com). Each component corresponds to one character and contains `r length(got_chars[[1]])` components which are named atomic vectors of various lengths and types.

~~~
str(got_chars, list.len = 3)
str(got_chars[[1]], list.len = 8)
~~~
{: .language-r}

### Explore `got_chars`

~~~
`View(got_chars)`
~~~
{: .language-r}


> ## Challenges
>
> 1. Read the documentation on `str()`. What does `max.level` control? Apply `str()` to `wesanderson` and/or `got_chars` and experiment with `max.level = 0`, `max.level = 1`, and `max.level = 2`. Which will you use in practice with deeply nested lists?
> 2. What does the `list.len` argument of `str()` control? What is its default value? Call `str()` on `got_chars` and then on a single component of `got_chars` with `list.len` set to a value much smaller than the default. What range of values do you think you'll use in real life?
> 3. Call `str()` on `got_chars`, specifying both `max.level` and `list.len`.
> 4. Call `str()` on the first element of `got_chars`, i.e. the first Game of Thrones character. Use what you've learned to pick an appropriate combination of `max.level` and `list.len`.
>
{: .challenge}
