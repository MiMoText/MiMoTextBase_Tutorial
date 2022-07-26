---
#title: Tutorial
tags: [mimotext_data]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: novels.html
folder: tutorial
toc: false
---

### **Novels**

With the information covered by the Bibliographie du genre romanesque français (Martin, Mylne, and Frautschi 1977) within the MiMoText graph, we can not only query which novels were published between 1751 and 1800, but dive much deeper into the novels themselves.

Because we are planning on integrating statements from scholarly publications into MiMoTextBase, it is important to add `wdt:P2` (instance of) `wd:Q2` (literary work) to the query to retrieve results concerning only the “novels”.

To get an overview of the narrative perspective the novels are written in, you can use the property `P33` (narrative form) in combination with `COUNT` (don’t forget the group by-operation!). By setting the `#defaultView` to "BarChart", the results will be displayed as a bar plot.

[Query to retrieve the narrative perspective of all novels by count](https://tinyurl.com/23jks3un)

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23%20Query%20to%20retrieve%20the%20narrative%20perspectives%20of%20the%20novels.%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0Aprefix%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0ASELECT%20%28count%28%3FnarrativePerspectiveLabel%29%20as%20%3Fcount%29%20%3FnarrativePerspectiveLabel%20%0AWHERE%0A%7B%0A%20%20%3Fwork%20wdt%3AP33%20%3FnarrativePerspective.%20%23%20work%20%28novel%29%20has%20property%20P33%20%28narrative%20perspective%29%0A%20%20%3FnarrativePerspective%20rdfs%3Alabel%20%3FnarrativePerspectiveLabel.%20%23%20using%20of%20rdfs%3Alabel%20to%20display%20labels%0A%20%20%0A%20%20FILTER%28lang%28%3FnarrativePerspectiveLabel%29%20%3D%20%22en%22%29%20%23%20filter%20is%20neccessary%20to%20display%20only%20one%20occurence.%20Other%20possibilites%20would%20be%20%22en%22%20or%20%22de%22.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2C%20en%22.%20%7D%0A%20%0A%7D%0A%0Agroup%20by%20%3FnarrativePerspectiveLabel%0A%23defaultView%3ABarChart"referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>
                </p>

In order to get the narrative perspective of each novel, you can simply replace the `COUNT`-operation with `?work` (to get the link to the respective novel or `?workLabel` to display the titles of the novels within the results list (or both if you want). (Please note: the value behind a `?` is freely selectable, but it has to stay the same within each query.)

[Query to retrieve the narrative perspective of each novel](https://tinyurl.com/29djnpv6)

By simply replacing `P33` with `P32` you can retrieve the narrative locations of each novel. To get all places referenced in all novels displayed one time, you can add `DISTINCT` in the selection part to group all multiple occurences.

[Query to retrieve the narrative locations in the corpus](https://tinyurl.com/29ozzvfb)

### **The tonality**

Those interested in the tonality of the novels will find an overview of this property per novel here:

[View as treemap](https://tinyurl.com/296vltge)

### **Book formats and publishing**

Those interested in book history will find data on publishing places of first editions and also distribution formats of first editions (property `P26`).

[Query: In which distribution formats were the novels published?](https://tinyurl.com/2dzfqpl8)

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23defaultView%3ABarChart%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASelect%20%20%28str%28SAMPLE%28year%28%3Fdate%29%29%29%20as%20%3Fyear%29%20%28count%28%3Fformat%29%20as%20%3Fcount%29%20%3Fformat%20%0A%20%20%20WHERE%7B%0A%20%20%20%3Fitem%20wdt%3AP26%20%3Fformat.%0A%20%20%20%3Fitem%20wdt%3AP9%20%3Fdate%20.%0A%20%20FILTER%28lang%28%3Fformat%29%20%3D%20%22fr%22%29%0A%23%20FILTER%28lcase%28%3Fformat%29%20%3D%20%2212-in%22%40fr%29%0A%20%20%20%20%20%20Filter%20%28regex%28lcase%28%3Fformat%29%2C%20%22in-%5C%5Cd%2B%5B%5C%5Cs%5C%5CS%5D%22%29%29%0A%20%20%20BIND%28str%28year%28%3Fdate%29%29%20as%20%3Fyear%29%0A%20%20%20SERVICE%20wikibase%3Alabel%20%7Bbd%3AserviceParam%20wikibase%3Alanguage%20%22%7BAUTO_LANGUAGE%7D%22%2C%22fr%22%20.%7D%0A%20%20%7D%0A%0AGROUP%20BY%20%3Fformat%20%3Fyear%20%3Fcount%0A%23having%20%28%3Fcount%3E%202%29%0A"referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>
                </p>

We can observe a diversification of small formats: in-12 and even in-18 and in-24. Smaller book formats enable the reader to read in a clandestine setting, on travels and individually, making their way out of the libraries and reading cabinets (cf. Sacquin n.d.).

<img src="images/rousseau_reading.png" alt="drawing" height="457" width="381"/>

Jean-Jacques Rousseau
Gravure d'Hippolyte Huet d'après un tableau de Joseph Albrier
XVIIIe siècle.        
BnF, Musique, fonds estampes, Rousseau J.-J.    
© Bibliothèque nationale de France


[Previous](./authors.html){: .btn-primary} [Next](./spaces.html){: .btn-primary}
