---
title: "Preparing a search strategy with litsearchr"
teaching: 
exercises:
questions:
objectives:
keypoints:
---

## Grouping keywords into concept categories

The output from the previous lesson is a potentially long list of suggested keywords, not all of which will be relevant. These terms need to be manually reviewed to remove irrelevant terms and to classify keywords into useful categories. Some keywords may fit into multiple components of PICO, in which case they can be grouped into both and the Boolean search litsearchr writes will account for this. Research teams should decide whether they want to decide on search terms in duplicate or singly; in this exercise groups may opt for either approach.

To group keywords into categories, we recommend exporting the suggested list of keywords to a .csv file, manually tagging each keyword for either one of your PICO categories or as irrelevant, then reading the data back in. In this exercise, we will export a .csv file, enter data outside of R, read that data from a .csv file, and merge groups together.

```{r}

write.csv(keywords, "./suggested_keywords.csv")

```

Learners should open their exported keywords file either in RStudio as a text file, or in their default spreadsheet program, whichever is most comfortable to work with. Learners should assign each term to one of their PICO categories or mark a term as irrelevant (e.g. by giving it the group "x"). Because all groups and terms will be different, this stage is not automatically done by litsearchr and requires some custom coding. Learners will eventually want to have a data frame resembling the example data below. 

```{r}

example_keywords <- c("black-backed woodpecker", 
                      "cavity nesting birds", 
                      "eastern bluebird",
                      "picoides arcticus",
                      "fire return interval",
                      "vegetation structure",
                      "burn severity",
                      "forest age",
                      "landscape characteristics",
                      "canopy cover",
                      "population dynamics",
                      "woodpecker abundance")

example_groups <- c("population",
                    "population",
                    "x",
                    "population",
                    "exposure",
                    "x",
                    "exposure",
                    "x",
                    "x",
                    "x",
                    "outcome",
                    "population, outcome")
                    
example_dat <- data.frame(group=example_groups, 
                          term=example_keywords)

# if working in a .csv file outside of R/RStudio, read in your sorted terms with read.csv()

```

Once terms have been manually grouped and read into a data frame in R, the terms associated with each concept group can be extracted to a character vector. For this, learners should use grep() to determine which terms match each group they coded, following the example code below. 

```{r}

# grep is a way to detect strings (i.e. words)
# we can use it to subset based on groups                           

population <- example_dat$term[grep("population", example_dat$group)]

exposure <- example_dat$term[grep("exposure", example_dat$group)]

outcome <- example_dat$term[grep("outcome", example_dat$group)]
```

Because litsearchr defaults to suggesting phrases with at least two words and may not pick up on highly specialized terms or jargon that appears infrequently in the literature, information specialists and researchers may want to add their own terms to the list of suggested keywords. This can easily be done with the append function. 

```{r}
# if you do not know if a term was already in the list, use unique() to keep only unique terms
population <- unique(append(population, c("woodpecker", "picoides borealis"))

outcome <- append(outcome, c("occupancy"))

```


## Writing a Boolean search with litsearchr

Now that all terms are selected and grouped, litsearchr can take a list of terms and turn them into a full Boolean search. Because each bibliographic database has slightly different assumptions about how search strings should be formatted, litsearchr has options for formatting, lemmatization/stemming, etc. We will review how to use all the different options and what they mean in terms of the logic of the final search in human terms. Learners are encouraged to play with different combinations to get a sense of how the options interact with each other.

### exactphrase
Should search terms be wrapped in quotes to retrieve the exact phrase? Although this is not universally the proper logic for bibliographic databases, it works on many common platforms, though note that if you are using Scopus or other platforms with irregular punctuation logic, you may need to replace "quotes" with {brackets} depending on the platform search guidance. 

### stemming
Should search terms be lemmatized (i.e. reduced to root word stems) and truncated with a wildcard marker? For example, "outdoor recreation" could be converted to "outdoor* recreat\*" to also capture terms like "outdoors recreation" or "outdoor recreational". There may be cases where researchers do not want this feature applied to subsets of words (e.g. "rat" and "rats" are not easily replaced by "rat\*"), so it can be disabled (though by default, litsearchr only allows stems of 4 letters or longer). If only some terms should be stemmed and others (e.g. ratio*) should not be, there is no easy solution in litsearchr. We recommend using the stemming option in these cases, then manually cleaning up the final search for cases where stemming is not appropriate.

### closure
By default, litsearchr removes redundant search terms to reduce the total length of a search string and to make it more efficient. For example, if search terms include "woodpecker", "woodpecker abundance", and "black-backed woodpecker", only the term "woodpecker" needs to be searched because it is contained within the other two terms, so they are redundant and can be eliminated from the search. There may be cases where information specialists and researchers do not want redundant terms removed (e.g. when including the singular and plural form of a term is important for database search rules). To accommodate these cases, users can specify how they want terms to be detected as redundant based on assumptions of closure.
* left -- If one term is the beginning of another term, the second term is redundant.
* right -- If one term is the end of another term, the second term is redundant.
* full -- Terms are only redundant if identical (after stemming, if this is an option).
* none -- If a term appears anywhere inside another term, the second term is redundant.

To understand the closure rules, play around with the mock search terms below. In all cases, we have left the other options the same. 

```{r}

terms <- c("cat", "cats", "cat abundance", "cation", "alleycat")

litsearchr::write_search(list(terms), closure="left", 
                          languages="English", stemming=TRUE, exactphrase=TRUE)

litsearchr::write_search(list(terms), closure="right",
                          languages="English", stemming=TRUE, exactphrase=TRUE)

litsearchr::write_search(list(terms), closure="full", 
                          languages="English", stemming=TRUE, exactphrase=TRUE)

litsearchr::write_search(list(terms), closure="none", 
                          languages="English", stemming=TRUE, exactphrase=TRUE)


```



- go over options, lemmatization, redundancies, etc. 
- closure for plurals and word forms

```{r}

```

## Translating search strings

- choosing languages with Ulrich
- Google Translate API [get an API for the course and delete afterwards?]

```{r}

```


