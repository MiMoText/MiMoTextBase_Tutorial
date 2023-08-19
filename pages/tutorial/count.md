---
#title: Count
#tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: count.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **COUNT**

The `COUNT`-operation lets you, as the name suggests, count specified items in the graph. In order to get the sum of all novels in the MiMoText graph written by Tiphaigne de la Roche, you can change your `SELECT`-part of the query to `SELECT (count(?item) as ?count)`.
The variable in brackets of COUNT represents the item you want to sum up; the variable behind the `AS` will be shown as a new column in the results table.

Example: [Get the count of the novels written by Tiphaigne de la Roche](https://tinyurl.com/248urno6){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/248urno6" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms" ></iframe></p>

In this case you only want to count the novels of one author; if you want to query how many novels all the authors have written, you have to add a `GROUP BY` operation at the end of your query. The `GROUP BY` variable needs to be the same as the one in the `COUNT`-operation.
You can add `ORDER BY DESC (?count)` if the results should be ordered descending by the count.

Example: [Get the count of written novels per author](https://tinyurl.com/2yazybnq){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/2yazybnq" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups" ></iframe></p>

To get all authors that have written more than 10 novels, you can add `HAVING (count(?authorName) > 10)` after the `GROUP BY`-operation; if you still want to see the count-result you should leave the `COUNT` in the `SELECT`-part.

Example: [Get the authors with more than 10 novels](https://tinyurl.com/29lwuzhr){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://tinyurl.com/29lwuzhr" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups"></iframe></p>

```
COUNT
: Count is a SPARQL set function which counts the number of times a given expression has a bound, and non-error value within the aggregate group.
```

[Previous](./bind.html){: .btn-primary} [Next](./limit.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
