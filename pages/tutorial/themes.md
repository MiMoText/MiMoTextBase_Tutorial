---
#title: Tutorial
tags: # add
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: themes.html
folder: tutorial
toc: false
---

### **Themes**

A first module within our knowledge graph focused on the extraction of topics in the full texts and of literary themes in the bibliographic metadata, a controlled vocabulary of thematic concepts being the intermediate between these sources.

To get an overview of thematic concepts within the whole domain of French novels 1751-1800 within the knowledge graph, we can formulate a query for all themes and visualize the results in a bubble chart.

[All thematic concepts per novels, visualization in a bubble chart](https://tinyurl.com/232phv97)

<img src="images/graph.png" alt="drawing" height="600" width="800"/>

If a researcher is interested in compiling a corpus of novels on a certain [theme](https://github.com/MiMoText/vocabularies/blob/main/thematic_vocabulary.tsv), for example “travel”, “melancholy”, “philosophy” or “sentimentalism”, one can formulate this in a query and get all novels matching this criteria. We could also ask for all the authors which cover a certain theme, for example:

[Which authors write about “sentimentalism”?](https://tinyurl.com/29rkz3hx)

As places of publication per novel are part of our properties, we could also combine the property of themes (`P36 about`) and `place of publication` (`P10` place of publication), resulting in the visual output of a map:

[Show all the places of publication of novels which are about “travel”](https://tinyurl.com/2q24hdlb)
![IMG](images/themes_per_narrative_loc.png)

Combining themes and spaces in the graph, there is the property `P32` `narrative_location`, which can show interesting patterns of correlations of spaces with themes in the French novel of that period.

Let’s see how the rather abstract location “rural area” is intertwined with concise thematic concepts in aggregating all novels and all themes with narrative location “rural area” in the graph.

[Thematic concepts linked to the narrative location “rural area”](https://tinyurl.com/2ywgh5nx)

![rural](images/themes_rural.png)

As a result, we see that the thematic concepts “sentimentalism”, “sentiment” and “unhappiness” are linked to the narrative location “rural area” (in aggregating all novels).

[Previous](./spaces.html){: .btn-primary} [Next](./change_over_time.html){: .btn-primary}
