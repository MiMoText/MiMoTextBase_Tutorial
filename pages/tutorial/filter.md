---
#title: Tutorial
#tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: filter.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **FILTER**

> In previous queries we used the Q-Identifier to filter the results for a specific item. Some information does not have a Q-Identifier, like e.g. the publication date of a novel. With the `FILTER`-operation within the WHERE-part of the query we still can reduce the results to one (or some) information of interest. In order to get all authors that published a novel in 1800 we need to add P7 (date of publication). The operation `FILTER(YEAR(?pubdate) = 1800)` selects all publication dates where the `YEAR` is 1800 (as the dates are of “time datatype” it is important to only select the `YEAR ` of it.
> All common operations like `= > < ` can be used in the `FILTER `-part.

As we only want to retrieve the authors that published a novel in 1800 we will use the `DISTINCT `-Method to get each author once:

Example: [Filter for all authors that published a novel in 1800](https://tinyurl.com/2ckd76n9){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://tinyurl.com/2ckd76n9" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups" ></iframe></p>

Another example for the `FILTER` would be searching for a substring within a string-Item (like the Label). If you are interested in all authors whose names contain “beau”, you need to retrieve the label of all authors and add the phrase `FILTER(CONTAINS(LCASE(?authorName), "beau"))`.
As the function `CONTAINS` is a String-Matching-Function that is sensible to upper and lower case strings, it is important to set the characters in ?authorName to lowercase characters.

Example: [Get all authors whose name contains “beau”](https://tinyurl.com/2ymeteoz){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen  src="https://tinyurl.com/2ymeteoz" referrerpolicy="origin" sandbox="allow-forms allow-scripts allow-same-origin allow-popups" ></iframe></p>

In our graph the labels of authors are structured in `SURNAME` (in upper case) and first name (in lower case). So if you only want to retrieve authors whose surname contains “beau”, you also could replace the FILTER part as follows: FILTER(contains(?authorName, "BEAU")).
But be careful, you need to know the data in order to get the desired (or if any at all) output. `FILTER(contains(?authorName, "beau"))`would not give you any result, because the only author whose first name contains “beau” is “SAINT-AULAIRE, Yrieix Beaupoil, marquis de” and here the “B” in “Beaupoil” also is upper case so it is not a match.

If you are interested in other string functions, have a look at the section "Functions on strings" in the [SPARQL Wikibook](https://en.wikibooks.org/wiki/SPARQL/Expressions_and_Functions#Functions_on_strings){:target="\_blank", rel: "noopener noreferrer"}.

```
Filter
: FILTERs restrict solutions to those for which the filter expression evaluates to TRUE.

```

[Previous](./limit.html){: .btn-primary} [Next](./optional.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
