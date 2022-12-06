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

Example: [SELECT all the items WHERE the author is Tiphaigne de la Roche ](https://tinyurl.com/2knv3bjr){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/2knv3bjr" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
                </p>

If you have a look at the results, you see the items, but you might be looking for the names of the novels, which are the labels of the items.

In order to display labels, we have to use `SERVICE wikibase:label { bd:serviceParam wikibase:language "en”. }`. The “`en`” specifies that we want to display the English labels. Our graph is multilingual (French, English and German), so the results can differ depending on the chosen output language. Use “`fr`” for French or “`de`” for German labels. This is the same query with English labels:

Example: [SELECT all the items and their labels WHERE the author is Tiphaigne de la Roche ](https://tinyurl.com/2hlhtzbl){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/2hlhtzbl" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
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
