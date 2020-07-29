---
title: "Write a Boolean search string with litsearchr"
teaching: 15
exercises: 5
questions:
- "How does litsearchr write a Boolean search from the list of terms?"
- "What are the different options for writing search strings?"
objectives:
- "Explain the different options for writing Boolean search strings with litsearchr."
keypoints:
- "Given a list of terms grouped by concept, litsearchr can write full Boolean search string from them."
---

## Options for writing a Boolean search with litsearchr

Now that all terms are selected and grouped, litsearchr can take a list of terms and turn them into a full Boolean search. Because each bibliographic database has slightly different assumptions about how search strings should be formatted, litsearchr has options for formatting, lemmatization/stemming, etc. We will review how to use all the different options and what they mean in terms of the logic of the final search in human terms. We encourage you to play with different combinations to get a sense of how the options interact with each other.

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

> ## Exercise: Understanding closure rules
> To understand the closure rules, play around with some mock search terms by changing the closure, stemming, and exactphrase options and seeing how the outcput changes.
> `terms <- c("advertise", "advertising", "alcohol advertising", "advertisement")`
> `write_search(list(terms), closure="left", languages="English", stemming=TRUE, exactphrase=TRUE)`
{: .challenge}


## Writing a Boolean search

To actually write a Boolean search for our example systematic review, we should give litsearchr our full term list. We can then either copy the output to a database search, or change `writesearch` to `TRUE` and litsearchr will write the search to a plain text file.

~~~
full_search <- write_search(list(population, exposure, outcome),
                            closure = "none",
                            languages = "English",
                            stemming = TRUE,
                            exactphrase = TRUE,
                            writesearch = FALSE
                            )
print(full_search)
~~~
{: .language-r}

> ## Check-in with helpers
> For virtual lessons: head to breakout rooms to check in with helpers.
{: .discussion}
