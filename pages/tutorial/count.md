---
#title: Count
#tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: count.html
folder: tutorial
toc: false
topnav: topnav_tut

---

### **COUNT**

The `COUNT`-operation lets you, as the name suggests, count specified items in the graph. In order to get the sum of all novels in the MiMoText graph written by Tiphaigne de la Roche, you can change your `SELECT`-part of the query to `SELECT (count(?item) as ?count)`.
The variable in brackets of COUNT represents the item you want to sum up; the variable behind the `AS` will be shown as a new column in the results table.

Example: [Get the count of the novels written by Tiphaigne de la Roche](https://tinyurl.com/2526xpow){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://query.mimotext.uni-trier.de/#%23%20count%20novels%20by%20Tiphaigne%20de%20la%20Roche%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%28count%28%3Fitem%29%20as%20%3Fcount%29%20%0AWHERE%20%0A%7B%0A%20%20%3Fitem%20wdt%3AP5%20wd%3AQ940.%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms" ></iframe></p>

In this case you only want to count the novels of one author; if you want to query how many novels all the authors have written, you have to add a `GROUP BY` operation at the end of your query. The `GROUP BY` variable needs to be the same as the one in the `COUNT`-operation.
You can add `ORDER BY DESC (?count)` if the results should be ordered descending by the count.

Example: [Get the count of written novels per authors](https://tinyurl.com/27b8o6lh){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://query.mimotext.uni-trier.de/#%23%20Get%20the%20count%20of%20written%20novels%20per%20authors%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3FauthorName%20%28count%20%28%3FauthorName%29%20as%20%3Fcount%29%0A%20WHERE%20%7B%0A%20%20%20%3Fwork%20wdt%3AP5%20%3Fauthor%20.%20%23%20work%20has%20author.%0A%20%20%20%3Fauthor%20rdfs%3Alabel%20%3FauthorName%20.%20%23%20get%20author%20label%20%28not%20only%20Link%20to%20author%29%0A%20%20%20FILTER%28LANG%28%3FauthorName%29%20%3D%20%22en%22%29%20%23%20other%20options%3A%20%22fr%22%2C%20%22de%22.%20Filter%20is%20needed%20as%20there%20is%20more%20than%20one%20label%20%28language%20dependent%29%0A%7D%20%0Agroup%20by%20%3FauthorName%0Aorder%20by%20desc%20%28%3Fcount%29%0A%0A" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups" ></iframe></p>

To get all authors that have written more than 10 novels, you can add `HAVING (count(?authorName) > 10)` after the `GROUP BY`-operation; if you still want to see the count-result you should leave the `COUNT` in the `SELECT`-part.

Example: [Get the authors with more than 10 novels](https://tinyurl.com/2d29tgn2){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://query.mimotext.uni-trier.de/#%23Get%20the%20authors%20with%20more%20than%2010%20novels%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3FauthorName%20%28count%20%28%3FauthorName%29%20as%20%3Fcount%29%0A%20WHERE%20%7B%0A%20%20%20%3Fwork%20wdt%3AP5%20%3Fauthor%20.%20%23%20work%20has%20author.%0A%20%20%20%3Fauthor%20rdfs%3Alabel%20%3FauthorName%20.%20%23%20get%20author%20label%20%28not%20only%20Link%20to%20author%29%0A%20%20%20FILTER%28LANG%28%3FauthorName%29%20%3D%20%22en%22%29%20%23%20other%20options%3A%20%22fr%22%2C%20%22de%22.%20Filter%20is%20needed%20as%20there%20is%20more%20than%20one%20label%20%28language%20dependent%29%0A%7D%20%0Agroup%20by%20%3FauthorName%0Ahaving%20%28count%28%3FauthorName%29%20%3E%2010%29%0Aorder%20by%20desc%20%28%3Fcount%29%0A%0A%0A" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups"></iframe></p>

```
COUNT
: Count is a SPARQL set function which counts the number of times a given expression has a bound, and non-error value within the aggregate group.
```

[Previous](./bind.html){: .btn-primary} [Next](./limit.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
