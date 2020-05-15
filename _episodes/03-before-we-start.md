---
title: "Before We Start"
teaching: 0
exercises: 0
questions:
- "How to navigate RStudio?"
- "How to run r code?"
- "How to install packages?"
- "How to load files in R?"
objectives:
- "Successfully import data into RStudio"
- "Successfully install packages in RStudio"
- "Successfully navigate and run r code"
keypoints:
- "Install tidyverse, a package of packages, including many that you are likely to use as you come to work with R"
- "Install devtools, a package needed to install litsearchr"
- "Install litsearchr, part of the metaverse, which is a set of R packages that span the entire scope of evidence synthesis in R"
-
---

# About R and RStudio

## What is R?
R is more of a programming language than a statistics program. You can use R to create, import, and scrape data from the web; clean and reshape it; visualize it; run statistical analysis and modeling operations on it; text and data mine it; and much more. 

R is also free and open source, distributed under the terms of the GNU General Public License. This means it is free to download and use the software for any purpose, modify it, and share it. As a result, R users have created thousands of packages and software to enhance user experience and functionality. 

When using R, you have a console window with a blinking cursor, and you type in a command according to the R syntax in order to make it do something. This can be intimidating for people who are used to Graphical User Interface (GUI) software such as Excel, where you use the mouse to point and click, and never or seldom have to type anything into the interface in order to get it to do something. While this can be seen as a drawback, it actually becomes a great advantage once you learn the R language, as you are not bound by the options presented to you in a GUI, but can craft flexible and creative commands.

## What is RStudio?
RStudio is a user interface for working with R. You can use R without RStudio, but it’s much more limiting. RStudio makes it easier to import datasets, create and write scripts, and has an autocomplete activated for functions and variables you’ve already assigned. RStudio makes using R much more effective, and is also free and open source.

## RStudio Console
After you install and open RStudio, you will see a window with four panes. You may need to open the top left "Source" pane by clicking on the maximize icon.

![](../fig/RStudio_capture.PNG)

## Console Pane (bottom left)
If you were just using the basic R interface, without RStudio, this is all you would see. You use this to type in a command and press enter to immediately evaluate it. It includes a > symbol and a blinking cursor prompting you to enter some code. Code that you type directly in the console will not be saved, though it is available in the History Pane. You can try it out by typing 2 + 2 into the console. 

## Script Pane (top left)
This is sort of like a text editor, or a place to write and save code. You then tell RStudio to run the line of code, or multiple lines of code, and you can see it appear in the console as it is running. Then save the script as a .R file for future use, or to share with others. To create a new .R script file, use File > New File > R Script, and to open a script, use File > Open, or Recent Files to see files you’ve worked with recently. Save the R script by going to File > Save.

## Environment & History Pane (top right)
This pane includes two different but important functions.

* Environment: This will display the objects that you’ve read into what is called the “global environment.” When you read a file into R, or manually create an R object, it enters into the computer’s working memory. When we manipulate or run operations on that data, it isn’t actually written to a file until we tell it to. It is kept here in the environment.

* The environment pane will also include any objects you have defined. For example, if you type y <- 5 into the console, you will now see y defined as a value in your environment.

* You can list all objects in the environment by typing ls() in the console and pressing Enter on your keyboard. You can clear all objects in the environment by clicking the broom icon to the right of the words “Import Dataset.”" Clear individual objects by using the rm function; for example: rm(y) will delete the y object from your environment.

~~~
## create object y
v <- 5

## list all objects in the enviroment
ls()

## remove object y
rm(y)
~~~
{: .language-r}

## Navigation pane (lower right)
This pane has multiple functions:

* Files: Navigate to files saved on your computer
* Plots: View plots (charts and graphs) you have created
* Packages: view add-on packages you have installed, or install new packages
* Help: Read help pages for R functions
* Viewer: View local web content

# Getting set up
You will need to create and set up your working directory in RStudio for this lesson. The working directory is very important, as it is the place where you will store, save, and retrieve your files. RStudio projects makes it easy to set up your working directory.

If for some reason your working directory is not set up correctly you can change it in the RStudio interface by navigating in the file browser where your working directory should be, and clicking on the blue gear icon "More", and select "Set As Working Directory". Alternatively you can use `setwd("/path/to/working/directory")` to reset your working directory.

# Create a new project
* Under the `File` menu, click on `New project`, choose `New directory`, then
  `New project`
* Enter a name for this new folder (or "directory"), for example `litsearchr-lesson`, and choose a convenient
  location for it. This will be your **working directory** for the rest of the
  day (e.g., `~/library-carpentry`)
* Click on `Create project`
* Create a new file where we will type our scripts. Go to File > New File > R
  script. Click the save icon on your toolbar and save your script as
  "`script.R`".

# Organize your working directory
Using consistent filing naming and folder structure across your projects will help keep things organized. It will also make it easy to find things in the future since systematic reviews typically take months to complete. This can be especially helpful when you are working on multiple reviews or checking in with a review team months after running the initial search. In general, you may create directories or folders for **scripts**, **data**, and **documents**. Create the following folders in your working directory:

 - **`search_results_data/`** Use this folder to store your raw data or the original files you export from a bibliographic database. For the sake of
   transparency and [provenance](https://en.wikipedia.org/wiki/Provenance), you
   should *always* keep a copy of your raw data accessible and do as much of
   your data cleanup and preprocessing programmatically (i.e., with scripts,
   rather than manually) as possible.
 - **`search_results_data_output/`** When you need to modify your raw data for your analyses,
   it might be useful to store the modified versions of the datasets generated
   by your scripts in a different folder.
 - **`documents/`** This would be a place to keep outlines, drafts, and other
   text.
 - **`scripts/`** This would be the location to keep your R scripts for
   different analyses or plotting.

You may want additional directories or subdirectories depending on your project
needs, but these should form the backbone of your working directory for this lesson.

We can create these folders using the RStudio interface by clicking on the "New Folder" button in the file pane (bottom right), or directly from R by typing in the console:

~~~
dir.create("search_results_data")
dir.create("search_results_data_output")
dir.create("documents")
dir.create("scripts")
~~~
{: .language-r}

# Download the data for this lesson
For this lesson we will be using a ...

Go to the Figshare page for this curriculum (https://doi.org/10.6084/m9.figshare.12098595.v1), and download the dataset called "`anderson_refs`". 

Place this downloaded file in the `search_results_data` folder you just created in your working directory. You can do this by opening your computer's downloads folder, locating the file you just downloaded ("`anderson_refs`"), and dragging and dropping it into your newly created R Project folder ("`search_results_data`"). 

# Installing packages
There are thousands of additional R packages, in addition to the core R installation packages, which can be utilized. During this lesson we will be using several of these packages such as tidyverse and devtools.

# Excercise
> Install the 'tidyverse' and the 'devtools' packages. 
>
> > ## Soltuion
> > From the packages tab, click ‘Install’ from the toolbar and type ‘tidyverse’ into the textbox then click ‘install’

> > The ‘tidyverse’ package is really a package of packages, including 'ggplot2' and 'dplyr', both of which require other packages to run correctly. All of these packages will be installed automatically. 

> > Depending on what packages have previously been installed in your R environment, the install of ‘tidyverse’ could be very quick or could take several minutes.

> > As the install proceeds messages relating to the progress will be written to the console. You will be able to see all of the packages which are actually being installed.

> > Repeat the same steps for the "devtools" package.
> {: .solution}

## Installing additional packages using R code

If you were watching the console window when you starting the
install of ‘tidyverse’ you may have noticed that before the start
of the installation messages, the line

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

# Excercise
> Create a new object...
