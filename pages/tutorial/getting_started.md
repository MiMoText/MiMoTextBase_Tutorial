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

### **Searching**

All novels are stored as items in our graph, comparable to a Wikidata item in the Wikidata graph. You can have a look at an individual novel item by using [data.mimotext.uni-trier.de](http://data.mimotext.uni-trier.de/wiki/Main_Page) and the search function. Type in the title of the novel you are looking for, hit enter and you see all properties stored on that novel (title, publication date, distribution format, number of pages, characters, style_attitude_tonality, plot_theme, author, narrative perspective, narrative location, place of publication):

![searching](images/searching.png)

### **How to run a query**

Follow the URL and let the query run by clicking on the "play"-Button. The results are visualized in a table as a default. Above the table, you can click on the arrow next to the eye. In the drop-down menu that pops up, you can choose different visualization options from the menu in order to display the results on a timeline, as a barchart, as a bubble chart and so on. Another way to display the results in a certain view is to specify it in the query itself. You can simply insert `#defaultView:Timeline` (for a timeline) or `#defaultView:BarChart` (for a barchart) or `#defaultView:Bubblechart` (for a bubble chart) in your SPARQL query.

```
SPARQL
:  SPARQL stands for SPARQL Protocol and RDF Query Language.
```

<!-- [Previous](./tutorial_index.html){: .btn-primary}--> [Next](./select.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
