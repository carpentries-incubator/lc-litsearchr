---
title: "Installing Packages"
teaching: 20
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

There are thousands of additional R packages, in addition to the core R installation packages, which can be utilized. During this lesson we will be using several of these packages such as litsearchr.

To install packages in R studio use the `install.packages()` fucntion.

~~~
install.packages("enter in package name here")
~~~
{: .language-r}

# devtools, remotes, and litsearchr
These useful packages are ones we’ll be using during this lesson. There are many others that you are likely to use as you come to work with R.

> ## Exercise
> Install the , `devtools`, `remotes`, and `litsearchr` packages. 
>
> In the script pane, type `install.packages("devtools")`
> ~~~
> install.packages("devtools")
> ~~~
> {: .language-r}
>
> As the install proceeds messages relating to the progress will be written to the console. You will be able to see all of the packages which are actually being installed.
>
> Depending on what packages have previously been installed in your R environment, the install of `devtools` could be very quick or could take several minutes.
> 
> Repeat the same steps for the `remotes` and `litsearchr` package.
>
> If `litsearchr` fails to load try the following:
>
> ~~~
> install_github("elizagrames/litsearchr", ref = "main", force=TRUE)
> ## select option 3 in the console when it asks for updates 
> ~~~
> {: .language-r}
>
> Alternatively, you could install packages from the toolbar. From the packages tab, click `Install` from the toolbar and type `tidyverse` into the textbox then click `install`
>
{: .checklist}

# Loading and using a package
After you install a package, you have to load it into your R session. You can do this using the `library()` function.

~~~
## If you try to run a function from a package without loading the library,
you'll get an error message 'could not find function'

## First, load the package using library
library("remotes")
~~~
{: .language-r}

Repeat the same steps for the `devtools` and `litsearchr` package.

To see what packages you have installed, and to read more about the functions in the package, click on the Packages tab in the Navigation Pane in RStudio, then click on the package. You can also use the help function to get help on a package. Some packages have what are called vignettes, which show examples of a package in use.

~~~
# get help with a package
help(package = "litsearchr")

# see vignettes available for a package. 
# vignettes for litsearchr
vignette(package = "litsearchr")
~~~
{: .language-r}


