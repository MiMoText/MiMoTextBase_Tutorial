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
In the example query, we want to retrieve all novels written by François-Thomas-Marie de Baculard d’Arnaud and, if available, their tone. As not all novels have an entry for that property, we are going to use the `OPTIONAL`-function as follows: `OPTIONAL{ ?work wdt:P31 ?tonality.}`

Example: [Get all novels written by François-Thomas-Marie de Baculard d’ARNAUD and their tone](https://tinyurl.com/26veu4u7){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/26veu4u7" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe></p>

```
OPTIONAL
: If the optional part does not match, it creates no bindings but does not eliminate the solution.
```

[Previous](./filter.html){: .btn-primary} [Next](./federated.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
