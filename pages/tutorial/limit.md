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

Example: [Limit the result to top 10](https://query.mimotext.uni-trier.de/#%23tile%3AAuthors%20and%20their%20count%20of%20novels%20limited%20to%20top%2010%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3FauthorName%20%28count%20%28%3FauthorName%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%20%20%3Fwork%20mmdt%3AP5%20%3Fauthor%20.%20%23%20work%20has%20author.%0A%20%20%20%3Fauthor%20rdfs%3Alabel%20%3FauthorName%20.%20%23%20get%20author%20label%20%28not%20only%20Link%20to%20author%29%0A%20%20%20FILTER%28LANG%28%3FauthorName%29%20%3D%20%22en%22%29%20.%20%23%20other%20options%3A%20%22fr%22%2C%20%22de%22.%20Filter%20is%20needed%20as%20there%20is%20more%20than%20one%20label%20%28language%20dependent%29%0A%7D%0A%0Agroup%20by%20%3FauthorName%0Aorder%20by%20desc%20%28%3Fcount%29%0Alimit%2010%0A){:target="\_blank", rel: "noopener noreferrer"}

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
