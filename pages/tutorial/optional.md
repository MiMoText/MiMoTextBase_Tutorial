---
#title: Tutorial
tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: union.html
folder: tutorial
toc: false
---

### **OPTIONAL**

> While querying for more than one item, it is possible that you do not retrieve all the items you would expect, because the result contains only those items that fulfill all conditions. Nonetheless, sometimes you may want to get all items that satisfy one condition and some others optionally. This can happen because not all of the items in our graph contain all properties.
In such a case, you can make use of the function <code>OPTIONAL</code>.
In the example query, we want to retrieve all novels written by Jean Castilhon and, if available, their tonality. As not all novels have an entry for that property, we are going to use the <code>OPTIONAL</code>-function as follows: <code>OPTIONAL{ ?work wdt:P50 ?tonality.}</code> 

Example: Get all novels written by François-Thomas-Marie de Baculard d’ARNAUD and their tonality

<iframe style="width: 80vw; height: 50vh; border: none;" src="http://zora.uni-trier.de:11100/embed.html#SELECT%20%3Fwork%20%3FworkLabel%20%3Ftonality%20%0AWHERE%0A%7B%0A%20%20%3Fwork%20wdt%3AP5%20wd%3AQ52.%20%23%20work%20has%20author%20Fran%C3%A7ois-Thomas-Marie%20de%20Baculard%20d%E2%80%99ARNAUD%20%20%0A%20%20OPTIONAL%20%7B%20%3Fwork%20wdt%3AP50%20%3Ftonality.%20%7D%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%22.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>
```
First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.
```

[Previous](./limit.html){: .btn-primary} [Next](./bind.html){: .btn-primary}

<!-- {% include links.html %} -->
