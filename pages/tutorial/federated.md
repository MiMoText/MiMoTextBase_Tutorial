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

One major advantage of linked open data is that we can use not only the information stored within our graph. Instead, because we have matched most of our values to existing WikiData-Items (where possible), we are able to write queries linking to different Knowledge Bases like WikiData [or others that also link to WikiData-Items].
As we have location information like places of publication or narrative locations of the novels and WikiData provides coordinates to many locations, we can write a federated query to retrieve those and visualize the locations on a map.

We plan to change the prefixes in our MiMoTextBase soon, so that the wikidata prefixes do not have to be changed. However, the default setting for each Wikibase instance are the Wikidata prefixes, so we have so far changed the actual Wikidata prefixes as shown below. First you need to define the Prefixes you are going to use for the other knowledge base in the query as:

`PREFIX wid: <http://www.wikidata.org/entity/> #wikidata wd PREFIX widt: <http://www.wikidata.org/prop/direct/> #wikidata wdt`

Within the `WHERE`-part you can query all items you want to as long as they have a `P13` (exact match with WikiData) property.
So in our example
`?item wdt:P32 ?nar_loc. #a novel has a narrative location ?nar_loc wdt:P13 ?WikiLink. #the narrative location has an exact match.`

Next using the `SERVICE` referring to the WikiData-SPARQL-Endpoint, we can get all information listed on the matching WikiData-entry. To write the triple, we now need to use the property-values of WikiData. Here `P625` is the coordinate location of the WikiData entity.

`SERVICE <https://query.wikidata.org/sparql> { ?wikidataEntityLink widt:P625 ?coordinateLocation. } `

Example: [Show all narrative places in Europe (using the coordinate locations property of Wikidata)](https://tinyurl.com/24e5b4g8){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://query.mimotext.uni-trier.de/#%23defaultView%3AMap%7B%22hide%22%3A%20%5B%22%3Fnar_loc%22%5D%2C%20%22markercluster%22%3A%22true%22%7D%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASelect%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3Fnar_loc%20%3Fnar_locLabel%20%3FWikiDataEntity%20%3FcoordinateLocation%20%0A%7B%0A%20%20%3Fitem%20wdt%3AP32%20%3Fnar_loc.%0A%20%20%3Fnar_loc%20wdt%3AP13%20%3FWikiDataEntity.%0A%20%20%0A%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiDataEntity%20%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20widt%3AP625%20%3FcoordinateLocation%0A%20%20%7D%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%0A%20%20%20%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%0A%20%20%7D%0A%7D%0A" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups" ></iframe></p>

```
Federated query
: SPARQL can be used to express queries across diverse data sources, whether the data is stored natively as RDF or viewed as RDF via middleware.

```

[Previous](./bind.html){: .btn-primary} [Next](./authors.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
