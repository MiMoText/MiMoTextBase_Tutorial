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

Example: [Retrieve the publication years of the novels](https://tinyurl.com/2czt8pff){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/2czt8pff" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe></p>

```
BIND
: The BIND form allows a value to be assigned to a variable from a basic graph pattern or property path expression.
Use of BIND ends the preceding basic graph pattern.
```

[Previous](./select.html){: .btn-primary} [Next](./count.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
