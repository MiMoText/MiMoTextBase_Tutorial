---
#title: Tutorial
tags: # add
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: themes.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **Themes**

One of the modules within our knowledge graph is focused on the extraction of topics in the full texts and of literary themes in the bibliographic metadata, a controlled vocabulary of thematic concepts being the intermediary between these sources.

To get an overview of thematic concepts within the whole domain of French novels 1751-1800 in the knowledge graph, we can formulate a query for all themes and visualise the results in a bubble chart.

[All thematic concepts of the novels, visualised as a bubble chart](https://tinyurl.com/23pvdfnc){:target="\_blank", rel: "noopener noreferrer"}

<img src="images/graph_reup.png" style="height:80%; width:80%" />

<!---
![concepts_bubble](images/graph_reup.png)
-->

If a researcher is interested in compiling a corpus of novels on a certain [theme](https://github.com/MiMoText/vocabularies/blob/main/thematic_vocabulary.tsv){:target="\_blank", rel: "noopener noreferrer"}d, for example “travel”, “melancholy”, “philosophy” or “sentimentalism”, one can formulate this in a query and get all novels matching this criteria. We could also ask for all the authors which cover a certain theme, for example:

[Which authors write about “sentimentalism”?](https://tinyurl.com/22qu4m9t){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/22qu4m9t" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe></p>

As publication places per novel are part of our properties, we could also combine the property of themes (`P36` `about`) and (`P10` `place of publication`) in the visual output of a map:

[Show all the places of publication of novels which are about “travel”](https://tinyurl.com/24k939dw){:target="\_blank", rel: "noopener noreferrer"}
![IMG](images/themes_per_narrative_loc.png)

Combining themes and spaces in the graph, there is the property `P32` `narrative_location`, which can show interesting patterns of correlations of spaces with themes in the French novel of that period.

Let’s see how the rather abstract location “rural area” is intertwined with concise thematic concepts in aggregating all novels and all themes with narrative location “rural area” in the graph.

[Thematic concepts linked to the narrative location “rural area”](https://tinyurl.com/28pfmpah){:target="\_blank", rel: "noopener noreferrer"}

![rural](images/themes_rural.png)

As a result, we see that the thematic concepts “sentimentalism”, “sentiment” and “unhappiness” are linked to the narrative location “rural area” (in aggregating all novels).

[Previous](./spaces.html){: .btn-primary} [Next](./change_over_time.html){: .btn-primary}

{% include help.html %}
