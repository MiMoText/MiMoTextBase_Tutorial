---
#title: Tutorial
#tags: [mimotext_data]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: secondary_literature.html
folder: tutorial
toc: false
#topnav: topnav
---

## **UNDER CONSTRUCTION**

### **Queries about secondary literature, references and quotations**

Next to the statements mined from literary works and the bibliographic metadata, the team annotated statements about the authors and the literary works in different secondary publications. These were then lodified and imported in the MiMoTextBase.
This allowed us to enrich the graph with different statements:
- for author-items: `topic interest` (P47)  
- for literary work-items: `about` (P36)

Using reification the statements themselves have statements:
- `stated in` (P18): reference to the scholarly work
- `quotation` (P42): String containing the quotation where the statement was derived from

In order to retrieve references using SPARQL, it is necessary to extend the `PREFIXES` declared. A more detailed explanation of the prefixes can be found elsewhere, eg. [here for wikidata](https://www.mediawiki.org/wiki/Wikibase/Indexing/RDF_Dump_Format#Prefixes_used){:target="\_blank", rel: "noopener noreferrer"}. For more information about references, see [here](https://en.wikibooks.org/wiki/SPARQL/WIKIDATA_Qualifiers,_References_and_Ranks#){:target="\_blank", rel: "noopener noreferrer"}.

Not only do we want to use the prefix `mmdt:` for the properties to point directly to the value, but we want to address the whole statement group.

With the following query, we can display all Labels of the secondary literature used in the MiMoTextBase. Klick [here](https://tinyurl.com/yo6arcms){:target="\_blank", rel: "noopener noreferrer"} to open it in a new tab.
<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/yo6arcms" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>

Please note: As we are addressing only the reference within this query, it would be possible to combine this lines
```sparql
?statement prov:wasDerivedFrom ?refnode.
?refnode mmpr:P18 ?ref.
```
using `property paths` into one line:
```sparql
?statement prov:wasDerivedFrom/mmpr:P18 ?ref.
```

With the [next query](https://tinyurl.com/yo4emnax){:target="\_blank", rel: "noopener noreferrer"}, we want to explore all items, either literary work-items or author-items, where any reference by a scholarly literature was made.
<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/yo4emnax" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>

How many references by scholarly works does each author has? Ordered in descending order.
<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/ytog3ku7" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>

If you want to ask the same for the literary works, just change line 11 from
```sparql
?item mmdt:P11 mmd:Q11. # item has occupation author
```
to 
```sparql
?item mmdt:P2 mmd:Q2. # item is instance of literary work
```
or click [here](https://tinyurl.com/yu3tunlp){:target="\_blank", rel: "noopener noreferrer"}.



[Previous](./visualizations.html){: .btn-primary} [Next](./change_over_time.html){: .btn-primary}

{% include help.html %}
