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
- "Discuss the limits and pitfalls of litsearchr and other automated approaches to systematic reviews"
keypoints:
- litsearchr helps identify search terms and write Boolean searches for systematic reviews
---

## How does litsearchr fit into the evidence synthesis workflow?

- mirror lesson 04 overview? metaverse context
- provide context for litsearchr in the synthesis workflow
- explain import and dedupe functions provided by synthesisr

## What is litsearchr and what does it do?

If you have ever had to iteratively test a search strategy for many hours, manually scanning articles for new keywords until you have identified all of the search terms needed to return a set of benchmark articles, you know how easy it can be to accidentally omit search terms. Even with iteratively testing a search strategy, keywords not included in the benchmark articles used to estimate the comprehensiveness of a search strategy can accidentally be omitted, which can limit the comprehensiveness of a systematic review. To quickly identify a suite of keywords that could be used as search terms for a systematic review and return potentially omitted terms, researchers and information specialists can supplement lists of terms identifed through conventional methods with terms identified by partially automated methods, which can reduce the time needed to deveop a search strategy while also increasing recall.

litsearchr is an R package that helps identify search terms to build more comprehensive search strategies and save time in selecting keywords. It does this by pulling out the most relevant keywords from articles on the research topic of interest and suggesting them as potential search terms. We will get more into the methods of how it does this and apply the methods in Part 6 -- Search term selection with litsearchr.

Once users have identified search terms, either conventionally and/or with the partially automated approach, litsearchr automaticaly writes Boolean search strings and can translate searches into up to 53 languages by calling the Google Translate API. When writing searches, litsearchr can also lemmatize/truncate terms and remove redundant terms (e.g. "fragmented agricultural landscape" and "fragmented agriculture" can both be reduced to "fragmented agric*"). 

Finally, litsearchr can help automate the process of testing search strategies, reducing the amount of time it takes to check if the target articles are returned when estimating comprehensiveness and making the process repeatable because everything is documented in code. 

## Advantages and pitfalls of semi-automated methods

Partially automated approaches to identifying search terms (and many other stages of the evidence synthesis workflow!) reduces the time needed to develop comprehensive search strategies and can reduce unintentional bias introduced when selecting terms, however, these approaches are not without downsides. Users are reminded to critically evaluate all decisions made during the process, consider how different options might change results, and not rely too much on the package to identify every search term. Just because litsearchr did not identify a search term as important does not mean that it should not still manually be added back into the search string! litsearchr can only identify terms from the set of articles it is given, which makes it extra important to choose the input carefully (more on this in Part 6 -- Search term selection with litsearchr).
