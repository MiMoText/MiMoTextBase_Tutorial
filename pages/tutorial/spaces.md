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

[Query: What are the most common publication places of French novels 1751-1800?](https://tinyurl.com/2aotam7o){: target="_blank" rel="noopener"}
<p>
<iframe style="width:100%;max-width:100%;height:550px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23defaultView%3AMap%7B%22hide%22%3A%20%5B%22%3Fpub_loc%22%2C%20%22%3Ftopic%22%5D%7D%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0A%0ASelect%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3Fpub_loc%20%3Fpub_locLabel%20%3FwikidataEntityLink%20%3FcoordinateLocation%20%3Ftheme%20%3FthemeLabel%0A%7B%0A%23%20%20%3Fitem%20wdt%3AP36%20%3Ftheme.%0A%20%20%3Fitem%20wdt%3AP10%0A%20%20%20%20%20%20%20%20%3Fpub_loc.%0A%20%20%3Fpub_loc%20wdt%3AP13%20%3FWikiLink.%0A%20%20%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiLink%20%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20widt%3AP625%20%3FcoordinateLocation%0A%20%20%7D%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%0A%20%20%20%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%0A%20%20%7D%0A%7D%0A"  referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>

As the first publication date of all novels is fed into the graph, we can also analyze the publication places in a diachronic perspective.

[Query: How did publication places change over time?](https://tinyurl.com/2anmw82t?){: target="_blank" rel="noopener"}

<p>
<iframe style="width:100%;max-width:100%;height:550px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23defaultView%3ABarChart%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASelect%20%3Fyear%20%3Fplacelabel%28count%28%2a%29%20as%20%3Fcountyear%29%20%0A%20%20%20WHERE%7B%0A%20%20%20%3Fitem%20wdt%3AP10%20%3Fplace.%0A%20%20%20%3Fplace%20rdfs%3Alabel%20%3Fplacelabel%20.%0A%20%20%20%3Fitem%20wdt%3AP9%20%3Fdate%20.%0A%20%20%20FILTER%28lang%28%3Fplacelabel%29%20%3D%20%22fr%22%29%0A%20%20%20BIND%28str%28year%28%3Fdate%29%29%20as%20%3Fyear%29%0A%20%20%20SERVICE%20wikibase%3Alabel%20%7Bbd%3AserviceParam%20wikibase%3Alanguage%20%22%7BAUTO_LANGUAGE%7D%22%2C%22fr%22%20.%7D%0A%20%20%7D%0A%0AGROUP%20BY%20%3Fyear%20%3Fplacelabel%0Ahaving%20%28%3Fcountyear%20%3E%201%29%0A%23ORDER%20BY%20asc%28%3Fyear%29%20desc%28%3Fcountyear%29%0A"  referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>


What strikes here is the abrupt break in places of publication concerning the Netherlands (Amsterdam, The Hague) with the year 1789. Not only the Dutch production sites, but also Switzerland (Neuchâtel, Genève) as a place of publication of French novels breaks off with the year of the revolution. The graphic output of the query shows that there was a change in the production conditions of French novels.

[Previous](./novels.html){: .btn-primary} [Next](./themes.html){: .btn-primary}

{% include help.html %}
