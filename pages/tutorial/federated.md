---
#title: Tutorial
tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: federated.html
folder: tutorial
toc: false
---

### **Federated queries**

One major advantage of linked open data is that we can use not only the information stored within our graph. Instead, because we have matched most of our values to existing WikiData-Items (where possible), we are able to write queries linking to different Knowledge Bases like WikiData [or others that also link to WikiData-Items].
As we have location information like places of publication or narrative locations of the novels and WikiData provides coordinates to many locations, we can write a federated query to retrieve those and visualize the locations on a map.

We plan to change the prefixes in our MiMoTextBase soon (see future work [LINK]), so that the wikidata prefixes do not have to be changed. However, the default setting for each Wikibase instance are the Wikidata prefixes, so we have so far changed the actual Wikidata prefixes as shown below. First you need to define the Prefixes you are going to use for the other knowledge base in the query as:

`PREFIX wid: <http://www.wikidata.org/entity/> #wikidata wd
PREFIX widt: <http://www.wikidata.org/prop/direct/> #wikidata wdt`

Within the `WHERE`-part you can query all items you want to as long as they have a `P13`  (exact match with WikiData) property.
So in our example
`?item wdt:P10 ?pub_place.    #a novel has a place of publication
?pub_place wdt:P13 ?WikiLink.    #the place of publication has an exact match.`

Next using the `SERVICE` referring to the WikiData-SPARQL-Endpoint, we can get all information listed on the matching WikiData-entry. To write the triple, we now need to use the property-values of WikiData. Here `P625` is the coordinate location of the WikiData entity.

`SERVICE <https://query.wikidata.org/sparql> {
   ?wikidataEntityLink widt:P625 ?coordinateLocation.
 }   `

 Example: Show all narrative places in Europe (using the coordinate locations property of Wikidata)   


```
Federated query
: SPARQL can be used to express queries across diverse data sources, whether the data is stored natively as RDF or viewed as RDF via middleware.

```

[Previous](./bind.html){: .btn-primary} [Next](./errors.html){: .btn-primary}

<!-- {% include links.html %} -->
