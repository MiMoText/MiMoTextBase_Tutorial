---
#title: Tutorial
#tags: [mimotext_data]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: spaces.html
folder: tutorial
toc: false
topnav: topnav_tut
---

### **Spaces**

Space and time are fundamental categories in literary studies. With the possibility of algorithms to count places in texts, this opened up a broad field of analysis of relationships between geography and literature in the field of Digital Humanities (Moretti 1999; Piatti u. a. 2009). The second module in the “Mining and Modeling Text” project focused on spaces and places: We were interested in generating statements on narrative locations, as well as on publication places.

The mining of places in the bibliographic metadata comprehends publication places and narrative locations. The novels were mined by named entity recognition with SpaCy, a process of manual corrections following the extraction. All entities were mapped to the Wikidata Graph by using the tool OpenRefine. Both processes (unifying the vocabulary and reconciliation against Wikidata entities) enable us to compare, analyze places in the graph and to visualize the results on a map with the help of federated queries.

[Query: What are the most common publication places of French novels 1751-1800?](https://tinyurl.com/2aotam7o)

As the first publication date of all novels is fed into the graph, we can also analyze the publication places in a diachronic perspective.

[Query: How did publication places change over time?](https://tinyurl.com/2anmw82t?)

What strikes here is the abrupt break in places of publication concerning the Netherlands (Amsterdam, The Hague) with the year 1789. Not only the Dutch production sites, but also Switzerland (Neuchâtel, Genève) as a place of publication of French novels breaks off with the year of the revolution. The graphic output of the query shows that there was a change in the production conditions of French novels.

[Previous](./novels.html){: .btn-primary} [Next](./themes.html){: .btn-primary}

{% include help.html %}
