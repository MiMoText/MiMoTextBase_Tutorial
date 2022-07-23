---
#title: Tutorial
tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: limit.html
folder: tutorial
toc: false
---

### **LIMIT**

The last part of the count operation limited the results by the count-variable. If you want to limit your results (e.g. to get an idea of the result table if you query takes a lot of time, or to get the top-10 items), you can add the limit-Operation at the end of your query.

<iframe class="" src="https://query.wikidata.org/#%23Locations%20of%20aviation%20accidents%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fcoords%0AWHERE%0A%7B%0A%20%20%20%3Fitem%20wdt%3AP31%20wd%3AQ744913.%20%20%20%20%20%20%23%20item%20is%20an%20instance%20of%20an%20aviation%20accident%0A%20%20%20%3Fitem%20wdt%3AP625%20%3Fcoords.%20%20%20%20%20%20%20%20%23%20item%27s%20coordinates%20are%20collected%20by%20the%20%3Fcoords%20variable%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" style="width:100%;max-width:100%;height:450px" frameborder="0"></iframe>

```
LIMIT
: The LIMIT clause puts an upper bound on the number of solutions returned.
```

[Previous](./count.html){: .btn-primary} [Next](./filter.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
