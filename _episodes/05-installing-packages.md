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
Install the `tidyverse` and the `remotes` packages. 
>
> From the packages tab, click `Install` from the toolbar and type `tidyverse` into the textbox then click `install`
>
> The `tidyverse` package is really a package of packages, including `ggplot2` and `dplyr`, both of which require other packages to run correctly. All of these packages will be installed automatically. 
> 
> Depending on what packages have previously been installed in your R environment, the install of `tidyverse` could be very quick or could take several minutes.
>
As the install proceeds messages relating to the progress will be written to the console. You will be able to see all of the packages which are actually being installed.
>
Repeat the same steps for the `remotes` package.
> 
{: .checklist}

## Installing additional packages using R code

If you were watching the console window when you started the install of ‘tidyverse’ you may have noticed that before the start of the installation messages, the line

~~~
install.packages("tidyverse")
~~~
{: .language-r}

was written to the console. 

You could also have installed the **`tidyverse`** packages by running this command directly at the R terminal. For install the **`remotes`** packages the command would look like this:

~~~
install.packages("remotes")
~~~
{: .language-r}

