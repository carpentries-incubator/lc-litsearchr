---
title: "An overview of systematic reviews"
teaching: 15
exercises: 10
questions:

- "What is a systematic review?"
- "What are the steps in a systematic review?"
- "How does an information expert help?"
- "How can a systematic review be automated?"

objectives:

- "Explain the differences between a systematic review and a narrative review"
- "Discuss the roles of an information specialist or librarian in a systematic review"
- "Describe the different steps of the systematic review process"
- "Identify different ways in which automation can facilitate the systematic review process"

keypoints:
- "Systematic reviews differ from traditional literature reviews in a number of significant ways"
- "Systematic review methods strive to reduce bias and increase reproducibility and transparency"
- "Automation and coding software like R can be used to facilitate parts of the systematic review process"
---

## Systematic reviews defined

Systematic reviews are comprehensive literature reviews conducted using established methods to find, appraise and synthesize existing research to answer a question. Systematic reviews are considered to be a reliable source of evidence to inform decision-making because they gather all of the available research evidence on a topic in an unbiased, transparent and reproducible way. 

Systematic reviews differ from traditional, 'narrative' literature reviews in the following ways:

| Systematic Reviews | Traditional Literature Reviews |
| ------------------ | ------------------------------ |
| The review question is focused, well-defined and specific | The review question is broad or open-ended with vaguely defined concepts |
| Searches for studies are exhaustive, cover many databases and include both peer-reviewed and gray literature sources | Searches in narrative reviews are often non-exhaustive and only include a few sources |
| Searches are reported and well-documented such that they can be reproduced at a later date by other researchers | The method to find studies is often vague if reported at all |
| Studies are selected based on pre-specified, well-defined criteria | Study selection usually involves  a 'cherry-picking' approach including studies already known to the author |
| Included studies are assessed for study quality and potential biases, and weighted accordingly in the analysis | Included studies are usually not assessed for quality or bias |
| Analysis may include meta-analytical quantitative methods | Analysis tends to be more qualitative in nature |


## The steps in a systematic review

A systematic review begins with a well-defined research question. The figure below indicates the step-by-step process used to search for studies, identify studies for inclusion, carry out analyses and report findings. 

![](../fig/SR-process.png)

## The role of an  information expert 

Given the need for comprehensive, reproducible searches and intensive information management, trained librarians and information professionals are a critical component to performing a high quality systematic review. 

Information specialists and librarians can assist in the following ways:

- Refining the research topic to an answerable research question appropriate for a systematic review.
- Developing search strategies, including identifying sources to search, harvesting search terms, and designing Boolean search across various databases.
- Gathering and deduplicating bibliographic records resulting from comprehensive database searches.

## Automating systematic reviews

Systematic reviews are intensive, time-consuming projects often involving multi-person teams over many months or even 1-2 years or more. Thus, much is underway to identify ways in which parts of the process can be sped up, facilitated or automated. 

The R package litsearchr provides a method to facilitate the harvesting of search terms to develop comprehensive search strategies, and to automatically create Boolean searches from lists of keywords, including incorporation of truncation and phrases.

> ## Think-Pair-Share: Reproducibility and search strategies
> Think about the process of developing a search strategy for a systematic review. What aspects of this process are reproducible? 
> What aspects are more difficult to reproduce? How do you think a tool like R and litsearchr can help to increase the reproducibility of this process? 
> Share your thoughts with your breakout room group, and then share with the rest of the group by adding a comment to the [Etherpad](https://pad.carpentries.org/litsearchr-alpha-202304).
{: .callout}

