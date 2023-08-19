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

Example: [Show all narrative places (using the coordinate locations property of Wikidata)](https://tinyurl.com/26t7xv98){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://tinyurl.com/26t7xv98" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups" ></iframe></p>

```
Federated query
: SPARQL can be used to express queries across diverse data sources, whether the data is stored natively as RDF or viewed as RDF via middleware.

```

[Previous](./bind.html){: .btn-primary} [Next](./authors.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
