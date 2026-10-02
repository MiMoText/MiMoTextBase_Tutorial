---
#title: Tutorial
#tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: select.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **The simplest query: SELECT WHERE**

We can start by a very basic SPARQL query, which lists all of the novels of a certain author. We `SELECT` all items `WHERE` the condition 'has author' has the value 'Tiphaigne de la Roche'.The `WHERE` defines which data should be picked, and the `SELECT` defines which data should be displayed.

<!-- Example: [SELECT all the items WHERE the author is Tiphaigne de la Roche ](https://tinyurl.com/2b8m9m7b){:target="\_blank", rel: "noopener noreferrer"} -->

Example: [SELECT all the items WHERE the author is Tiphaigne de la Roche ](https://query.mimotext.uni-trier.de/#%23title%3Anovels%20by%20Tiphaigne%20de%20la%20Roche%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fitem%0AWHERE%20%0A%7B%0A%20%20%3Fitem%20mmdt%3AP5%20mmd%3AQ940.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D){:target="\_blank", rel: "noopener noreferrer"}

<!-- 
<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/2b8m9m7b" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
                </p>
-->
```sparql
#title:novels by Tiphaigne de la Roche
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/> 

SELECT ?item
WHERE 
{
  ?item mmdt:P5 mmd:Q940.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

If you have a look at the results, you see the items, but you might be looking for the names of the novels, which are the labels of the items.

In order to display labels, we have to use `SERVICE wikibase:label { bd:serviceParam wikibase:language "en”. }`. The “`en`” specifies that we want to display the English labels. Our graph is multilingual (French, English and German), so the results can differ depending on the chosen output language. Use “`fr`” for French or “`de`” for German labels. This is the same query with English labels:


<!-- Example: [SELECT all the items and their labels WHERE the author is Tiphaigne de la Roche ](https://tinyurl.com/2ddclspa){:target="\_blank", rel: "noopener noreferrer"} -->

Example: [SELECT all the items and their labels WHERE the author is Tiphaigne de la Roche ](https://query.mimotext.uni-trier.de/#%23title%3Anovels%20by%20Tiphaigne%20de%20la%20Roche%2C%20with%20labels%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fitem%20%3FitemLabel%0AWHERE%20%0A%7B%0A%20%20%3Fitem%20mmdt%3AP5%20mmd%3AQ940.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D){:target="\_blank", rel: "noopener noreferrer"}

<!--
<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/2ddclspa" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
                </p>
-->

```sparql
#title:novels by Tiphaigne de la Roche, with labels
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/> 

SELECT ?item ?itemLabel
WHERE 
{
  ?item mmdt:P5 mmd:Q940.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

Note:
The name of the variables can be chosen freely, but they always need the “?” at the beginning and need to stay the same in the whole query.
After a triple pattern you should use the “.”
In a basic `SELECT-WHERE`-Query, you can add as many variables in the `SELECT` part as you wish as long as they appear in the `WHERE`-part (otherwise they won’t contain any information and stay empty).

```
SELECT
: The SELECT form of results returns variables and their bindings directly.

```

[Previous](./getting_started.html){: .btn-primary} [Next](./bind.html){: .btn-primary}

{% include help.html %}
