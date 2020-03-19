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

Now that all terms are selected and grouped, litsearchr can take the lists of terms and turn them into a full Boolean search. Because each bibliographic database has slightly different assumptions about 

- go over options, lemmatization, redundancies, etc. 
- closure for plurals and word forms

```{r}

```

## Translating search strings

- choosing languages with Ulrich
- Google Translate API [get an API for the course and delete afterwards?]

```{r}

```


