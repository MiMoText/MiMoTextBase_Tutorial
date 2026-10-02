---
#title: Tutorial
#tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: filter.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **FILTER**

> In previous queries we used the Q-Identifier to filter the results for a specific item. Some information does not have a Q-Identifier, like e.g. the publication date of a novel. With the `FILTER`-operation within the WHERE-part of the query we still can reduce the results to one (or some) information of interest. In order to get all authors that published a novel in 1800 we need to add P7 (date of publication). The operation `FILTER(YEAR(?pubdate) = 1800)` selects all publication dates where the `YEAR` is 1800 (as the dates are of “time datatype” it is important to only select the `YEAR ` of it.
> All common operations like `= > < ` can be used in the `FILTER `-part.

As we only want to retrieve the authors that published a novel in 1800 we will use the `DISTINCT `-Method to get each author once:

Example: [Filter for all authors that published a novel in 1800](https://query.mimotext.uni-trier.de/#%23title%3Aauthors%20that%20published%20a%20novel%20in%201800%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20DISTINCT%20%3FauthorName%20%28YEAR%28%3Fpubdate%29%20as%20%3Fyear%29%0AWHERE%20%7B%0A%20%20%3Fwork%20mmdt%3AP5%20%3Fauthor%3B%20mmdt%3AP9%20%3Fpubdate.%20%23%20work%20has%20author%20and%20a%20publication%20date%0A%20%20%3Fauthor%20rdfs%3Alabel%20%3FauthorName%20.%20%23%20get%20author%20label%20%28not%20only%20Link%20to%20author%29%0A%20%20FILTER%28LANG%28%3FauthorName%29%20%3D%20%22en%22%29.%20%23%20other%20options%3A%20%22fr%22%2C%20%22de%22.%20Filter%20is%20needed%20as%20there%20is%20more%20than%20one%20label%20%28language%20dependent%29%0A%20%20FILTER%28YEAR%28%3Fpubdate%29%20%3D%201800%29.%20%23%20filter%20for%20the%20publication%20date%20of%20interest%0A%7D){:target="\_blank", rel: "noopener noreferrer"}

<!--
<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://tinyurl.com/2ckd76n9" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups" ></iframe></p>
-->

```sparql
#title:authors that published a novel in 1800
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT DISTINCT ?authorName (YEAR(?pubdate) as ?year)
WHERE {
  ?work mmdt:P5 ?author; mmdt:P9 ?pubdate. # work has author and a publication date
  ?author rdfs:label ?authorName . # get author label (not only Link to author)
  FILTER(LANG(?authorName) = "en"). # other options: "fr", "de". Filter is needed as there is more than one label (language dependent)
  FILTER(YEAR(?pubdate) = 1800). # filter for the publication date of interest
}
```


Another example for the `FILTER` would be searching for a substring within a string-Item (like the Label). If you are interested in all authors whose names contain “beau”, you need to retrieve the label of all authors and add the phrase `FILTER(CONTAINS(LCASE(?authorName), "beau"))`.
As the function `CONTAINS` is a String-Matching-Function that is sensible to upper and lower case strings, it is important to set the characters in ?authorName to lowercase characters.

Example: [Get all authors whose name contains “beau”](https://query.mimotext.uni-trier.de/index.html#%23title%3AAuthors%20%20whose%20name%20contains%20%22beau%22%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3FauthorName%20%3Fauthor%0AWHERE%20%7B%0A%20%20%3Fauthor%20mmdt%3AP11%20mmd%3AQ11%20.%20%23%20item%20has%20property%20%22occupation%22%28P11%29%20namely%20%22author%22%28Q11%29.%0A%20%20%3Fauthor%20rdfs%3Alabel%20%3FauthorName%20.%20%23%20get%20author%20label%20%28not%20only%20URL%20to%20author%29%0A%20%20FILTER%28LANG%28%3FauthorName%29%20%3D%20%22fr%22%29%20.%0A%20%20FILTER%28CONTAINS%28LCASE%28%3FauthorName%29%2C%20%22beau%22%29%29.%0A%7D%0A){:target="\_blank", rel: "noopener noreferrer"}

<!--
<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://tinyurl.com/2ymeteoz" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups" ></iframe></p>
-->

```sparql
#title:Authors  whose name contains "beau"
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT ?authorName ?author
WHERE {
  ?author mmdt:P11 mmd:Q11 . # item has property "occupation"(P11) namely "author"(Q11).
  ?author rdfs:label ?authorName . # get author label (not only URL to author)
  FILTER(LANG(?authorName) = "fr") .
  FILTER(CONTAINS(LCASE(?authorName), "beau")).
}
```

In our graph the labels of authors are structured in `SURNAME` (in upper case) and first name (in lower case). So if you only want to retrieve authors whose surname contains “beau”, you also could replace the FILTER part as follows: FILTER(contains(?authorName, "BEAU")).
But be careful, you need to know the data in order to get the desired (or if any at all) output. `FILTER(contains(?authorName, "beau"))`would not give you any result, because the only author whose first name contains “beau” is “SAINT-AULAIRE, Yrieix Beaupoil, marquis de” and here the “B” in “Beaupoil” also is upper case so it is not a match.

If you are interested in other string functions, have a look at the section "Functions on strings" in the [SPARQL Wikibook](https://en.wikibooks.org/wiki/SPARQL/Expressions_and_Functions#Functions_on_strings){:target="\_blank", rel: "noopener noreferrer"}.

```
Filter
: FILTERs restrict solutions to those for which the filter expression evaluates to TRUE.

```

[Previous](./limit.html){: .btn-primary} [Next](./optional.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
