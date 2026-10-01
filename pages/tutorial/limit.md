---
#title: Tutorial
#tags: [getting_started]

keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: limit.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **LIMIT**

The last part of the count operation limited the results by the count variable. If you want to limit your results (e.g. to get an idea of the result table if your query takes a lot of time, or to get the top 10 items), you can add the limit operation at the end of your query.

Example: [Limit the result to top 10](https://tinyurl.com/29qcyffc){:target="\_blank", rel: "noopener noreferrer"}

<!--<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/29qcyffc" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe></p>
-->

```sparql
#tile:Authors and their count of novels limited to top 10
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT ?authorName (count (?authorName) as ?count)
WHERE {
   ?work mmdt:P5 ?author . # work has author.
   ?author rdfs:label ?authorName . # get author label (not only Link to author)
   FILTER(LANG(?authorName) = "en") . # other options: "fr", "de". Filter is needed as there is more than one label (language dependent)
}

group by ?authorName
order by desc (?count)
limit 10
```

```
LIMIT
: The LIMIT clause puts an upper bound on the number of solutions returned.
```

[Previous](./count.html){: .btn-primary} [Next](./filter.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
