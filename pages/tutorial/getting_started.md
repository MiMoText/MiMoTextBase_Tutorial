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

All novels are stored as items in our graph, comparable to a Wikidata item in the Wikidata graph. You can have a look at an individual novel item by using [data.mimotext.uni-trier.de](http://data.mimotext.uni-trier.de/wiki/Main_Page){:target="\_blank", rel: "noopener noreferrer"} and the search function. Type in the title of the novel you are looking for, hit enter and you see all properties stored on that novel (title, publication date, distribution format, number of pages, characters, style_attitude_tonality, plot_theme, author, narrative perspective, narrative location, place of publication):

![searching](images/searching.png)

### **How to run a query**

Follow the URL and let the query run by clicking on the "play"-Button. The results are visualized in a table as a default. Above the table, you can click on the arrow next to the eye. In the drop-down menu that pops up, you can choose different visualization options from the menu in order to display the results on a timeline, as a barchart, as a bubble chart and so on. Another way to display the results in a certain view is to specify it in the query itself. You can simply insert `#defaultView:Timeline` (for a timeline) or `#defaultView:BarChart` (for a barchart) or `#defaultView:Bubblechart` (for a bubble chart) in your SPARQL query.

<!-- [Query to get an overview over the MiMoText data](https://tinyurl.com/25rt89cw){:target="\_blank", rel: "noopener noreferrer"} -->

[Query to get an overview over the MiMoText data](https://query.mimotext.uni-trier.de/#%23title%3ASome%20data%20about%20the%20MiMoTextBase%20such%20as%20Authors%2C%20Novels%2C%20publication%20years%2C%20tone%20etc.%0Aprefix%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fbgrf%20%3Fitem%20%3Fauthorlabel%20%3FitemLabel%20%3Fyear%20%3Fnarrpers%20%3Ftonality%20%3Fpages%20%3Fnormalized%20WHERE%20%7B%0A%20%3Fitem%20mmdt%3AP5%20%3Fauthor%3B%20%23%20who%20is%20the%20author%3F%0A%20%20%20%20%20%20%20mmdt%3AP4%20%3Ftitle%3B%20%23%20what%20is%20the%20title%3F%0A%20%20%20%20%20%20%20mmdt%3AP22%20%3Fbgrf%3B%20%20%23%20what%20is%20the%20identifier%20in%20the%20bibliographic%20metadata%3F%0A%20%20%20%20%20%20%20mmdt%3AP9%20%3Fdate%3B%20%23%20what%20is%20the%20publication%20date%3F%0A%20OPTIONAL%20%7B%0A%20%20%20%3Fitem%20mmdt%3AP27%20%3Fnarrpers%3B%20mmdt%3AP31%20%3Ftonality%3B%20mmdt%3AP25%20%3Fpages.%20%0A%20%7D%0A%20BIND%28YEAR%28%3Fdate%29%20as%20%3Fyear%29.%0A%20BIND%28if%28bound%28%3Fnarrpers%29%2C%20%3Fnarrpers%2C%20%22unbekannt%22%29%20as%20%3Fnormalized%29%0A%20%3Fauthor%20rdfs%3Alabel%20%3Fauthorlabel.%0A%20FILTER%28LANG%28%3Fauthorlabel%29%20%3D%20%22en%22%29%0A%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2C%20fr%22.%20%7D%0A%7D%20ORDER%20BY%20%3Fyear){:target="\_blank", rel: "noopener noreferrer"}

```sparql
#title:Some data about the MiMoTextBase such as Authors, Novels, publication years, tone etc.
prefix mmd:<http://data.mimotext.uni-trier.de/entity/>
prefix mmdt:<http://data.mimotext.uni-trier.de/prop/direct/> 
SELECT DISTINCT ?bgrf ?item ?authorlabel ?itemLabel ?year ?narrpers ?tonality ?pages ?normalized WHERE {
 ?item mmdt:P5 ?author; # who is the author?
       mmdt:P4 ?title; # what is the title?
       mmdt:P22 ?bgrf;  # what is the identifier in the bibliographic metadata?
       mmdt:P9 ?date; # what is the publication date?
 OPTIONAL {
   ?item mmdt:P27 ?narrpers; mmdt:P31 ?tonality; mmdt:P25 ?pages. 
 }
 BIND(YEAR(?date) as ?year).
 BIND(if(bound(?narrpers), ?narrpers, "unbekannt") as ?normalized)
 ?author rdfs:label ?authorlabel.
 FILTER(LANG(?authorlabel) = "en")
 SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE], fr". }
} ORDER BY ?year
```

<!-- 
<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/25rt89cw" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
                </p>
-->
```
SPARQL
:  SPARQL stands for SPARQL Protocol and RDF Query Language.
```

{% include warning.html content="Not every result can be visualized with all View-Types. It depends on the data you choose in your query." %}

<!-- Example: [Get a Timeline vizualisation ](https://tinyurl.com/28t86eyo){:target="\_blank", rel: "noopener noreferrer"} -->

Example: [Get a Timeline vizualisation ]([https://tinyurl.com/28t86eyo](https://query.mimotext.uni-trier.de/#%23title%3AAuthors%20on%20a%20timeline%2C%20limited%20to%20100%20results%0A%23defaultView%3ATimeline%7B%22hide%22%3A%5B%22%3Fdate%22%5D%7D%0Aprefix%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0ASelect%20%3Fauthorlabel%20%3Ftitel%20%28YEAR%28%3Fdate%29%20as%20%3Fyear%29%20%3Fdate%20%0Awhere%7B%0A%20%3Fitem%20mmdt%3AP5%20%3Fauthor%3B%20mmdt%3AP9%20%3Fdate%3B%20mmdt%3AP4%20%3Ftitel%20.%0A%20%3Fauthor%20rdfs%3Alabel%20%3Fauthorlabel%20.%0A%20FILTER%28lang%28%3Fauthorlabel%29%20%3D%20%22fr%22%29%20.%0A%20SERVICE%20wikibase%3Alabel%20%7Bbd%3AserviceParam%20wikibase%3Alanguage%20%22%7BAUTO_LANGUAGE%7D%22.%7D%0A%7DLIMIT%20100)){:target="\_blank", rel: "noopener noreferrer"}

<!-- [Previous](./tutorial_index.html){: .btn-primary}--> [Next](./select.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
