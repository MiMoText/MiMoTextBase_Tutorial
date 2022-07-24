---
#title: Tutorial
tags: [getting_started]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: filter.html
folder: tutorial
toc: false
---

### **Filter**

> In previous queries we used the Q-Identifier to filter the results for a specific item. Some information does not have a Q-Identifier, like e.g. the publication date of a novel. With the `FILTER`-operation within the WHERE-part of the query we still can reduce the results to one (or some) information of interest. In order to get all authors that published a novel in 1800 we need to add P7 (date of publication). The operation  `FILTER(YEAR(?pubdate) = 1800)` selects all publication dates where the  `YEAR` is 1800 (as the dates are of  “time datatype” it is important to only select the  `YEAR ` of it. 
All common operations like  `= > < ` can be used in the  `FILTER `-part.

As we only want to retrieve the authors that published a novel in 1800 we will use the  `DISTINCT `-Method to get each author once.

<iframe class="" src="https://query.wikidata.org/#%23Locations%20of%20aviation%20accidents%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fcoords%0AWHERE%0A%7B%0A%20%20%20%3Fitem%20wdt%3AP31%20wd%3AQ744913.%20%20%20%20%20%20%23%20item%20is%20an%20instance%20of%20an%20aviation%20accident%0A%20%20%20%3Fitem%20wdt%3AP625%20%3Fcoords.%20%20%20%20%20%20%20%20%23%20item%27s%20coordinates%20are%20collected%20by%20the%20%3Fcoords%20variable%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" style="width:100%;max-width:100%;height:450px" frameborder="0"></iframe>


Example: [Get all authors that published a novel in 1800](https://tinyurl.com/2cfajx6w)

Another example for the `FILTER` would be searching for a substring within a string-Item (like the Label). If you are interested in all authors whose names contain “beau”, you need to retrieve the label of all authors and add the phrase `FILTER(CONTAINS(LCASE(?authorName), "beau"))`.
As the function `CONTAINS` is a String-Matching-Function that is sensible to upper and lower case strings it is important to set the characters in ?authorName to lowercase characters. 


Example: [Get all authors whose name contains “beau”](https://tinyurl.com/2yqdlt4w)

In our graph the labels of authors are structured in `SURNAME` (in upper case) and first name (in lower case). So if you only want to retrieve authors whose surname contains “beau”, you also could replace the FILTER part as follows: FILTER(contains(?authorName, "BEAU")). 
But be careful, you need to know the data in order to get the desired (or if any at all) output.  `FILTER(contains(?authorName, "beau"))`would not give you any result, because the only author whose first name contains “beau” is “SAINT-AULAIRE, Yrieix Beaupoil, marquis de” and here the “B” in “Beaupoil” also is upper case so it is not a match.

If you are interested in other string functions, have a look at the section "Functions on strings" in the [SPARQL Wikibook](https://en.wikibooks.org/wiki/SPARQL/Expressions_and_Functions#Functions_on_strings). 

```
Filter
: FILTERs restrict solutions to those for which the filter expression evaluates to TRUE.

```

[Previous](./limit.html){: .btn-primary} [Next](./optional.html){: .btn-primary}

<!-- {% include links.html %} -->

{% include help.html %}
