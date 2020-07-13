---
title: "Installing Packages"
teaching: 10
exercises: 15
questions:
- "How to install packages?"
objectives:
- "Successfully install packages in RStudio"
keypoints:
- "Install tidyverse, a package of packages, including many that you are likely to use as you come to work with R"
- "Install devtools, a package needed to install litsearchr"
- "Install litsearchr, part of the metaverse, which is a set of R packages that span the entire scope of evidence synthesis in R"
---
# Packages
When you download R it already has a number of functions built in: these encompass what is called Base R. However, many R users write their own libraries of functions, package them together in R Packages, and provide them to the R community at no charge. This extends the capacity of R and allows us to do much more. In many cases, they improve on the Base R functions by making them easier and more straightforward to use.

For example, litsearchr is part of the metaverse, which is a set of R packages that span the entire scope of evidence synthesis in R, from generating search terms, assembling results, screening articles, visualizing risk of bias, doing a meta-analysis, and presenting results.

# Installing packages
In R, the fundamental unit of shareable code is the package. A package bundles together code, data, documentation, and tests, and is easy to share with others. As of January 2015, there were over 6,000 packages available on the Comprehensive R Archive Network, or CRAN, the public clearing house for R packages. This huge variety of packages is one of the reasons that R is so successful: the chances are that someone has already solved a problem that you’re working on, and you can benefit from their work by downloading their package.

There are thousands of additional R packages, in addition to the core R installation packages, which can be utilized. During this lesson we will be using several of these packages such as tidyverse and devtools.

# tidyverse, devtools, and litsearchr
The tidyverse includes several useful packages we’ll be using during this lesson, including dplyr, stringr, and purrr. Tidyverse is actually a package of packages, including many others that you are likely to use as you come to work with R.

> ## Exercise
Install the `tidyverse`, `devtools`, and `litsearchr` packages. 
>
> From the packages tab, click `Install` from the toolbar and type `tidyverse` into the textbox then click `install`
>
> The `tidyverse` package is really a package of packages, including `ggplot2` and `dplyr`, both of which require other packages to run correctly. All of these packages will be installed automatically. 
> 
> Depending on what packages have previously been installed in your R environment, the install of `tidyverse` could be very quick or could take several minutes.
>
As the install proceeds messages relating to the progress will be written to the console. You will be able to see all of the packages which are actually being installed.
>
Repeat the same steps for the `devtools` and `litsearchr` package.
> 
{: .checklist}

# Loading and using a package
After you install a package, you have to load it into your R session. You can do this using the library() function.

~~~
# If you try to run a function from a package without loading the library,
# you'll get an error message 'could not find function'
filter(x, z = TRUE)
## Error: could not find function 'filter'

# First, load the package using library
library("tidyverse")
~~~

To see what packages you have installed, and to read more about the functions in the package, click on the Packages tab in the Navigation Pane in RStudio, then click on the package. You can also use the help function to get help on a package. Some packages have what are called vignettes, which show examples of a package in use.

~~~
# get help with a package
help(package = "tidyverse")

# see vignettes available for a package. this pops a window up showing 5
# vignettes for tidyverse
vignette(package = "tidyverse")

# view a specific vignette
vignette("tidyverse")
~~~

## Installing additional packages using R code

If you were watching the console window when you started the install of ‘tidyverse’ you may have noticed that before the start of the installation messages, the line

~~~
install.packages("tidyverse")
~~~
{: .language-r}

was written to the console. 

You could also have installed the **`tidyverse`** packages by running this command directly at the R terminal. For install the **`devtools`** packages the command would look like this:

~~~
install.packages("devtools")
~~~
{: .language-r}
