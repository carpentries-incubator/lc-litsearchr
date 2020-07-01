---
title: "Developing a naive search and importing search results"
teaching: 40
exercises: 50
questions:
- "What is the purpose of a naive search?"
objectives:
- "Explain the characteristics of a good naive search and practice identifying components."
- "Work through the process of importing and deduplicating bibliographic data."
keypoints:
- A good naive search provides a good basis for identifying potential search terms on a topic.
- Search results should be deduplicated to avoid terms used in some papers being overrepresented.
---

## What is a naive search and how is it used?

To identify potential search terms, litsearchr extracts keywords from the results of a naive search. The goal of a naive search is to return a set of highly relevant articles to a topic, even if they may not meet all the criteria, because they will contain the best terms. A naive search should have high precision, as opposed to high recall, because if too many irrelevant articles are retrieved litsearchr will select vague keywords. 

The reason for this is that litsearchr selects keywords based on how often they co-occur in the same article as other keywords; terms that co-occur frequently with other terms are classified as more important to the research topic since they are well-connected. If there are too many irrelevant articles in the naive search results, the terms that co-occur frequently across all the articles will be generic terms like "linear models" or "positive effect", which clearly are not good keywords.

Coming up with a naive search is very similar to developing a search strategy with conventional methods, except without reading papers to identify terms. Once the components of PICO (or one of its variants, like TOPICS+M) have been identified, come up with a set of the most precise terms you can think of that fit in the concept categories. 

For example, if the population of interest is college students, you might come up with the terms "college student", "undergraduates", "post-secondary student", "university student", etc. You would not want to incude just "student" on its own since that could encompass earlier education stages or non-traditional education, and could result in many mis-hits for "Student's t-test" which are not at all relevant.


> ## Exercise: Develop a naive search
> Working either alone or in small groups of 2-3, take 10 minutes to develop a naive search for this paper: "Impact of alcohol advertising and media exposure on adolescent
> alcohol use: a systematic review of longitudinal studies". We will be using this systematic review by Anderson et al. (2009) throughout the lesson because it is open 
> access and is of general public interest, but you can easily adapt the steps and code for your own research later.
>
> Start by identifying the PICO (or one of its variants, such as PICOTS or PECO) components of the question and then generate all of the most precise synonyms. For 
> example, you might opt for PECO and will identify the population as adolescents, exposure as alcohol advertising, and the outcome as alcohol use, but not include a 
> comparator in the search terms.
{: .checklist}


## Data used in this lesson

Normally once you have developed a naive search string, you would run the search in 2-3 databases appropriate for the topic and download the results in .ris or .bib format. You should make a note of which databases you searched, how many hits you got in each database, and any constraints you placed on the search for reproducibility. 

The bibliographic data used in this lesson came from a search in MEDLINE (1990-2008) on Web of Science and PsycINFO (1990-2008) on EBSCO. We searched the title, abstract, keywords, and MESH fields using the naive search string below. We retrieved 603 results in MEDLINE and 71 in PsycINFO.

((teens OR teen OR teenager OR adolescent OR youth OR "high school") AND (advertis* OR marketing OR television OR magazine OR "TV") AND (alcohol OR liquor OR drinking OR wine OR beer))

## Importing search results

Before we can work with bibliographic data in R, we first need to import it. To do this, litsearchr relies on its sister package [synthesisr](https://cran.r-project.org/web/packages/synthesisr/index.html), which contains functions for manipulating bibliographic data and generic functions for working with text data. Import and deduplication can be done directly from litsearchr, or learners can try out the underlying functions directly in synthesisr for more flexibility. 

First, we need to load litsearchr to use the functions in it. We do this with the `library` function, which loads all the functions and data in the litsearchr package.

~~~
library(litsearchr)
~~~
{: .language-r}


Now that we have loaded the library, we can use all the functions in litsearchr. The first function we will use is `import_results`, which as you might guess, imports bibliographic search results. Most functions in litsearchr have sensible names (but not all of them!) and you can view the help files for them using `?`, such as `?import_results` to determine what information needs to be passed to the function for it to work properly.

~~~
?import_results
~~~
{: .language-r}

There is no output from running this code, however, the Help panel will open up with information about `import_results`, including which arguments it takes. We have results saved in a directory (i.e. a folder), so we want to use the directory option rather than the file option, which would be for a single bibliographic file. Because the default option for `verbose` is `TRUE`, we do not need to specify it in order to have the function print status updates. Status updates are useful for importing results when you have a lot of results and want to make sure the function is working, or for diagnosing errors if the function fails to import a file and you want to know which one. 

~~~
naive_import <- import_results(directory="./data/anderson_naive/")
## Reading file ./data/anderson_naive//MEDLINE_1-500.txt ... done
## Reading file ./data/anderson_naive//MEDLINE_501-603.txt ... done
## Reading file ./data/anderson_naive//PsycINFO.bib ... done
~~~
{: .language-r}

We can now check if all our search results were imported successfully. There were no errors in output, but we should also check that the correct number of results were imported. There should be 674 rows in the data frame because we had 603 search results in MEDLINE and 71 in PsycINFO. We can use `nrow` to print the number of rows in the data frame of imported search results to confirm this. 

~~~
nrow(naive_import)
## [1] 674
~~~
{: .language-r}

## Deduplicating search results

Some articles may be indexed in multiple databases. We need to remove duplicate articles because otherwise the terms found in those articles will be overrepresented in the dataset. 

There are a lot of options for how to detect and remove duplicates. For example, you could remove articles that have the exact same title, or that have the same DOI, or that have abstracts which are highly similar to each other and may just differ by extra information that a database appends to the abstract field (e.g. starting with ABSTRACT: ). There are even more options for customizing deduplication if using the synthesisr package directly, but we will stick with a fairly simple deduplication because if a few duplicate articles are missed, it will not affect the keyword extraction too much.

Here, we will remove any titles that are identical. litsearchr will automatically ignore case and punctuation, so "TITLE:"", "title--"", and "Title"" are considered duplicates. 

~~~
naive_results <- remove_duplicates(naive_import, field = "title", method = "exact")
~~~
{: .language-r}


> ## Exercise: Counting unique records
> Check how many unique records were retained with `nrow`. 
> Since there were only two databases, how many records can we conclude were unique to PsycINFO and not in the MEDLINE output?
{: .callout}