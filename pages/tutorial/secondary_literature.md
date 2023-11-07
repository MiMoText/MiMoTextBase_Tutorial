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


For each of the secondary literature-items within the MiMoTextBase count how many references / quotations they have in total (please note: there can be the same quotations if it is connected to more than one work, author or statement).
See query [here](https://tinyurl.com/ywokvzfl){:target="\_blank", rel: "noopener noreferrer"}
<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/ywokvzfl" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>


The following queries focus on the statements of the individual works. 

The first [query](https://tinyurl.com/yncdql3v){:target="\_blank", rel: "noopener noreferrer"} retrieves novels and the counts of their associated `P36 (about)`-statements that are referenced at least three times by any scholarly work. 
<p><iframe  style="width:100%;max-width:100%;height:600px" frameborder="0" allowfullscreen src="https://tinyurl.com/yncdql3v" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>

In the [next query](https://tinyurl.com/ywzbjx74){:target="\_blank", rel: "noopener noreferrer"}, the works will be narrowed down to those that deal with the theme of "libertinism". In addition, we ask for the literature on which the topic is referenced and the corresponding quotations.
<p><iframe  style="width:100%;max-width:100%;height:600px" frameborder="0" allowfullscreen src="https://tinyurl.com/ywzbjx74" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>


Next we are going to connect both the `topic interest`-statements of the author items and the `about`-statements of the novels. With this [query](https://tinyurl.com/ylem7eol){:target="\_blank", rel: "noopener noreferrer"} we retrieve all topic interests of one author and show the novels were these topic interests are represented. Also show the respective quotations for the `about` statements of the novels as well as the quotations for that statement found in `topic interest` within the author-statements. Show the quotations only if they are not the same within the `topic interest` and the `about`-statement.
<p><iframe  style="width:100%;max-width:100%;height:800px" frameborder="0" allowfullscreen src="https://tinyurl.com/ylem7eol" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>

If you want to bind the references and the quotations additionally, so that all quotations for `topic interest` and all quotations of `about` are shown as one string each, check this [query](https://query.mimotext.uni-trier.de/#PREFIX%20mmdref%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Freference%2F%3E%0APREFIX%20mmpq%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fqualifier%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20mmps%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fstatement%2F%3E%0Aprefix%20mmpr%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Freference%2F%3E%0Aprefix%20mmp%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2F%3E%0A%0A%23%20get%20all%20topic%20interests%20of%20one%20authors%20and%20show%20books%20where%20that%20is%20represented%0A%23%20and%20respective%20quotations%20for%20novel%20is%20about%20and%20author%20has%20topic%20interest%0A%0ASELECT%20DISTINCT%20%3Fauthor%20%3FauthorLabel%20%3FaboutLabel%0A%28GROUP_CONCAT%28DISTINCT%20%3Fauthorstmt%3B%20separator%3D%22%3B%20%22%29%20as%20%3FauthorstmtAll%29%20%0A%28GROUP_CONCAT%28DISTINCT%20%3Fnovelstmt%3B%20separator%3D%22%3B%20%22%29%20as%20%3FnovelstmtAll%29%0A%28GROUP_CONCAT%28DISTINCT%20%3FitemLabel%3B%20separator%3D%22%3B%20%22%29%20as%20%3Ffound_in_items%29%20%0A%0AWHERE%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2.%20%23item%20is%20instance%20of%20literary%20work%0A%20%20%3Fitem%20rdfs%3Alabel%20%3FitemLabel.%0A%20%20FILTER%28LANG%28%3FitemLabel%29%20%3D%20%22en%22%29.%0A%20%20%3Fitem%20mmdt%3AP5%20%3Fauthor.%20%23%20item%20has%20an%20author%0A%20%20%0A%20%20%3Fitem%20mmp%3AP36%20%3Fstatement.%0A%20%20%3Fstatement%20mmps%3AP36%20%3Fabout.%0A%20%20%3Fstatement%20prov%3AwasDerivedFrom%20%3Fref.%0A%20%20%3Fref%20mmpr%3AP18%20%3Frefnode.%0A%20%20%3Frefnode%20rdfs%3Alabel%20%3FrefnodeLabel.%0A%20%20FILTER%28LANG%28%3FrefnodeLabel%29%20%3D%22en%22%29.%0A%20%20OPTIONAL%7B%3Fref%20mmpr%3AP42%20%3FquotationNovel.%7D%0A%20%20%0A%20%20%3Fauthor%20mmp%3AP47%20%3FstatementAuthor.%20%23%20the%20author%20has%20the%20same%20topic%20interest%20as%20the%20topics%20of%20the%20novels.%0A%20%20%3FstatementAuthor%20mmps%3AP47%20%3Fabout.%0A%20%20%3FstatementAuthor%20prov%3AwasDerivedFrom%20%3FrefTopicInterest.%0A%20%20%3FrefTopicInterest%20mmpr%3AP18%20%3FrefnodeTopicInterest.%0A%20%20%3FrefnodeTopicInterest%20rdfs%3Alabel%20%3FrefnodeTopicInterestLabel.%0A%20%20FILTER%28LANG%28%3FrefnodeTopicInterestLabel%29%20%3D%20%22en%22%29.%0A%20%20OPTIONAL%7B%0A%20%20%3FrefTopicInterest%20mmpr%3AP42%20%3FquotationAuthor.%20%7D%0A%20%20%0A%20%20FILTER%28%3FquotationNovel%20%21%3D%20%3FquotationAuthor%29.%0A%20%20%0A%20%20BIND%28CONCAT%28%3FrefnodeLabel%2C%20%22%20quotes%3A%20%22%2C%20%3FquotationNovel%29%20as%20%3Fnovelstmt%29.%0A%20%20BIND%28CONCAT%28%3FrefnodeTopicInterestLabel%2C%20%22%20quotes%3A%20%22%2C%20%3FquotationAuthor%29%20as%20%3Fauthorstmt%29.%0A%0A%20%20%0A%20%20%0A%20%20%3Frefnode%20mmdt%3AP2%20mmd%3AQ3.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D%0AGROUP%20BY%20%3Fauthor%20%3FauthorLabel%20%3FaboutLabel%0AORDER%20by%20%3FauthorLabel){:target="\_blank", rel: "noopener noreferrer"}.


As the quotation statements are of the datatype "string", it is possible to create a string search within the quotations.
For example if you want to search for the mention of "Voltaire" in either `about`-statements of the novels or the `topic interest`-statements of the authors, you can add the line `FILTER(CONTAINS(?quotation, "Voltaire"))`, see query [here](https://tinyurl.com/ynjvux6e){:target="\_blank", rel: "noopener noreferrer"}.
<p><iframe  style="width:100%;max-width:100%;height:650px" frameborder="0" allowfullscreen src="https://tinyurl.com/ynjvux6e" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
</p>




[Previous](./visualizations.html){: .btn-primary} [Next](./change_over_time.html){: .btn-primary}

{% include help.html %}
