---
#title: Tutorial
tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: select.html
folder: tutorial
toc: false
---

### **The simplest query: SELECT WHERE**

We can start by a very basic SPARQL query, which lists all of the novels of a certain author. We `SELECT` all items `WHERE` the condition 'has author' has the value 'Tiphaigne de la Roche'.The `WHERE` defines which data should be picked, and the `SELECT` defines which data should be displayed.

Example: [SELECT all the items WHERE the author is Tiphaigne de la Roche ](https://tinyurl.com/235c7uen).

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23%20novels%20by%20Tiphaigne%20de%20la%20Roche%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3Fitem%20%0AWHERE%20%0A%7B%0A%20%20%3Fitem%20wdt%3AP5%20wd%3AQ940.%0A%20%20%20%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D" referrerpolicy="origin" </iframe>
                </p>

If you have a look at the results, you see the items, but you might be looking for the names of the novels, which are the labels of the items.

In order to display labels, we have to use `SERVICE wikibase:label { bd:serviceParam wikibase:language "en”. }`. The “`en`” specifies that we want to display the English labels. Our graph is multilingual (French, English and German), so the results can differ depending on the chosen output language. Use “`fr`” for French or “`de`” for German labels. This is the same query with English labels:

Example: [SELECT all the items and their labels WHERE the author is Tiphaigne de la Roche ](https://tinyurl.com/23pzmwxq)

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de%23%20novels%20by%20Tiphaigne%20de%20la%20Roche%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3Fitem%20%3FitemLabel%0AWHERE%20%0A%7B%0A%20%20%3Fitem%20wdt%3AP5%20wd%3AQ940.%0A%20%20%20%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D" referrerpolicy="origin" </iframe>
                </p>

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
