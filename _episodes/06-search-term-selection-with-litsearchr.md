---
title: "Search term selection with litsearchr"
teaching: 10
exercises: 50
questions:
objectives:
keypoints:
---


## What is a naive search and how is it used?

To identify potential search terms, litsearchr extracts keywords from the results of a naive search. The goal of a naive search is to return a set of highly relevant articles to a topic, even if they may not meet all the criteria, because they will contain the best terms. A naive search should have high precision, as opposed to high recall, because if too many irrelevant articles are retrieved litsearchr will select vague keywords. The reason for this is that litsearchr selects keywords based on how often they co-occur in the same article as other keywords; terms that co-occur frequently with other terms are classified as more important to the research topic since they are well-connected. If there are too many irrelevant articles in the naive search results, the terms that co-occur frequently across all the articles will be generic terms like "linear models" or "positive effect", which clearly are not good keywords.

Coming up with a naive search is very similar to developing a search strategy with conventional methods, except without reading papers to identify terms. Once the components of PICO (or one of its variants, like TOPICS+M) have been identified, users should come up with a set of the most precise terms they can think of that fit in the concept categories. For example, if the population of interest is college students, a user might come up with the terms "college student", "undergraduates", "post-secondary student", "university student", etc. but would not want to incude just "student" on its own since that could encompass earlier education stages or non-traditional education. 

## Exercise: Develop a naive search

Working either alone or in small groups of 2-3, learners should take 10 minutes to develop a naive search either for a project they are working on, or one of the options below that is most closely matched to their expertise. Start by identifying the PICO (or one of its variants, such as PICOTS or PECO) components of the question and then generate all of the most precise synonyms. For example, if working with the second option below, learners will likely opt for PECO and will identify the population as adolescents, exposure as alcohol advertising, and the outcome as alcohol use, but not include a comparator in the search terms.

The topics listed below come from published systematic reviews that we will use throughout the lesson to identify terms, and later, to check the performance of different search strings (Part 08 -- Test a search strategy with litsearchr). We encourage learners to stick with the same topic throughout the lesson because it will make the connections between parts more apparent, and, if learners choose one of the options below, they can contribute data to a project testing the sensitivity of litsearchr to different decisions made by different groups of learners (completely optional). These particular systematic reviews were chosen because they are open access, represent several disciplines, and the topics are of general public interest.

Are current management recommendations for saproxylic invertebrates effective? A systematic review

Impact of alcohol advertising and media exposure on adolescent alcohol use: a systematic review of longitudinal studies

Dietary sugars and body weight: systematic review and meta-analyses of randomised controlled trials and cohort studies

Evidence-based interventions for immigrant students experiencing behavioral and academic problems: a systematic review of the literature

NOTE: Eliza still has to pull together the descriptions for this and a plan for people to contribute data (presumably a website that explains it more). The idea is for lesson participants to anonymously upload their naive search, final keywords, and how well the final search string did at retrieving the benchmark articles at the end of the lesson. Eliza, and whoever else is interested, will eventually review/score all of the naive searches then test this score of quality/completeness in relation to recall of the original articles included in the published systematic review to see how sensitive litsearchr is to different initial inputs.

## Importing and deduplicating naive search results

Once learners have developed their naive search string, they should run the search in 2-3 databases appropriate for the topic and download the results in .ris or .bib format. If learners plan to contribute data to test the sensitivity of the package to different decisions, they should make a note of which databases they searched, how many hits they got in each database, and any constraints they made on the search. This is a good thing to do regardless of the project for reproducibility, so all learners are encouraged to keep notes on decisions made while identifying search terms. 

Before we can work with bibliographic data in R, we first need to import it and remove duplicates so that some articles are not over-represented if they were indexed in multiple databases. To do this, litsearchr relies on its sister package synthesisr, which contains functions for manipulating bibliographic data and doing some generic text mining. Import and deduplication can be done directly from litsearchr, or learners can try out the underlying functions directly in synthesisr for more flexibility. 

```{r}
library(litsearchr)

# most functions in litsearchr have sensible names (but not all!)
# the function import_results() will import a file or directory of results 
# and the function remove_duplicates() will deduplicate them

```

## Extracting keywords from naive search results

```{r}


```

## Identifying important keywords

```{r}

```
