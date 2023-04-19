---
title: Queries used in different publications
#keywords:
#summary: Queries used in different publications
sidebar: false
permalink: queries.html
folder: queries
toc: true
---

### DH Abstract

1\. [Which thematic concepts are represented in the French novel 1751-1800?](https://query.mimotext.uni-trier.de/index.html#%23%20Which%20thematic%20concepts%20are%20represented%20in%20the%20corpus%3F%20%0A%23defaultView%3ABubbleChart%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3FtopLabel%20%28count%28%2a%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%3Fitem%20wdt%3AP36%20%3Ftop%20.%20%23%20P36%20%3D%20thematic%20concept%20of%20the%20literary%20work%0A%20%3Ftop%20rdfs%3Alabel%20%3FtopLabel%20.%0A%20FILTER%28LANG%28%3FtopLabel%29%20%3D%20%22en%22%29.%0A%7D%0AGROUP%20BY%20%3FtopLabel%0AORDER%20BY%20desc%28%3Fcount%29%0A%0A%0A%0A){:target="_blank"}

```sparql
# Which thematic concepts are represented in the corpus? 
#defaultView:BubbleChart
PREFIX wd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX wdt:<http://data.mimotext.uni-trier.de/prop/direct/> 
SELECT ?topLabel (count(*) as ?count)
WHERE {
 ?item wdt:P36 ?top . # P36 = thematic concept of the literary work
 ?top rdfs:label ?topLabel .
 FILTER(LANG(?topLabel) = "en").
}
GROUP BY ?topLabel
ORDER BY desc(?count)
```


2\. [Federated queries in SPARQL allow querying several knowledge graphs simultaneously.](https://query.mimotext.uni-trier.de/index.html#%23%20show%20authors%2C%20their%20Wikidata%20match%2C%20their%20birth%20dates%20in%20a%20timeline%20%0A%23defaultView%3ATimeline%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20prefix%20definition%20for%20entity%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20prefix%20definition%20for%20property%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%23mimotext%20prefix%20for%20entity%20is%20wd%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%23mimotext%20prefix%20for%20property%20is%20wdt%0ASELECT%20%3Fauthor%20%3FauthorLabel%20%3FwikiLink%20%3Fbirth%20%3Fimage%20%0AWHERE%7B%0A%20%20%3Fauthor%20wdt%3AP11%20%3Foccupation.%0A%20%20%3Fauthor%20wdt%3AP13%20%3FwikiLink.%0A%20%20%3Fauthor%20rdfs%3Alabel%20%3FauthorLabel.%0A%20%20FILTER%28LANG%28%3FauthorLabel%29%20%3D%20%22en%22%29.%0A%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FwikiLink%20widt%3AP569%20%3Fbirth.%20%0A%20%20%20%20OPTIONAL%7B%20%20%20%3FwikiLink%20widt%3AP18%20%3Fimage.%7D%0A%20%20%7D%20%20%20%20%20%20%20%20%20%0A%7D%0A){:target="_blank"}

```sparql
# show authors, their Wikidata match, their birth dates in a timeline 
#defaultView:Timeline
PREFIX wid: <http://www.wikidata.org/entity/> #wikidata prefix definition for entity
PREFIX widt: <http://www.wikidata.org/prop/direct/> #wikidata prefix definition for property
PREFIX wd:<http://data.mimotext.uni-trier.de/entity/> #mimotext prefix for entity is wd
PREFIX wdt:<http://data.mimotext.uni-trier.de/prop/direct/> #mimotext prefix for property is wdt
SELECT ?author ?authorLabel ?wikiLink ?birth ?image 
WHERE{
  ?author wdt:P11 ?occupation.
  ?author wdt:P13 ?wikiLink.
  ?author rdfs:label ?authorLabel.
  FILTER(LANG(?authorLabel) = "en").
          
  SERVICE <https://query.wikidata.org/sparql> {
    ?wikiLink widt:P569 ?birth. 
    OPTIONAL{   ?wikiLink widt:P18 ?image.}
  }         
}
```

3\. [Query to retrieve the number of authors having a wikidata-match](https://query.mimotext.uni-trier.de/index.html#%23%20Query%20to%20retrieve%20the%20number%20of%20authors%20having%20a%20wikidata-match%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0ASELECT%20%3FauthorName%0AWHERE%20%7B%0A%20%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11%20.%20%23%20item%20has%20property%20%22occupation%22%28P11%29%20namely%20%22author%22%28Q11%29.%0A%20%20%20%3Fauthor%20rdfs%3Alabel%20%3FauthorName%20.%20%23%20get%20author%20label%20%28not%20only%20Link%20to%20author%29%0A%20%20%20FILTER%28LANG%28%3FauthorName%29%20%3D%20%22en%22%29%20%23%20other%20options%3A%20%22fr%22%2C%20%22de%22.%20Filter%20is%20needed%20as%20there%20is%20more%20than%20one%20label%20%28language%20dependent%29%0A%20%20%20%3Fauthor%20wdt%3AP13%20%3Fwikimatch.%0A%7D%0AORDER%20BY%20%3FauthorName%0A){:target="_blank"}

```sparql
# Query to retrieve the number of authors having a wikidata-match
PREFIX wd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX wdt:<http://data.mimotext.uni-trier.de/prop/direct/>
SELECT ?authorName
WHERE {
   ?author wdt:P11 wd:Q11 . # item has property "occupation"(P11) namely "author"(Q11).
   ?author rdfs:label ?authorName . # get author label (not only Link to author)
   FILTER(LANG(?authorName) = "en") # other options: "fr", "de". Filter is needed as there is more than one label (language dependent)
   ?author wdt:P13 ?wikimatch.
}
ORDER BY ?authorName
```


<!--
### DHd Abstract

[Welche thematischen Konzepte sind im französischen Roman 1751-1800 vertreten?](https://query.mimotext.uni-trier.de/index.html#%23defaultView%3ABubbleChart%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3FtopLabel%20%28count%28%2a%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%3Fitem%20wdt%3AP36%20%3Ftop%20.%0A%20%3Ftop%20rdfs%3Alabel%20%3FtopLabel%20.%0A%20filter%28lang%28%3FtopLabel%29%20%3D%20%22en%22%29%0A%7D%0AGROUP%20BY%20%3FtopLabel%0AORDER%20BY%20desc%28%3Fcount%29)


```sql
#defaultView:BubbleChart
prefix wd:<http://data.mimotext.uni-trier.de/entity/>
prefix wdt:<http://data.mimotext.uni-trier.de/prop/direct/> 
SELECT ?topLabel (count(*) as ?count)
WHERE {
 ?item wdt:P36 ?top .
 ?top rdfs:label ?topLabel .
 filter(lang(?topLabel) = "en")
}
GROUP BY ?topLabel
ORDER BY desc(?count)
```
-->