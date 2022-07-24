---
#title: Count
tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: count.html
folder: tutorial
toc: false
---

### **Count**

The `COUNT`-operation lets you, as the name suggests, count specified items in the graph. In order to get the sum of all novels in the MiMoText graph written by Tiphaigne de la Roche, you can change your `SELECT`-part of the query to `SELECT (count(?item) as ?count)`.
The variable in brackets of COUNT represents the item you want to sum up; the variable behind the `AS` will be shown as a new column in the results table.

Example: Get the count of the novels written by Tiphaigne de la Roche

<iframe class="" src="https://query.wikidata.org/#%23Locations%20of%20aviation%20accidents%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fcoords%0AWHERE%0A%7B%0A%20%20%20%3Fitem%20wdt%3AP31%20wd%3AQ744913.%20%20%20%20%20%20%23%20item%20is%20an%20instance%20of%20an%20aviation%20accident%0A%20%20%20%3Fitem%20wdt%3AP625%20%3Fcoords.%20%20%20%20%20%20%20%20%23%20item%27s%20coordinates%20are%20collected%20by%20the%20%3Fcoords%20variable%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" style="width:100%;max-width:100%;height:450px" frameborder="0"></iframe>

In this case you only want to count the novels of one author; if you want to query how many novels all the authors have written, you have to add a `GROUP BY` operation at the end of your query. The `GROUP BY` variable needs to be the same as the one in the `COUNT`-operation.
You can add `ORDER BY DESC (?count)` if the results should be ordered descending by the count.

Example: Get the count of written novels per authors

<iframe class="" src="https://query.wikidata.org/#%23Locations%20of%20aviation%20accidents%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fcoords%0AWHERE%0A%7B%0A%20%20%20%3Fitem%20wdt%3AP31%20wd%3AQ744913.%20%20%20%20%20%20%23%20item%20is%20an%20instance%20of%20an%20aviation%20accident%0A%20%20%20%3Fitem%20wdt%3AP625%20%3Fcoords.%20%20%20%20%20%20%20%20%23%20item%27s%20coordinates%20are%20collected%20by%20the%20%3Fcoords%20variable%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" style="width:100%;max-width:100%;height:450px" frameborder="0"></iframe>

To get all authors that have written more than 10 novels, you can add `HAVING (count(?authorName) > 10)` after the `GROUP BY`-operation; if you still want to see the count-result you should leave the `COUNT` in the `SELECT`-part.

Example: Get the authors with more than 10 novels

<iframe class="" src="https://query.wikidata.org/#%23Locations%20of%20aviation%20accidents%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fcoords%0AWHERE%0A%7B%0A%20%20%20%3Fitem%20wdt%3AP31%20wd%3AQ744913.%20%20%20%20%20%20%23%20item%20is%20an%20instance%20of%20an%20aviation%20accident%0A%20%20%20%3Fitem%20wdt%3AP625%20%3Fcoords.%20%20%20%20%20%20%20%20%23%20item%27s%20coordinates%20are%20collected%20by%20the%20%3Fcoords%20variable%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" style="width:100%;max-width:100%;height:450px" frameborder="0"></iframe>

```
COUNT
: Count is a SPARQL set function which counts the number of times a given expression has a bound, and non-error value within the aggregate group.
```

[Previous](./bind.html){: .btn-primary} [Next](./limit.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
