---
#title: Tutorial
tags: [mimotext_data]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: authors.html
folder: tutorial
toc: false
---

### **Authors**

One major focus of the MiMoText graph are the authors who published novels in French during 1751-1800. Based on the Bibliographie du genre romanesque français (Martin, Mylne, and Frautschi 1977), we extracted the authors of French novels whose first publication date lies in between that period, which means we excluded translations (in French) and re-editions.

The following query shows which authors are represented in the MiMoText graph via the property item `occupation` (P11) namely `author` (Q11).

[Query to retrieve all authors in the graph](https://tinyurl.com/y569bduk)

Via changing the `SELECT` part to `SELECT (count(?authorName) as ?count)`` you can get the total count of the authors represented in the graph.

[Query to retrieve the count of authors](https://tinyurl.com/2zxhkpom)

Authors with the most publications of novels during 1751-1800:

[Query to retrieve authors with most novels published (top 20)](https://tinyurl.com/2llk5jau)

To get more information on the authors like dates of birth and deaths or people who influenced them, you can use [federated queries](./federated.html) to query Wikidata.

But first of all, it is important to get an idea of how many of the authors within MiMoTextBase do actually have a mapping with Wikidata.

[Query to retrieve the number of authors having a wikidata-match](https://tinyurl.com/2zscslwj)

To see in comparison of how many authors have a mapping with Wikidata vs. those who don’t, you can run the following query:

[Comparison of wikidata matches vs. no matches on authors](https://tinyurl.com/2qzou3h8)

### **A timeline**

As described in the section above, federated queries allow querying several knowledge graphs at once. We can explore federated queries by querying the MiMoText graph and the Wikidata knowledge graph, making use of the Wikidata property date of birth and of the property image which allows us to see the date of birth of the authors in a timeline.

[Query](https://tinyurl.com/28x5ajjy)

[Please note, that only the authors of the full text corpus are mapped to Wikidata yet.]
