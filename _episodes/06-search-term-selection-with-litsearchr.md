---
title: "Search term selection with litsearchr"
teaching: 40
exercises: 50
questions:
- "What is the purpose of a naive search?"
- "How does litsearchr identify potential keywords?"
- "How does litsearchr select important keywords?"
objectives:
- "Explain the characteristics of a good naive search and practice identifying components."
- "Work through the process of importing and deduplicating bibliographic data."
- "Explain how to extract potential terms using different methods."
- "Explain the method litsearchr uses to identify important terms and work through this process."
keypoints:
- litsearchr helps identify important search terms related to the topic of a systematic review.
---

## What is a naive search and how is it used?

To identify potential search terms, litsearchr extracts keywords from the results of a naive search. The goal of a naive search is to return a set of highly relevant articles to a topic, even if they may not meet all the criteria, because they will contain the best terms. A naive search should have high precision, as opposed to high recall, because if too many irrelevant articles are retrieved litsearchr will select vague keywords. 

The reason for this is that litsearchr selects keywords based on how often they co-occur in the same article as other keywords; terms that co-occur frequently with other terms are classified as more important to the research topic since they are well-connected. If there are too many irrelevant articles in the naive search results, the terms that co-occur frequently across all the articles will be generic terms like "linear models" or "positive effect", which clearly are not good keywords.

Coming up with a naive search is very similar to developing a search strategy with conventional methods, except without reading papers to identify terms. Once the components of PICO (or one of its variants, like TOPICS+M) have been identified, come up with a set of the most precise terms you can think of that fit in the concept categories. 

For example, if the population of interest is college students, you might come up with the terms "college student", "undergraduates", "post-secondary student", "university student", etc. You would not want to incude just "student" on its own since that could encompass earlier education stages or non-traditional education, and could result in many mis-hits for "Student's t-test" which are not at all relevant.

## Exercise: Develop a naive search

Working either alone or in small groups of 2-3, take 10 minutes to develop a naive search for this paper: "Impact of alcohol advertising and media exposure on adolescent alcohol use: a systematic review of longitudinal studies". We will be using this systematic review by Anderson et al. (2009) throughout the lesson because it is open access and is of general public interest, but you can easily adapt the steps and code for your own research later.

Start by identifying the PICO (or one of its variants, such as PICOTS or PECO) components of the question and then generate all of the most precise synonyms. For example, you might opt for PECO and will identify the population as adolescents, exposure as alcohol advertising, and the outcome as alcohol use, but not include a comparator in the search terms.


## Importing and deduplicating naive search results

Normally once you have developed a naive search string, you would run the search in 2-3 databases appropriate for the topic and download the results in .ris or .bib format. You should make a note of which databases you searched, how many hits you got in each database, and any constraints you placed on the search for reproducibility. 

The bibliographic data used in this lesson came from a search in MEDLINE (1990-2008) on Web of Science and PsycINFO (1990-2008) on EBSCO. We searched the title, abstract, keywords, and MESH fields using the naive search string below. We retrieved 603 results in MEDLINE and 71 in PsycINFO.

((teens OR teen OR teenager OR adolescent OR youth OR "high school") AND (advertis* OR marketing OR television OR magazine OR "TV") AND (alcohol OR liquor OR drinking OR wine OR beer))

Before we can work with bibliographic data in R, we first need to import it and remove duplicates so that some articles are not over-represented if they were indexed in multiple databases. To do this, litsearchr relies on its sister package synthesisr, which contains functions for manipulating bibliographic data and generic functions for working with text data. Import and deduplication can be done directly from litsearchr, or learners can try out the underlying functions directly in synthesisr for more flexibility. 

```{r}
library(litsearchr)

# to import all of our search results at once, we can use the function import_results()
# most functions in litsearchr have sensible names (but not all!)

naive_import <- litsearchr::import_results("./data/anderson_naive/")

# did all our search results get imported?
# there should be 674 rows in the data frame (603 MEDLINE + 71 PsycINFO)

```

Some articles may be indexed in multiple databases. We need to remove duplicate articles because otherwise the terms found in those articles will be overrepresented in the dataset. There are a lot of options for how to detect and remove duplicates. For example, you could remove articles that have the exact same title, or that have the same DOI, or that have abstracts which are highly similar to each other and may just differ by extra information that a database appends to the abstract field (e.g. starting with ABSTRACT: ). There are even more options for customizing deduplication if using the synthesisr package directly, but we will stick with a fairly simple deduplication because if a few duplicate articles are missed, it will not affect the keyword extraction too much.

Here, we will remove any titles that are identical. litsearchr will automatically ignore case and punctuation, so "TITLE:"", "title--"", and "Title"" are considered duplicates.

```{r}

naive_results <-
  litsearchr::remove_duplicates(naive_import, field = "title", method = "exact")

# this removed 39 results, which means there were 32 unique hits in PsycINFO

```
## Extracting potential keywords from naive search results

Now that we have our deduplicated results, we can extract a list of potential keywords from them. This is not the list of keywords you will want to consider including in your search (we will get to that in a bit), and is simply all of the terms that the keyword extraction algorithm identifies as being a possible keyword. 

To use the extract_terms function, we first have to give it the text from which to extract terms. Using the titles, abstracts, and author- or database-tagged keywords makes the most sense, so we will paste those together as the text argument. 

The method we will use for this is called "fakerake" since it is an adaptation of the Rapid Automatic Keyword Extraction algorithm. You can also use the "RAKE" method when using litsearchr on your own if you want; it is faster, but it requires rJava which can be difficult to install depending on your operating system.

You will want to tweak the next three options depending on how many articles are returned by your naive search and how specific you want the search term suggestions to be. If you have a lot of naive search results, you may want to increase min_freq to higher numbers; here, we are only requiring a term to appear twice anywhere in the text in order to be identified as a keyword. This removes many spurious keywords and unhelpful terms like specific locations where a study took place. The next two arguments, ngrams and min_n, refer to whether or not litsearchr should only retrieve phrases of a certain length. There are very few situations where you will not want ngrams to equal TRUE; this is the tested method for litsearchr and what it is designed to do. Similarly, we recommend min_n = 2 because then all phrases with at least two words are suggested as keywords. 

Lastly, the language argument is used to determine what stopwords (terms like "the", "should", "are", etc.) will not be allowed as keywords. 

```{r}

raked_keywords <-
  litsearchr::extract_terms(
    text = paste(naive_results$title, naive_results$abstract, naive_results$keywords),
    method = "fakerake",
    min_freq = 2,
    ngrams = TRUE,
    min_n = 2,
    language = "English"
  )

# we can view some of the keywords with the function head()
head(raked_keywords, 20)

# some of these are clearly not relevant (e.g. "additional research")
# but those will be removed in subsequent filtering steps

# if we want to inspect keywords that contain some terms, we can use grep 
# this is not necessary, but can be reassuring that good keywords are retrieved!

alcohol <- raked_keywords[grep("alcohol", raked_keywords)]
head(alcohol, 20)

# we can also remove some terms that we suspect might be well connected
# but that we know are not important and could skew what we get in the end

irrelevant <- c("signific", "negative", "positive", "relationship", "analys",
                "regression", "model", "sample", "research", "survey", 
                "findings", "results", "study", "abstract")

remove <- unique(unlist(lapply(irrelevant, function(x){grep(x, raked_keywords)})))
raked_keywords[remove]

raked_keywords <- raked_keywords[-remove]

# we could also repeat this for other generic types of information
# for example, we could remove country names

countries <- countrycode::codelist_panel
countries <- unique(countries$country.name.en)

remove <- unique(unlist(lapply(tolower(countries), function(x){grep(x, raked_keywords)})))
raked_keywords[remove]

raked_keywords <- raked_keywords[-remove]


```

## Identifying important keywords

Because not all the keywords are relevant (and you probaby do not want to run a search with several thousand terms!), the next step is to determine which keywords are important to the topic of the systematic review and manually review those suggestions. 

To do this, litsearchr puts all of the terms into a keyword co-occurrence network. What this means is that if two terms both appear in the title/abstract/keywords of an article, they get marked as co-occurring. Terms that co-occur with other terms frequently are considered to be important to the topic because they are well-connected, especially if they are connected to other terms that are also well-connected. Building the keyword co-occurrence network lets litsearchr automatically identify which terms are probably important and suggest them as potential keywords. 

First, we will create a document-feature matrix. What litsearchr will do is take the list of potential keywords and determine which articles they appear in. Once we have this matrix, we can convert it to a network graph which makes it easy to to visualize relationships between terms and to assess their importance.

```{r}

naive_dfm <-
  litsearchr::create_dfm(
    elements = paste(naive_results$title, naive_results$abstract, naive_results$keywords),
    features = raked_keywords
  )

# we have the option here again to restrict how many studies a term must appear in to be included
# we have left it the same as when identifying possible terms (2)

naive_graph <-
  litsearchr::create_network(
    search_dfm = as.matrix(naive_dfm),
    min_studies = 2,
    min_occ = 2
  )

```

Now that we have our network, we need to figure out which terms are the most important. One of the interesting things about keyword co-occurrence networks (and networks in general) is that their importance metrics follow a power law, where there are many terms with low importance and a few terms that are very important. To see what this looks like, we can extract the strengths from the network using the igraph package, sort them, and plot the curve.

```{r}

strengths <- sort(igraph::strength(naive_graph), decreasing=TRUE)

# then we can see the most important terms
head(strengths, 10)

# most of them look pretty relevant to the topic, which is good


# to see what we mean by the strengths following a power law, let's plot them
plot(strengths, type="l", las=1)

# to see the least important terms, we can look at the terms in the tail of the distribution
tail(strengths, 10)

```

We can use this power law relationship as a way to identify important terms. We want all the terms above some cutoff in importance, and do not want to consider the terms in the tail of the distribution. For this exercise, we are going to use the minimum number of terms that gives us 50% of the total importance values in the network. This will give us a vector of important keywords to manually consider whether or not they should be included in the search terms. 

```{r}

cutoff <-
  litsearchr::find_cutoff(
    naive_graph,
    method = "cumulative",
    percent = .50,
    imp_method = "strength"
  )

reduced_graph <-
  litsearchr::reduce_graph(naive_graph, cutoff_strength = cutoff[1])

search_terms <- litsearchr::get_keywords(reduced_graph)

head(search_terms, 20)

```

