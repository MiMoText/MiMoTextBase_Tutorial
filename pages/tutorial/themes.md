---
#title: Tutorial
tags: # add
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: themes.html
folder: tutorial
toc: false
topnav: topnav_tut
---

### **Themes**

A first module within our knowledge graph focused on the extraction of topics in the full texts and of literary themes in the bibliographic metadata, a controlled vocabulary of thematic concepts being the intermediate between these sources.

To get an overview of thematic concepts within the whole domain of French novels 1751-1800 within the knowledge graph, we can formulate a query for all themes and visualize the results in a bubble chart.

[All thematic concepts per novels, visualization in a bubble chart](https://tinyurl.com/232phv97){:target="\_blank", rel: "noopener noreferrer"}

<img src="images/graph.png" alt="drawing" height="600" width="800"/>

If a researcher is interested in compiling a corpus of novels on a certain [theme](https://github.com/MiMoText/vocabularies/blob/main/thematic_vocabulary.tsv), for example “travel”, “melancholy”, “philosophy” or “sentimentalism”, one can formulate this in a query and get all novels matching this criteria. We could also ask for all the authors which cover a certain theme, for example:

[Which authors write about “sentimentalism”?](https://tinyurl.com/29rkz3hx){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23%20authors%20with%20novels%20about%20sentimentalism%0A%23defaultView%3ABubbleChart%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3Fname%20%28count%28%2a%29%20as%20%3Fcount%29%20where%20%7B%0A%20%20%3Fitem%20wdt%3AP36%20%3Ftheme%20%3B%0A%20%20%20%20%20%20%20%20wdt%3AP5%20%3Fauthor%20.%0A%20%20%3Ftheme%20rdfs%3Alabel%20%3Fabout%20.%0A%20%20%3Fauthor%20rdfs%3Alabel%20%3Fname%20.%0A%0A%20%20%20%20%0A%20%20filter%28lang%28%3Fabout%29%20%3D%20%22en%22%29%0A%20%20filter%28lang%28%3Fname%29%20%3D%20%22en%22%29%0A%20%20%20filter%28contains%28lcase%28%3Fabout%29%2C%20%22sentimentalism%22%29%29%0A%7D%0A%0Agroup%20by%20%3Fname%0Aorder%20by%20desc%28%3Fcount%29%0A%20%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe></p>

As places of publication per novel are part of our properties, we could also combine the property of themes (`P36 about`) and `place of publication` (`P10` place of publication), resulting in the visual output of a map:

[Show all the places of publication of novels which are about “travel”](https://tinyurl.com/22xurtqc){:target="\_blank", rel: "noopener noreferrer"}
![IMG](images/themes_per_narrative_loc.png)

Combining themes and spaces in the graph, there is the property `P32` `narrative_location`, which can show interesting patterns of correlations of spaces with themes in the French novel of that period.

Let’s see how the rather abstract location “rural area” is intertwined with concise thematic concepts in aggregating all novels and all themes with narrative location “rural area” in the graph.

[Thematic concepts linked to the narrative location “rural area”](https://tinyurl.com/2ywgh5nx){:target="\_blank", rel: "noopener noreferrer"}

![rural](images/themes_rural.png)

As a result, we see that the thematic concepts “sentimentalism”, “sentiment” and “unhappiness” are linked to the narrative location “rural area” (in aggregating all novels).

[Previous](./spaces.html){: .btn-primary} [Next](./change_over_time.html){: .btn-primary}

{% include help.html %}
