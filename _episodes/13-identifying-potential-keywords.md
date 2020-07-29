---
title: "Identifying potential keywords with litsearchr"
teaching: 30
exercises: 15
questions:
- "How does litsearchr identify potential keywords?"
objectives:
- "Explain how to extract potential terms using different methods."
keypoints:
- litsearchr helps identify potential search terms related to the topic of a systematic review.
---

## Extracting potential keywords from naive search results

Now that we have our deduplicated results, we can extract a list of potential keywords from them. This is not the list of keywords you will want to consider including in your search (we will get to that in a bit), and is simply all of the terms that the keyword extraction algorithm identifies as being a possible keyword. 

We can identify potential keywords with the `extract_terms` function. To use `extract_terms`, we have to give it the text from which to extract terms. Using the titles, abstracts, and author- or database-tagged keywords makes the most sense, so we will paste those together. To subset these columns from our data frame, we can use `$` to extract named elements, which in our case are columns.

~~~
my_text <- paste(naive_results$title, 
                 naive_results$abstract, 
                 naive_results$keywords)
~~~
{: .language-r}



The method we will use to extract terms is called "fakerake" since it is an adaptation of the Rapid Automatic Keyword Extraction algorithm.

When working with your own data, you will want to tweak the options in `extract_terms` depending on how many articles are returned by your naive search and how specific you want the search term suggestions to be. If you have a lot of naive search results, you may want to increase `min_freq` to higher numbers; here, we are only requiring a term to appear twice anywhere in the text in order to be identified as a keyword. This removes many spurious keywords and unhelpful terms like specific locations where a study took place.

The next two arguments, `ngrams` and `min_n`, refer to whether or not litsearchr should only retrieve phrases of a certain length. There are very few situations where you will not want ngrams to equal TRUE; this is the tested method for litsearchr and what it is designed to do. Similarly, we recommend `min_n = 2` because then all phrases with at least two words are suggested as keywords. 

Lastly, the language argument is used to determine what stopwords (terms like "the", "should", "are", etc.) will not be allowed as keywords. 


~~~
raked_keywords <- extract_terms(
  text = my_text,
  method = "fakerake",
  min_freq = 2,
  ngrams = TRUE,
  min_n = 2,
  language = "English"
)
## Loading required namespace: stopwords
~~~
{: .language-r}

> ## Check-in with helpers
> For virtual lessons: head to breakout rooms to check in with helpers.
{: .discussion}

## Inspecting identified keywords

We can view some of the keywords using `head` and specifying how many terms we want to view. 

~~~
head(raked_keywords, 20)
##  [1] "abstract truncated"         "abuse education"            "abuse prevention"          
##  [4] "abuse prevention programs"  "abuse treatment"            "academic performance"      
##  [7] "active participation"       "active students"            "activities designed"       
## [10] "activity habits"            "activity level"             "activity levels"           
## [13] "activity patterns"          "actual alcohol"             "actual alcohol consumption"
## [16] "addictive behaviors"        "addictive substances"       "additional research"       
## [19] "adequately studied"         "administered questionnaire"
~~~
{: .language-r}

Some of these are clearly not relevant (e.g. "additional research"), but terms like this will be removed in subsequent filtering steps. If we want to inspect keywords that contain certain terms, we can use `grep` to subset these terms and view them. This can be useful if you want to reassure yourself that good keywords were retrieved in the naive search.

Here, we are checking to see if terms related to alcohol were retrieved and make sense for this topic.

~~~
alcohol <- raked_keywords[grep("alcohol", raked_keywords)]
head(alcohol, 20)
##  [1] "actual alcohol"                 "actual alcohol consumption"     "adolescent alcohol"            
##  [4] "adolescent alcohol consumption" "adolescent alcohol initiation"  "affect alcohol"                
##  [7] "aggregate alcohol"              "alcohol abuse"                  "alcohol abuse education"       
## [10] "alcohol abuse prevention"       "alcohol abusers"                "alcohol addiction"             
## [13] "alcohol advertisement"          "alcohol advertisement exposure" "alcohol advertisements"        
## [16] "alcohol advertisers"            "alcohol advertising"            "alcohol advertising effects"   
## [19] "alcohol advertising exposure"   "alcohol advertising targeted"  
~~~
{: .language-r}

> ## Exercise: Subsetting keywords
> Using what you have just learned, write R code that subsets out terms that contain "advertis", similar to searching 
> for advertis* to capture advertisement, advertising, advertiser, etc.
>
> 
> How many terms contain "advertis"? Hint: `length` will be useful.
{: .callout}
