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

### **SELECT**

We can start by a very basic SPARQL query, which lists all of the novels of a certain author. We `SELECT` all items `WHERE` the condition 'has author' has the value 'Tiphaigne de la Roche'.The `WHERE` defines which data should be picked, and the `SELECT` defines which data should be displayed.

<iframe class="" src="https://query.wikidata.org/#%23Locations%20of%20aviation%20accidents%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fcoords%0AWHERE%0A%7B%0A%20%20%20%3Fitem%20wdt%3AP31%20wd%3AQ744913.%20%20%20%20%20%20%23%20item%20is%20an%20instance%20of%20an%20aviation%20accident%0A%20%20%20%3Fitem%20wdt%3AP625%20%3Fcoords.%20%20%20%20%20%20%20%20%23%20item%27s%20coordinates%20are%20collected%20by%20the%20%3Fcoords%20variable%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" style="width:100%;max-width:100%;height:450px" frameborder="0"></iframe>


If you have a look at the results, you see the items, but you might be looking for the names of the novels, which are the labels of the items.

In order to display labels, we have to use `SERVICE wikibase:label { bd:serviceParam wikibase:language "en”. }`. The “`en`” specifies that we want to display the English labels. Our graph is multilingual (French, English and German), so the results can differ depending on the chosen output language. Use “`fr`” for French or “`de`” for German labels. This is the same query with English labels:

Note:
The name of the variables can be chosen freely, but they always need the “?” at the beginning and need to stay the same in the whole query.
After a triple pattern you should use the “.”
In a basic `SELECT-WHERE`-Query, you can add as many variables in the `SELECT` part as you wish as long as they appear in the `WHERE`-part (otherwise they won’t contain any information and stay empty).

```
SELECT
: The SELECT form of results returns variables and their bindings directly.

```

[Previous](./tutorial_index.html){: .btn-primary} [Next](./limit.html){: .btn-primary}

<!-- {% include links.html %} -->
