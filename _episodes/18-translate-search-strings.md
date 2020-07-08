---
title: "Translating searches with litsearchr"
teaching: 30
exercises: 30
questions:
- "How does litsearchr translate searches?"
objectives:
- "Identify non-English languages that you might consider searching for a review topic."
keypoints:
- "litsearchr can translate full Boolean search strings into up to 53 languages."
---

## Translating search strings

To help reduce language barriers when searching for evidence in systematic reviews, litsearchr can suggest which non-English languages a research team may want to consider searching in based on the topic of the review. It can also translate search strings by calling the Google Translate API. You will need to sign up for an API key to use that feature, but it is free unless you are running thousands of searches per month. If you choose to use litsearchr to translate search strings, it is as simple as changing the languages argument in write_search as is shown below. The code is commented out with # so it is not run because we need an API key for that.

~~~
# write_search(list(population, exposure, outcome), closure="none", 
#                          languages=c("English", "French", "Dutch"), stemming=TRUE, exactphrase=TRUE)
~~~
{: .language-r}

## Choosing which languages to search in

In this lesson, we will identify other languages we should consider searching in but will not use the translation feature because it requires an API. The way litsearchr suggests languages is by querying a snapshot of Ulrich's global serials directory containing academic journal articles in STEM fields (including social sciences); it currently cannot suggest languages for humanities because it needs more information about humanities journals to make good recommendations.

To get a list of suggested languages, a count of how many journals are published in that language related to the key topics, and whether or not litsearchr can translate them, we can use the function `get_languages`. Key topics should be fairly general, such as entire discipline names, rather than specific to the topic of the review.

~~~
get_languages(c("psychology", "sociology", "health", "advertising", "alcohol"))
~~~
{: .language-r}

> ## Challenge: Choosing languages for other topics
> What languages would you want to consider searching in for a review on the topic of forestry? What about a review on dentistry? How different are the suggested lists of languages?
{: .callout}

