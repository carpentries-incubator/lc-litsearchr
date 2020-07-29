---
title: "Group search terms to concept categories"
teaching: 10
exercises: 15
questions:
- "Can you add in more search terms that were not identified by litsearchr?"
objectives:
- "Practice grouping search terms into concept categories and reading data."
- "Practice adding more keywords into the list of search terms."
keypoints:
- "litsearchr assumes keywords are grouped into distinct concept categories."
---

## Grouping keywords into concept categories

The output from the previous episode is a long list of suggested keywords, not all of which will be relevant. These terms need to be manually reviewed to remove irrelevant terms and to classify keywords into useful categories. Some keywords may fit into multiple components of PICO, in which case they can be grouped into both. Research teams should decide whether they want to decide on search terms in duplicate or singly. 

To group keywords into categories, we recommend exporting the suggested list of keywords to a .csv file, manually tagging each keyword for either one of your PICO categories or as irrelevant, then reading the data back in. In this section, we will export a .csv file, enter data outside of R, read that data from a .csv file, and merge groups together.

> ## Exercise: Grouping terms
> 
> First, use `write.csv` to save the search_terms to a file on your computer. 
> `write.csv(search_terms, file="./suggested_keywords.csv")`
> 
> Next, open the exported .csv file in whatever software you use to work with spreadsheets (e.g. LibreOffice or Microsoft Excel). Add a column to the spreadsheet called 'group' and rename the column of terms 'term'. 
>
> Take 3-5 minutes to go through as many terms in the list as you have time for and decide whether they match to the population (adolescents), exposure (alcohol advertising), outcome (alcohol use), or none of the groups. In the 'group' column of the spreadsheet, indicate the group(s) that a term belongs to; for example, "teen binge drinking" would be marked as "population, outcome" in the 'group' column because it matches two of the concept categories. For terms that are not relevant, you can mark the group as "x" or "not relevant" or another term that makes sense to you.
>
> You should not expect to finish reviewing terms in that amount of time, but can practice classifying them. We will use a pre-filled out .csv for subsequent practice. 
{: .challenge}

## Reading grouped terms into R

We need to read the spreadsheet of grouped terms back into R so that litsearchr can use the categories to write a Boolean search. To do this, we will use `read.csv` to import our spreadsheet and then use `head` to confirm that the data we read in is what we expected based on the exercise. It will not be identical to the results from the exercise because we are using a pre-filled out .csv so that everyone has the same set of terms and can follow along.

~~~
grouped_terms <- read.csv("./data/suggested_keywords_grouped.csv")

head(grouped_terms)
~~~
{: .language-r}

Once terms have been manually grouped and read into a data frame in R, the terms associated with each concept group can be extracted to a character vector. Because all groups and terms will be different depending on the topic of a review, this stage is not automatically done by litsearchr and requires some custom coding to pull out the different groups.

We can use `grep` to determine which terms belong to each group; `grep` is a way to detect strings (i.e. words). The output of `grep` is a vector of numbers that indicate which elements from grouped_terms$group contain the term 'population' which we can use to subset them out. We can combine this with square brackets `[]` to subset the 'term' column of grouped_terms and extract just the ones that contain the pattern 'population'.

~~~
grep(pattern="population", grouped_terms$group)

population <- grouped_terms$term[grep(pattern="population", grouped_terms$group)]
~~~
{: .language-r}

> ## Exercise: Subsetting terms
> Using what you just learned to subset the population terms, repeat this process for the outcome and exposure groups and save them to character vectors named `outcome` and `exposure`.
>
> `exposure <- grouped_terms$term[grep("exposure", grouped_terms$group)]`
> `outcome <- grouped_terms$term[grep("outcome", grouped_terms$group)]`
{: .challenge}

## Adding new terms to a search

Because litsearchr defaults to suggesting phrases with at least two words and may not pick up on highly specialized terms or jargon that appears infrequently in the literature, information specialists and researchers may want to add their own terms to the list of suggested keywords. This can easily be done with the append function. 

For example, we may want to add back the terms from our naive search:

((teens OR teen OR teenager OR adolescent OR youth OR "high school") AND (advertis* OR marketing OR television OR magazine OR "TV") AND (alcohol OR liquor OR drinking OR wine OR beer))

To do this, we can use `append` to add more terms to the end of our character vector. If you do not know if a term was already in the list, add it anyways and use `unique` to keep only unique terms.

~~~
population <- append(population, c("teenager", "teen", "teens", 
                                  "adolescent", "adolescents", 
                                  "youth", "high school"))

exposure <- append(exposure, c("marketing", "television", "TV", "magazine"))

outcome <- append(outcome, c("alcohol", "liquor", "drinking", "wine", "beer"))
~~~
{: .language-r}

> ## Check-in with helpers
> For virtual lessons: head to breakout rooms to check in with helpers.
{: .discussion}