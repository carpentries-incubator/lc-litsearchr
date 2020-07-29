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

> ## Check-in with helpers
> For virtual lessons: head to breakout rooms to check in with helpers.
{: .discussion}

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

> ## Check-in with helpers
> For virtual lessons: head to breakout rooms to check in with helpers.
{: .discussion}

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
{: .challenge}

## Reproducibility of search testing

One of the nice things about testing search strategies in R is that your tests are reproducible. You can re-run the code with the same files and will get the same results. You can also save your workspace so you know exactly what the output was the last time you ran the code. This is especially helpful for testing search strategies, since you may tweak which terms you include in the search and want a record of which articles were retrieved. 

To save the output of running your code, you can either write files like we have been doing (e.g. with `write.csv`) or you can save the R objects themselves. You can save everything in your Global Environment with `save.image` or you can save one or more individual objects with `save`. Here, we will save the full search we wrote, the results we got in MEDLINE, and the recall of our search string and name the file something sensible.

~~~
save(full_search, medline, recall, file="search_test_round1.rda")
~~~
{: .language-r}

If we then want to read those objects into R again, we can use `load` to read them into our workspace, or we could send the .rda file to a colleague who could also load the objects without having to run all the code or need the files you used to produce them.

> ## Check-in with helpers
> For virtual lessons: head to breakout rooms to check in with helpers.
{: .discussion}