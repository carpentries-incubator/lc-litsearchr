---
title: "Installing Packages"
teaching: 
exercises: 0
questions:
- "How to install packages?"
objectives:
- "Successfully install packages in RStudio"
keypoints:
- "Install tidyverse, a package of packages, including many that you are likely to use as you come to work with R"
- "Install devtools, a package needed to install litsearchr"
- "Install litsearchr, part of the metaverse, which is a set of R packages that span the entire scope of evidence synthesis in R"
---
# Installing packages
There are thousands of additional R packages, in addition to the core R installation packages, which can be utilized. During this lesson we will be using several of these packages such as tidyverse and devtools.

> ## Exercise
Install the `tidyverse` and the `devtools` packages. 
>
> From the packages tab, click `Install` from the toolbar and type `tidyverse` into the textbox then click `install`
>
> The `tidyverse` package is really a package of packages, including `ggplot2` and `dplyr`, both of which require other packages to run correctly. All of these packages will be installed automatically. 
> 
> Depending on what packages have previously been installed in your R environment, the install of `tidyverse` could be very quick or could take several minutes.
>
As the install proceeds messages relating to the progress will be written to the console. You will be able to see all of the packages which are actually being installed.
>
Repeat the same steps for the `devtools` package.
> 
{: .checklist}

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

