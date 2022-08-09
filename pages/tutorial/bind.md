---
#title: Tutorial
#tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: bind.html
folder: tutorial
toc: false
#topnav: topnav
---

### **BIND**

If you want to assign some value based on known properties (e.g. based on some calculations done in the query) to a new variable, you can use the BIND-operation. It follows the syntax `BIND(SOME-OPERTION-WITH-KNOWN-VARIABLES AS ?new-variable)`.
As the dates of publication needed to be imported in DateTime-Format, we always get the First of January as the days and month for this information. We can use `BIND` to extract the `YEAR` of `P7` (date of publication) to assign the year to a new variable named `?year` which then will be displayed in the result table.

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23%20Query%20to%20retrieve%20the%20publicationyears%20of%20the%20novels%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3Fwork%20%3FworkLabel%20%3Fyear%20%20%23display%20work%20as%20Link%2C%20the%20Label%20and%20the%20year%0A%20WHERE%20%0A%20%7B%0A%20%20%20%3Fwork%20wdt%3AP9%20%3Fpubyear%20.%20%23%20P7%20%3A%20date%20of%20publication%0A%20%20%20%3Fwork%20rdfs%3Alabel%20%3FworkLabel%20.%20%23%20get%20the%20label%20of%20your%20item%20%28work%29%0A%20%20%20FILTER%28lang%28%3FworkLabel%29%20%3D%20%22fr%22%29%20.%20%23%20filter%20the%20language%2C%20otherwise%20you%20will%20get%20triple%20the%20amount%20of%20results%0A%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2C%20fr%22.%20%7D%0A%20%20%20%0A%20%20%20BIND%28YEAR%28%3Fpubyear%29%20as%20%3Fyear%29.%20%23%20extract%20the%20year%20of%20the%20datetime-formatted%20%3Fpubyear%20and%20bind%20it%20to%20%3Fyear%0A%20%7D%0A%20ORDER%20BY%20%3Fyear%20%23%20sort%20the%20results%20by%20ascending%20%28default%29%20year" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
                </p>

```
BIND
: The BIND form allows a value to be assigned to a variable from a basic graph pattern or property path expression.
Use of BIND ends the preceding basic graph pattern.
```

[Previous](./select.html){: .btn-primary} [Next](./count.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
