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
- "Use install.packages("tidyverse"), a package of packages, including many that you are likely to use as you come to work with R"
- "Use install.packages("devtools"), a package needed to install litsearchr"
- "Use devtools::install_github("elizagrames/litsearchr"), part of the metaverse, which is a set of R packages that span the entire scope of evidence synthesis in R"
---

## About R and RStudio

>## What is R?
>R is more of a programming language than a statistics program. You can use R to create, import, and scrape data from the web; clean and reshape it; visualize it; run statistical analysis and modeling operations on it; text and data mine it; and much more. 
>
>R is also free and open source, distributed under the terms of the GNU General Public License. This means it is free to download and use the software for any purpose, modify it, and share it. As a result, R users have created thousands of packages and software to enhance user experience and functionality. 
>
>When using R, you have a console window with a blinking cursor, and you type in a command according to the R syntax in order to make it do something. This can be intimidating for people who are used to Graphical User Interface (GUI) software such as Excel, where you use the mouse to point and click, and never or seldom have to type anything into the interface in order to get it to do something. While this can be seen as a drawback, it actually becomes a great advantage once you learn the R language, as you are not bound by the options presented to you in a GUI, but can craft flexible and creative commands.

>## What is RStudio?
>RStudio is a user interface for working with R. You can use R without RStudio, but it’s much more limiting. RStudio makes it easier to import datasets, create and write scripts, and has an autocomplete activated for functions and variables you’ve already assigned. RStudio makes using R much more effective, and is also free and open source.

>## RStudio Console
>After you install and open RStudio, you will see a window with four panes. You may need to open the top left "Source" pane by clicking on the maximize icon.

![](../fig/R_console_image.png)

>Console Pane (bottom left)
>If you were just using the basic R interface, without RStudio, this is all you would see. You use this to type in a command and press enter to immediately evaluate it. It includes a > symbol and a blinking cursor prompting you to enter some code. Code that you type directly in the console will not be saved, though it is available in the History Pane. You can try it out by typing 2 + 2 into the console. 

>Script Pane (top left)
>This is sort of like a text editor, or a place to draft and save code. You then tell RStudio to run the line of code, or multiple lines of code, and you can see it appear in the console as it is running. Then save the script as a .R file for future use, or to share with others. To create a new .R script file, use File > New File > R Script, and to open a script, use File > Open, or Recent Files to see files you’ve worked with recently. Save the R script by going to File > Save.

>Environment & History Pane (top right)
>This pane includes two different but important functions.

* Environment: This will display the objects that you’ve read into what is called the “global environment.” When you read a file into R, or manually create an R object, it enters into the computer’s working memory. When we manipulate or run operations on that data, it isn’t actually written to a file until we tell it to. It is kept here in the environment.

* The environment pane will also include any objects you have defined. For example, if you type y <- 5 into the console, you will now see y defined as a value in your environment.

* You can list all objects in the environment by typing ls() in the console and pressing Enter on your keyboard. You can clear all objects in the environment by clicking the broom icon to the right of the words “Import Dataset.”" Clear individual objects by using the rm function; for example: rm(y) will delete the y object from your environment.

~~~
## create object y
v <- 5

## list all objects in the enviroment
1s()

## remove object y
rm(y)
~~~
{: .language-r}

>Navigation pane (lower right)
>This pane has multiple functions:

* Files: Navigate to files saved on your computer
* Plots: View plots (charts and graphs) you have created
* Packages: view add-on packages you have installed, or install new packages
* Help: Read help pages for R functions
* Viewer: View local web content
{
