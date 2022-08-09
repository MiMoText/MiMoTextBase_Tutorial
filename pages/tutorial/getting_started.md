---
#title: Tutorial
#tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: getting_started.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **Searching**

All novels are stored as items in our graph, comparable to a Wikidata item in the Wikidata graph. You can have a look at an individual novel item by using [data.mimotext.uni-trier.de](http://data.mimotext.uni-trier.de/wiki/Main_Page){:target="_blank", rel: "noopener noreferrer"} and the search function. Type in the title of the novel you are looking for, hit enter and you see all properties stored on that novel (title, publication date, distribution format, number of pages, characters, style_attitude_tonality, plot_theme, author, narrative perspective, narrative location, place of publication):

![searching](images/searching.png)

### **How to run a query**

Follow the URL and let the query run by clicking on the "play"-Button. The results are visualized in a table as a default. Above the table, you can click on the arrow next to the eye. In the drop-down menu that pops up, you can choose different visualization options from the menu in order to display the results on a timeline, as a barchart, as a bubble chart and so on. Another way to display the results in a certain view is to specify it in the query itself. You can simply insert `#defaultView:Timeline` (for a timeline) or `#defaultView:BarChart` (for a barchart) or `#defaultView:Bubblechart` (for a bubble chart) in your SPARQL query.


<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#prefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fbgrf%20%3Fitem%20%3Fauthorlabel%20%3FitemLabel%20%3Fyear%20%20%3Fnarrpers%20%20%3Ftonality%20%3Fpages%20%7B%0A%20%3Fitem%20wdt%3AP5%20%3Fauthor%3B%20%23%20who%20is%20the%20autorh%3F%0A%20%20%20%20%20%20%20wdt%3AP4%20%3Ftitle%3B%20%23%20what%20is%20the%20title%3F%0A%20%20%20%20%20%20%20wdt%3AP22%20%3Fbgrf%3B%20%20%23%20what%20is%20the%20identifier%20in%20the%20bibliographic%20metadata%3F%0A%20%20%20%20%20%20%20wdt%3AP9%20%3Fdate%3B%20%23%20what%20is%20the%20publication%20date%3F%0A%20%20%20OPTIONAL%20%7B%0A%20%20%20%3Fitem%20wdt%3AP27%20%3Fnarrpers%20.%0A%20%20%20%3Fitem%20wdt%3AP31%20%3Ftonality.%20%0A%20%20%20%20%3Fitem%20wdt%3AP25%20%3Fpages.%0A%20%7D%0A%20%20BIND%28YEAR%28%3Fdate%29%20as%20%3Fyear%29.%20%0A%20%3Fauthor%20rdfs%3Alabel%20%3Fauthorlabel.%0A%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%20bind%28if%28bound%28%3Fnarrpers%29%2C%20%3Fnarrpers%2C%20%22unbekannt%22%29%20as%20%3Fnormalized%29%0A%7D%0A%0AORDER%20BY%20%3Fyea" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
                </p>

```
SPARQL
:  SPARQL stands for SPARQL Protocol and RDF Query Language.
```

<!-- [Previous](./tutorial_index.html){: .btn-primary}--> [Next](./select.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
