---
title: "Testing search strategy performance with litsearchr"
teaching: 20
exercises: 20
questions:
- "How should benchmark articles be chosen and used?"
- "How do you add missing search terms to retrieve benchmark articles?"
objectives:
- "Explain how to check search string recall with litsearchr."
- "Practice identifying missing search terms with litsearchr."
keypoints:
- "litsearchr can help test the recall (sensitivity) of search strategies."
---

## Selecting benchmark articles

To estimate if a search string is comprehensive, we need a set of benchmark articles to test it against. Normally, these will come from previous reviews on similar topics or from a list suggested by subject experts. For this exercise, we will use the list of articles included in the original systematic review that we are using as an example. Although the original review included 16 articles, here, we only have 15 articles because one was in press at the time of the original article, so we know it will not be retrieved by our replicated searches as we set the years of articles to return to be from 1990-2008. 

Not all of our benchmark articles will be indexed in the databases we are testing our search strategy in. To test our string, we really want to know if our search string can retrieve an article only if it is included in the database. The easiest way to check this is to search for the titles of the articles we want to retrieve in the databases we are using. To check this, we can use `write_title_search`, which is really just a special case of writing a Boolean search that does not allow stemming and retains all terms in the title. 


~~~
load("./data/anderson_studies.rda")
benchmark <- anderson_studies$title

write_title_search(benchmark)

~~~
{: .language-r}

We can then copy the title search and see if the articles are indexed by searching the databases we are using. When you only have a handful of benchmark articles like in this case, it is fairly easy to manually check if they were retrieved. But what if you had a list of dozens, or even a hundred, benchmark articles and wanted to check whether they are retrieved across databases? That's where partially automated search testing can be especially useful. The other benefit of testing search strategies in R is that the results are then reproducible and you can easily document what modifications were needed to retrieve all the benchmark articles and how those decisions were made.


## Importing quasi-gold standard articles and search results

First, we need to read in the results of searching for titles in a database; this is our new gold standard. We also want to import the search results from the database(s) we are testing our search in. In this exercise, we will just test our search strategy in MEDLINE since all our benchmark articles are indexed in it.

~~~
# note that we use file as the argument here because we only have one file for the search result
gold_standard <- import_results(file="./data/search_testing/qgs.txt")

# but here, we use directory because we have saved several files to our search results folder
medline <- import_results(directory="./data/search_testing/search_results/")
~~~
{: .language-r}

## Estimating search strategy comprehensiveness

We can now check if our gold standard articles are retrieved by the search with the check_recall function. It compares the similarity of our gold standard titles to the ones our search found and reports this information back. Articles with a similarity of 1 were almost certainly retrieved (though be careful if you ever have a benchmark article with an extremely generic title!), and anything below that should be manually checked to see if they are the same title. 

~~~
recall <- check_recall(tolower(gold_standard$title), tolower(medline$title))
~~~
{: .language-r}

> ## Exercise: Checking articles with low similarity
> 
> For our benchmark articles, we should manually review whether or not they were indeed retrieved if they have low similarity scores. To find articles below a certain similarity level, we will need to convert it to a number.
> `recall[,'Similarity'] <- as.numeric(recall[,'Similarity'])`
>
> Now we can view articles with similarities below 1.
> `recall[which(recall[,'Similarity'] < 1),]`
>
> Were all the benchmark articles retrieved?
{: .callout}
