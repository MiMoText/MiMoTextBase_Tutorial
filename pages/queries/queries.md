---
title: Queries used in different publications
#keywords:
#summary: Queries used in different publications
sidebar: false
permalink: queries.html
folder: queries
toc: true
---

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


### DH Abstract