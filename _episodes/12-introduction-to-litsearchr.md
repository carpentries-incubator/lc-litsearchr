---
title: "Introduction to litsearchr"
teaching: 20
exercises: 0
questions:
- "What is litsearchr?"
- "What can it do?"
objectives:
- "Provide context for litsearchr within the synthesis workflow"
- "Explain what litsearchr can do"
- "Explain how the litsearchr can help with systematic reviews"
keypoints:
- litsearchr helps identify search terms and write Boolean searches for systematic reviews.
---

## What is litsearchr and what does it do?

litsearchr is one part of the [metaverse](https://rmetaverse.github.io/), a suite of integrated R packages that facilitate partial automation and reproducible evidence synthesis workflows in R.

### Identify keywords
If you have ever had to iteratively test a search strategy for many hours, manually scanning articles for new keywords until you have identified all of the search terms needed to return a set of benchmark articles, you know how easy it can be to accidentally omit search terms. Even with iteratively testing a search strategy, keywords not included in the benchmark articles used to estimate the comprehensiveness of a search strategy can accidentally be omitted, which can limit the comprehensiveness of a systematic review. To quickly identify a suite of keywords that could be used as search terms for a systematic review and return potentially omitted terms, researchers and information specialists can supplement lists of terms identifed through conventional methods with terms identified by partially automated methods, which can reduce the time needed to deveop a search strategy while also increasing recall.

litsearchr is an R package that helps identify search terms to build more comprehensive search strategies and save time in selecting keywords. It does this by pulling out the most relevant keywords from articles on the research topic of interest and suggesting them as potential search terms. We will get more into the methods of how it does this and apply the methods in [Search term selection with litsearchr]("../13-search-term-selection-with-litsearchr/index.html").

### Write and translate searches
Once users have identified search terms, either conventionally and/or with the partially automated approach, litsearchr automaticaly writes Boolean search strings and can translate searches into up to 53 languages by calling the Google Translate API. When writing searches, litsearchr can also lemmatize/truncate terms and remove redundant terms (e.g. "fragmented agricultural landscape" and "fragmented agriculture" can both be reduced to "fragmented agric*"). 

### Test search strategies
Finally, litsearchr can help automate the process of testing search strategies, reducing the amount of time it takes to check if the target articles are returned when estimating comprehensiveness and making the process repeatable because everything is documented in code. 
