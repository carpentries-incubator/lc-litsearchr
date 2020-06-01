---
title: "Introduction"
teaching: 15
exercises: 0
questions:
- "Why should I learn how to use R and litsearchr?"
objectives:
- "Explain the advantages of using R and litsearchr for systematic reviews."
keypoints:
- "R and litsearch can help automate repetive tasks of a systematic review and add to the reproducibility of the the search development process."
---

## Introduction

This Library Carpentry lesson introduces librarians and researchers to the R programming language, R Studio and the R package litsearchr. The lesson is intended for librarians and researchers involved in, supporting or intending to carry out systematic reviews, scoping reviews and other forms of evidence synthesis that require comprehensive Boolean search strategies. Learners need not have any coding experience or experience with R or R Studio. 

## Why R?

R is a powerful open source tool for statistical analysis, data cleaning and wrangling, data visualization and the automation of repetitive tasks. For librarians and researchers involved in supporting or conducting evidence synthesis, R and the R package litsearchr can be used to facilitate term harvesting and automate the construction of Boolean searches, a task that can otherwise be lengthy and tedious. 

Another advantage of using a programming tool like R is that it lends itself to reproducibility, such that lines of R code can be saved, shared and reused to repeat and reproduce one's work. Reproducibility and transparency of methods are key concepts underlying the strength of high quality systematic reviews and other types of evidence synthesis. 

In this lesson, learners will be introduced to R syntax (i.e., the set of rules dictating the correct structure and format of R code). And we will use R Studio, a popular platform used to develop and execute R code. 

## Why litsearchr?

To learn any new tool or skill, it is best to put that skill to use in a practical way. Thus, we've developed this lesson around the R package litsearchr for use in the context of developing comprehensive search strategies for evidence synthesis. Learners will use the bibliographic data from a citation file to identify additional keywords and build Boolean searches using R code.

## Setup instructions

**R** and **RStudio** are separate downloads and installations. R is the
underlying statistical computing environment, but using R alone is no
fun. RStudio is a graphical integrated development environment (IDE) that makes
using R much easier and more interactive. You need to install R before you
install RStudio. Once installed, because RStudio is an IDE, RStudio will run R in the background.  You do not need to run it separately. After installing both programs, you will need to install the
**`tidyverse`** package from within RStudio. Follow the instructions below for
your operating system, and then follow the instructions to install
**`tidyverse`**.

### Windows

#### If you already have R and RStudio installed

* Open RStudio, and click on "Help" > "Check for updates". If a new version is
	available, quit RStudio, and download the latest version for RStudio.
* To check which version of R you are using, start RStudio and the first thing
  that appears in the console indicates the version of R you are
  running. Alternatively, you can type `sessionInfo()`, which will also display
  which version of R you are running. Go on
  the [CRAN website](https://cran.r-project.org/bin/windows/base/) and check
  whether a more recent version is available. If so, please download and install
  it. You can [check here](https://cran.r-project.org/bin/windows/base/rw-FAQ.html#How-do-I-UNinstall-R_003f) for
  more information on how to remove old versions from your system if you wish to do so.

#### If you don't have R and RStudio installed

* Download R from
  the [CRAN website](http://cran.r-project.org/bin/windows/base/release.htm).
* Run the `.exe` file that was just downloaded
* Go to the [RStudio download page](https://www.rstudio.com/products/rstudio/download/#download)
* Under *Installers* select **RStudio x.yy.zzz - Windows
  Vista/7/8/10** (where x, y, and z represent version numbers)
* Double click the file to install it
* Once it's installed, open RStudio to make sure it works and you don't get any
  error messages.


### macOS

#### If you already have R and RStudio installed

* Open RStudio, and click on "Help" > "Check for updates". If a new version is
	available, quit RStudio, and download the latest version for RStudio.
* To check the version of R you are using, start RStudio and the first thing
  that appears on the terminal indicates the version of R you are running. Alternatively, you can type `sessionInfo()`, which will also display which version of R you are running. Go on
  the [CRAN website](https://cran.r-project.org/bin/macosx/) and check
  whether a more recent version is available. If so, please download and install
  it.

#### If you don't have R and RStudio installed

* Download R from
  the [CRAN website](http://cran.r-project.org/bin/macosx/).
* Select the `.pkg` file for the latest R version
* Double click on the downloaded file to install R
* It is also a good idea to install [XQuartz](https://www.xquartz.org/) (needed
  by some packages)
* Go to the [RStudio download page](https://www.rstudio.com/products/rstudio/download/#download)
* Under *Installers* select **RStudio x.yy.zzz - Mac OS X 10.6+ (64-bit)**
  (where x, y, and z represent version numbers)
* Double click the file to install RStudio
* Once it's installed, open RStudio to make sure it works and you don't get any
  error messages.


### Linux

* Follow the instructions for your distribution
  from [CRAN](https://cloud.r-project.org/bin/linux), they provide information
  to get the most recent version of R for common distributions. For most
  distributions, you could use your package manager (e.g., for Debian/Ubuntu run
  `sudo apt-get install r-base`, and for Fedora `sudo yum install R`), but we
  don't recommend this approach as the versions provided by this approach are
  usually out of date. In any case, make sure you have at least R 3.3.1.
* Go to the
  [RStudio download page](https://www.rstudio.com/products/rstudio/download/#download)
* Under *Installers* select the version that matches your distribution, and
  install it with your preferred method (e.g., with Debian/Ubuntu `sudo dpkg -i
  rstudio-x.yy.zzz-amd64.deb` at the terminal).
* Once it's installed, open RStudio to make sure it works and you don't get any
  error messages.


### For everyone

**After installing R and RStudio, you need to install the
