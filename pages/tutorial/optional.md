---
#title: Tutorial
#tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: optional.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **OPTIONAL**

While querying for more than one item, it is possible that you do not retrieve all the items you would expect, because the result contains only those items that fulfill all conditions. Nonetheless, sometimes you may want to get all items that satisfy one condition and some others optionally. This can happen because not all of the items in our graph contain all properties.
In such a case, you can make use of the function `OPTIONAL`.
In the example query, we want to retrieve all novels written by François-Thomas-Marie de Baculard d’Arnaud and, if available, their tone. As not all novels have an entry for that property, we are going to use the `OPTIONAL`-function as follows: `OPTIONAL{ ?work mmdt:P31 ?tonality.}`

Example: [Get all novels written by François-Thomas-Marie de Baculard d’ARNAUD and their tone](https://query.mimotext.uni-trier.de/#%23title%3ANovels%20by%20Fran%C3%A7ois-Thomas-Marie%20de%20Baculard%20d%E2%80%99ARNAUD%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3Fwork%20%3FworkLabel%20%3Ftonality%20%0AWHERE%0A%7B%0A%20%20%3Fwork%20mmdt%3AP5%20mmd%3AQ68%20%23%20work%20has%20author%20Fran%C3%A7ois-Thomas-Marie%20de%20Baculard%20d%E2%80%99ARNAUD%20%20%0A%20%20OPTIONAL%20%7B%20%3Fwork%20mmdt%3AP31%20%3Ftonality.%20%7D%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%20%7D%0A%7D){:target="\_blank", rel: "noopener noreferrer"}

<!--
<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/2xk2426o" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe></p>
-->

```sparql
#title:Novels by François-Thomas-Marie de Baculard d’ARNAUD
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/> 
SELECT ?work ?workLabel ?tonality 
WHERE
{
  ?work mmdt:P5 mmd:Q68 # work has author François-Thomas-Marie de Baculard d’ARNAUD  
  OPTIONAL { ?work mmdt:P31 ?tonality. }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]". }
}
```


```
OPTIONAL
: If the optional part does not match, it creates no bindings but does not eliminate the solution.
```

[Previous](./filter.html){: .btn-primary} [Next](./federated.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
