---
layout: lesson
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
---
This Library Carpentry lesson introduces people working in library- and information-related roles to using R and Rstudio when working on systematic reviews. In addition to the basics of R and RStudio, you will learn to use the litsearchr R package. 

`litsearchr` facilitates the development of a systematic search strategy, partially automating keyword selection from a set of search results and writing Boolean searches, including automating truncation of terms. 

This is an introduction to R and RStudio designed for participants with no programming experience. At the conclusion of the lesson you will understand what R and RStudio does and how to use the litsearchr package to advance your work with systematic reviews.

<!-- this is an html comment -->

{% comment %} This is a comment in Liquid {% endcomment %}

> ## Getting Started
>
> Library Carpentry’s teaching is hands-on, so participants are encouraged to use their own computers to ensure the proper setup of tools for an efficient workflow. 
> Our lessons focus on building software and data skills within library and information-related communities. 
> To most effectively participate in the lesson, please make sure to download the data and necessary software beforehand.
> 
> 
> This workshop assumes no prior experience with the tools covered in the lesson.
>
> To get started, follow the directions in the [Setup](https://ameliakallaher.github.io/lc-litsearchr/setup.html) tab to
> get access to the required software and data for this workshop.
{: .prereq}

> ## Data
>
> To complete this lesson you will need to install [R](http://cran.r-project.org/bin/windows/base/release.htm) and [RStudio](https://www.rstudio.com/products/rstudio/download/#download) and download the following files from Figshare.
> * [anderson_refs.csv](https://doi.org/10.6084/m9.figshare.12417554.v1) 
> * [anderson_refs.rda](https://doi.org/10.6084/m9.figshare.12685472)
> * [anderson_studies.rda](https://doi.org/10.6084/m9.figshare.12685481)
> * [anderson_naive](https://doi.org/10.6084/m9.figshare.12685487) 
>
> For this lesson we'll be using a published systematic review [Impact of alcohol advertising and media exposure on adolescent alcohol use: a systematic review of longitudinal studies](https://pubmed.ncbi.nlm.nih.gov/19144976/) which assessed the impact of alcohol advertising and media exposure on future adolescent alcohol use.
>
> See [Setup](https://ameliakallaher.github.io/lc-litsearchr/setup.html) for information about how to install R and RStudio.
{: .prereq}

## Lesson Overview 

| Lesson    | Overview |
| ------- | ---------- |
| [Day One: Introduction to R and RStudio](https://ameliakallaher.github.io/lc-litsearchr/01-introduction/index.html) | Get an overview of systematic reviews, learn how to interact with R, install packages, and get data into RStudio. |
| [Day Two: Introduction to litsearchr](https://ameliakallaher.github.io/lc-litsearchr/11-introduction-to-litsearchr/index.html) | Explore, develop, and identify potential search terms before writing, translating, and testing search strategies with litsearchr. |


{% include links.md %}
