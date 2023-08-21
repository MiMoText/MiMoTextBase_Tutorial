---
#title: Tutorial
#tags: [mimotext_data]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: novels.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **Novels**

With the information covered by the _Bibliographie du Genre Romanesque Français_ (Martin, Mylne, and Frautschi 1977) within the MiMoText graph, we can not only query which novels were published between 1751 and 1800, but dive much deeper into the novels themselves.

Because we are planning on integrating statements from scholarly publications into MiMoTextBase, it is important to add `wdt:P2` (instance of) `wd:Q2` (literary work) to the query to retrieve results concerning only the “novels”.

To get an overview of the narrative perspective the novels are written in, you can use the property `P33` (narrative form) in combination with `COUNT` (don’t forget the group by-operation!). By setting the `#defaultView` to "BarChart", the results will be displayed as a bar plot.

[Query to retrieve the narrative perspective of all novels by count](https://tinyurl.com/2d5xo7re){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/2d5xo7re" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
                </p>

In order to get the narrative perspective of each novel, you can simply replace the `COUNT`-operation with `?work` (to get the link to the respective novel or `?workLabel` to display the titles of the novels within the results list (or both if you want). (Please note: the value behind a `?` is freely selectable, but it has to stay the same within each query.)

[Query to retrieve the narrative perspective of each novel](https://tinyurl.com/22u6fukj){:target="\_blank", rel: "noopener noreferrer"}

By simply replacing `P33` with `P32` you can retrieve the narrative locations of each novel. To get all places referenced in all novels displayed one time, you can add `DISTINCT` in the selection part to group all multiple occurences.

[Query to retrieve the narrative locations in the corpus](https://tinyurl.com/22q7d8nb){:target="\_blank", rel: "noopener noreferrer"}

### **Tone**

Those interested in the tone of the novels will find an overview of this property per novel here:

[View as treemap](https://tinyurl.com/2cavgm5q){:target="\_blank", rel: "noopener noreferrer"}

### **Book formats and publishing**

Those interested in book history will find data on publishing places of first editions and also distribution formats of first editions (property `P26`).

[Query: In which distribution formats were the novels published?](https://tinyurl.com/2dea7qjy){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe style="width: 80vw; height: 50vh; border: none;" src="https://tinyurl.com/2dea7qjy" ></iframe></p>

We can observe a diversification of small formats: in-12 and even in-18 and in-24. Smaller book formats enable the reader to read in a clandestine setting, on travels and individually, making their way out of the libraries and reading cabinets (cf. Sacquin n.d.).

<img src="images/rousseau_reading.png" alt="drawing" height="457" width="381"/>

<!---
<img src="images/rousseau_reading.png" style="height:35%; width:35%" />
-->

<p><b>Jean-Jacques Rousseau</b><br>
Gravure d'Hippolyte Huet d'après un tableau de Joseph Albrier<br>
XVIIIe siècle.<br>
BnF, Musique, fonds estampes, Rousseau J.-J.<br>    
© Bibliothèque nationale de France</p>
<br>

[Previous](./authors.html){: .btn-primary} [Next](./spaces.html){: .btn-primary}

{% include help.html %}
