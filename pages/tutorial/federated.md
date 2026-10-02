---
#title: Tutorial
#tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: federated.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **Federated queries**

One major advantage of linked open data is that we can use not only the information stored within our graph, but also write queries linking to different knowledge bases like Wikidata or others that link to Wikidata items. This is possible because we have matched most of our values to existing Wikidata items.

Since we have location information like places of publication or narrative locations of the novels and Wikidata provides coordinates to many locations, we can write a federated query to retrieve those and visualize the locations on a map.

First you need to define the prefixes you are going to use for the other knowledge base in the query as:

`PREFIX wd: <http://www.wikidata.org/entity/> #wikidata wd 
PREFIX wdt: <http://www.wikidata.org/prop/direct/> #wikidata wdt`

Within the `WHERE`-part you can query all items you want to as long as they have a `P13` (exact match with Wikidata) property.
So in our example
`?item mmdt:P32 ?nar_loc. #a novel has a narrative location ?nar_loc mmdt:P13 ?WikiLink. #the narrative location has an exact match.`

Next using the `SERVICE` referring to the Wikidata SPARQL endpoint, we can get all information listed on the matching Wikidata entry. To write the triple, we now need to use the property values of Wikidata. Here `P625` is the coordinate location of the Wikidata entity.

`SERVICE <https://query.wikidata.org/sparql> { ?wikidataEntityLink widt:P625 ?coordinateLocation. } `

Example: [Show all narrative places (using the coordinate locations property of Wikidata)](https://query.mimotext.uni-trier.de/#%23title%3ANarrative%20places%20%28using%20Wikidata%20coordinate%20locations%29%0A%23defaultView%3AMap%7B%22hide%22%3A%20%5B%22%3Fnar_loc%22%5D%2C%20%22markercluster%22%3A%22true%22%7D%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3Fnar_loc%20%3Fnar_locLabel%20%3FWikiDataEntity%20%3FcoordinateLocation%0AWHERE%20%7B%20%3Fitem%20mmdt%3AP32%20%3Fnar_loc.%0A%20%20%3Fnar_loc%20mmdt%3AP13%20%3FWikiDataEntity.%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiDataEntity%20wdt%3AP625%20%3FcoordinateLocation%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A){:target="\_blank", rel: "noopener noreferrer"}

<!--
<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://tinyurl.com/26t7xv98" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups" ></iframe></p>
-->

```sparql
#title:Narrative places (using Wikidata coordinate locations)
#defaultView:Map{"hide": ["?nar_loc"], "markercluster":"true"}
PREFIX wd: <http://www.wikidata.org/entity/> #wikidata wd
PREFIX wdt: <http://www.wikidata.org/prop/direct/> #wikidata wdt
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/> 
SELECT DISTINCT ?item ?itemLabel ?nar_loc ?nar_locLabel ?WikiDataEntity ?coordinateLocation
WHERE { ?item mmdt:P32 ?nar_loc.
  ?nar_loc mmdt:P13 ?WikiDataEntity.
  #Federated Query -> Wikidata
  SERVICE <https://query.wikidata.org/sparql> {
    ?WikiDataEntity wdt:P625 ?coordinateLocation
  }           
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en" . }
}
```


```
Federated query
: SPARQL can be used to express queries across diverse data sources, whether the data is stored natively as RDF or viewed as RDF via middleware.

```

[Previous](./bind.html){: .btn-primary} [Next](./authors.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
