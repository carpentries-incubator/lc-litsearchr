---
title: "Testing search strategy performance with litsearchr"
teaching: 
exercises:
questions:
objectives:
keypoints:
---

## Selecting benchmark articles

To test if a 

For this exercise, we will use the list of articles included in the original systematic review that we are using as an example. Although the original review included 16 articles, here, we only have 15 articles because one was in press at the time of the original article, so we know it will not be retrieved by our replicated searches as we set the years of articles to return to be from 1990-2008. 

## Identifying quasi-gold standard articles

Not all of our benchmark articles will be indexed in the databases we are testing our search strategy in. To test our string, we really want to know if our search string can retrieve an article only if it is included in the database. The easiest way to check this is to search for the titles of the articles we want to retrieve in the databases we are using. To check this, we can use write_title_search(), which is really just a special case of writing a Boolean search that doesn't allow stemming and retains all terms in the title. 


```{r}

load("./data/anderson_studies.rda")
benchmark <- anderson_studies$title

benchmark <- gsub("\\?", " ", benchmark)

litsearchr::write_title_search(benchmark)

```

We can then take the title search and see if the articles are indexed. When you only have a handful of benchmark articles like in this case, it is fairly easy to manually check if they are retrieved. But what if you had a list of dozens, or even a hundred, benchmark articles and wanted to check whether they are retrieved across databases? That's where partially automated search testing can be especially useful. The other benefit of testing search strategies in R is that the results are then reproducible and you can easily document what modifications were needed to retrieve all the benchmark articles and how those decisions were made.

First, we need to read in the results of searching for titles in a database; this is our new gold standard. We also want to import the search results from the database(s) we are testing our search in. In this exercise, we will just test our search strategy in MEDLINE since all our benchmark articles are indexed in it.

```{r}

gold_standard <- litsearchr::import_results(file="./data/search_testing/qgs.txt")

medline <- litsearchr::import_results(directory="./data/search_testing/search_results/")

```

## Estimating search strategy comprehensiveness

We can now check if our gold standard articles are retrieved by the search with the check_recall function. It compares the similarity of our gold standard titles to the ones our search found and reports this information back. Articles with a similarity of 1 were almost certainly retrieved (though be careful if you ever have an article with an extremely generic title!), and anything below that should be manually checked to see if they are the same title. 

```{r}

recall <- litsearchr::check_recall(tolower(gold_standard$title), tolower(medline$title))

# to find articles below a certain similarity level, we will need to convert it to a number
recall[,'Similarity'] <- as.numeric(recall[,'Similarity'])

# then we can view articles with similarities below 1
recall[which(recall[,'Similarity'] < 1),]

# were all the articles retrieved?
# the first two in this list were and are only different because of punctuation
# but the last article is definitely not a match

```

For any gold standard articles that are not retrieved by our search, we want to find out which of our concept categories in the search string was not found and what terms we are missing. This functionality has not been implemented in litsearchr yet, but there are plans to add it in the next release of the package (FIXME -- will definitely be available by August). In the meantime, we can check manually since in this example we only missed one article.

```{r}

# find out which row of gold_standard we should investigate
grep("longitudinal study of parental movie", tolower(gold_standard$title))

missed_terms <- litsearchr::extract_terms(paste(gold_standard$title[7], gold_standard$abstract[7], gold_standard$keywords[7]), method="fakerake", min_freq=1, min_n=2)

missed_terms

# looks like we forgot to include movies as a type of media exposure

```
