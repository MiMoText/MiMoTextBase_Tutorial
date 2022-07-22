---
#title: Tutorial
tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: getting_started.html
folder: tutorial
toc: false
---

### **Getting Started**

Searching
All novels are stored as items in our graph, comparable to a Wikidata item in the Wikidata graph. You can have a look at an individual novel item by using [data.mimotext.uni-trier.de](/www.data.mimotext.uni-trier.de) and the search function. Type in the title of the novel you are looking for, hit enter and you see all properties stored on that novel (title, publication date, distribution format, number of pages, characters, style_attitude_tonality, plot_theme, author, narrative perspective, narrative location, place of publication):

How to run a query
Follow the URL and let the query run by clicking on the "play"-Button. The results are visualized in a table as a default. Above the table, you can click on the arrow next to the eye. In the drop-down menu that pops up, you can choose different visualization options from the menu in order to display the results on a timeline, as a barchart, as a bubble chart and so on. Another way to display the results in a certain view is to specify it in the query itself. You can simply insert `#defaultView:Timeline` (for a timeline) or `#defaultView:BarChart` (for a barchart) or `#defaultView:Bubblechart` (for a bubble chart) in your SPARQL query.

<iframe class="" src="https://query.wikidata.org/#%23Locations%20of%20aviation%20accidents%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fcoords%0AWHERE%0A%7B%0A%20%20%20%3Fitem%20wdt%3AP31%20wd%3AQ744913.%20%20%20%20%20%20%23%20item%20is%20an%20instance%20of%20an%20aviation%20accident%0A%20%20%20%3Fitem%20wdt%3AP625%20%3Fcoords.%20%20%20%20%20%20%20%20%23%20item%27s%20coordinates%20are%20collected%20by%20the%20%3Fcoords%20variable%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" style="width:100%;max-width:100%;height:450px" frameborder="0"></iframe>

```
SPARQL
:  SPARQL stands for SPARQL Protocol and RDF Query Language.
```

[Previous](./select.html){: .btn-primary} [Next](./union.html){: .btn-primary}

<!-- {% include links.html %} -->
