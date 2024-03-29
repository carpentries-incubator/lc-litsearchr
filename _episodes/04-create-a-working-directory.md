---
title: "Create a Working Directory"
teaching: 20
exercises: 20
questions:
- "How to create a working directory?"
objectives:
- "Successfully set up a working directory in RStudio"
keypoints:
- "The working directory is very important, as it is the place where you will store, save, and retrieve your files."
- "Using consistent filing naming and folder structure across your projects will help keep things organized."
- "Download the file for this lesson if you haven't done so already."
---

## Getting set up
You will need to create and set up your working directory in RStudio for this lesson. The working directory is very important, as it is the place where you will store, save, and retrieve your files. RStudio projects makes it easy to set up your working directory.

For this lesson we'll create a new project.

* Under the `File` menu, click on `New project`, choose `New directory`, then `New project`

* Enter a name for this new project `library-carpentry`, and choose your desktop as the location. 

* Click on `Create project`

If for some reason your working directory is not set up correctly you can change it in the RStudio interface by navigating in the file browser where your working directory should be, and clicking on the blue gear icon "More", and select "Set As Working Directory". 

If you haven't already, [download the workshop files](https://github.com/carpentries-incubator/lc-litsearchr/raw/gh-pages/data/lc_litsearchr.zip), unzip or decompress the folder and place it into your new library-carpentry project directory by dragging and dropping file. 

> ## Make sure the files you downloaded from the zip folder are organized correctly before continuing on. 
>
> If you need to reorganize your files the instructions are below:
>
> Create three folders on your computer desktop and name them `data`, `anderson_naive`, and `search_results`
>  
> Add the following files you downloaded at the beginning of the lesson to the `data `folder. 
> * anderson_refs.csv
> * anderson_refs.rda
> * andersosn_studies.rda
> * suggested_keywords_grouped
>
> Add the three downloaded files from the anderson_naive zip folder to the `anderson_naive` folder.
> * MEDLINE_1-500
> * MEDLINE_501-603
> * PsycINFO
>
> Add the three downloaded savedrecs files to the `search_results` folder. 
> * savedrecs(1)
> * savedrecs(2)
> * savedrecs(3)
>
> Add your three new folders, `data`, `anderson_naive`, and `search_results` to the `library-carpentry` folder you just created.
>
>

{: .callout}

## Set your working directory
The **working directory** is the location on your computer R will use for reading and writing files. Use `getwd()` to print your current working directory to the console. Use `setwd()` to set your working directory. 

~~~
# Determine which directory your R session is using as its current working directory using getwd().
getwd()
~~~
{: .language-r}

To set your new working directory go to:
1. Under `Session` at the top
2. Scroll down to `Set Working Directory`
3. Select `Choose Directory`
4. Choose the folder `lc_litsearchr` on your desktop


## Organize your working directory
Using consistent filing naming and folder structure across your projects will help keep things organized. It will also make it easy to find things in the future since systematic reviews typically take months to complete. This can be especially helpful when you are working on multiple reviews or checking in with a review team months after running the initial search. In general, you can create directories or folders for **scripts**, **data**, and **documents**. 

For this lesson, we will create the following in your working directory:

* `search_results_data/` Use this folder to store your raw data or the original files you export from a bibliographic database. For the sake of transparency and [provenance](https://en.wikipedia.org/wiki/Provenance), you should *always* keep a copy of your raw data accessible and do as much of your data cleanup and preprocessing programmatically (i.e., with scripts, rather than manually) as possible.

* `search_results_data_output/` When you need to modify your raw data for your analyses, it might be useful to store the modified versions of the datasets generated by your scripts in a different folder.

* `documents/` This would be a place to keep outlines, drafts, and other text.

* `scripts/` This would be the location to keep your R scripts for different analyses or plotting.

You may want additional directories or subdirectories depending on your project needs, but these should form the backbone of your working directory for this lesson.

We can create these folders using the RStudio interface by clicking on the "New Folder" button in the file pane (bottom right), or directly from R by typing in the console. 

~~~
# Use dir.create() to create directories in the current working directory called "search_results_data", "search_results_data_output", "documents", and "scripts".

dir.create("search_results_data")
dir.create("search_results_data_output")
dir.create("documents")
dir.create("scripts")
~~~
{: .language-r}


## Exploring your working directory

Create a new object by assigning 8 to x using x <- 8.

~~~
x <- 8
~~~
{: .language-r}

You can list all the objects in your local workspace using `ls()`. See if the object `x` is listed. 

~~~
ls()
~~~
{: .language-r}

Now, list all the files in your working directory using `list.files()` or `dir()`.

~~~
dir()
~~~
{: .language-r}

As we go through this lesson, you should be examining the help page for each new function. Check out the help page for list.files with the command `?list.files`.

~~~
?list.files
~~~
{: .language-r}

One of the most helpful parts of any R help file is the See Also section. Read that section for list.files. 

Using the `args()` function on a function name is also a handy way to see what arguments a function can take. Use the `args()` function to determine the arguments to list.files().

~~~
args(list.files)

function (path = ".", pattern = NULL, all.files = FALSE, 
    full.names = FALSE, recursive = FALSE, ignore.case = FALSE, 
    include.dirs = FALSE, no.. = FALSE) 
NULL
~~~
{: .language-r}

Create a file in your working directory called "mylesson.R" by using the `file.create()` function.

~~~
file.create("mylesson.R")
~~~
{: .language-r}

Typing in `list.files()` shows that the directory contains mylesson.R.

~~~
list.files()
~~~
{: .language-r}

You can check to see if "mylesson.R" exists in the working directory by using the `file.exists()` function.

~~~
file.exists("mylesson.R")
~~~
{: .language-r}

You can change the name of the file "mylesson.R" to "myscript.R" by using `file.rename()`.

~~~
file.rename("mylesson.R", "myscript.R")
~~~
{: .language-r}

You can make a copy of "myscript.R" called "myscript2.R" by using `file.copy()`.

~~~
file.copy("myscript.R", "myscript2.R")
~~~
{: .language-r}



