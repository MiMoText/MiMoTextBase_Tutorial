---
#title: Tutorial
#tags: [mimotext_data]
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: authors.html
folder: tutorial
toc: false
#topnav: topnav
---

### **Authors**

One major focus of the MiMoText graph are the authors who published novels in French during 1751-1800. Based on the _Bibliographie du Genre Romanesque Français_ (Martin, Mylne, and Frautschi 1977), we extracted the authors of French novels whose first publication date lies in between that period, which means we excluded translations (in French) and re-editions.

The following query shows which authors are represented in the MiMoText graph via the property item `occupation` (P11) namely `author` (Q11):

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23%20Query%20to%20retrieve%20all%20authors%20in%20the%20graph%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fauthor%20%3FauthorName%0AWHERE%20%7B%0A%20%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11%20.%20%23%20item%20has%20property%20%22occupation%22%28P11%29%20namely%20%22author%22%28Q11%29.%0A%20%20%20%3Fauthor%20rdfs%3Alabel%20%3FauthorName%20.%20%23%20get%20author%20label%20%28not%20only%20Link%20to%20author%29%0A%20%20%20FILTER%28LANG%28%3FauthorName%29%20%3D%20%22en%22%29%20%23%20other%20options%3A%20%22fr%22%2C%20%22de%22.%20Filter%20is%20needed%20as%20there%20is%20more%20than%20one%20label%20%28language%20dependent%29%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
                </p>

Via changing the `SELECT` part to `SELECT (count(?authorName) as ?count)` you can get the total count of the authors represented in the graph: [Query to retrieve the count of authors](https://tinyurl.com/2dg84acv){:target="\_blank" rel="noopener"}.

You can also get authors with the most publications of novels during 1751-1800 (top 20):

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23%20Query%20to%20retrieve%20authors%20with%20most%20novels%20published%20%28top%2020%29%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3FauthorName%20%28count%20%28%3FauthorName%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%20%20%3Fwork%20wdt%3AP5%20%3Fauthor%20.%20%23%20work%20has%20author.%0A%20%20%20%3Fauthor%20rdfs%3Alabel%20%3FauthorName%20.%20%23%20get%20author%20label%20%28not%20only%20Link%20to%20author%29%0A%20%20%20FILTER%28LANG%28%3FauthorName%29%20%3D%20%22en%22%29%20%23%20other%20options%3A%20%22fr%22%2C%20%22de%22.%20Filter%20is%20needed%20as%20there%20is%20more%20than%20one%20label%20%28language%20dependent%29%0A%20%7D%20%0Agroup%20by%20%3FauthorName%0Aorder%20by%20desc%20%28%3Fcount%29%0Alimit%2020" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms" ></iframe></p>

To get more information on the authors like dates of birth and death or people who influenced them, you can use [federated queries](./federated.html) to query Wikidata.

But first of all, it is important to get an idea of how many of the authors within MiMoTextBase do actually have a mapping with Wikidata: [Query to retrieve the number of authors having a wikidata-match](https://tinyurl.com/22qg7h5l){:target="\_blank" rel="noopener"}.

To compare how many authors have a mapping with Wikidata and how many don’t, you can run the following query: [Comparison of wikidata matches vs. no matches on authors](https://tinyurl.com/2yoduuws){:target="\_blank" rel="noopener"}

### **A timeline**

As described in the section above, federated queries allow querying several knowledge graphs at once. We can explore federated queries by querying the MiMoText graph and the Wikidata knowledge graph, making use of the Wikidata property date of birth and of the property image which allows us to see the date of birth of the authors in a timeline.

[Show all authors in a timeline of birth dates](https://tinyurl.com/28x5ajjy){:target="\_blank" rel="noopener"}

<p><img src="images/timeline_authors.PNG" alt="timeline" height="600" width="800"/></p>
<br>
Please note that only the authors of the full text corpus are mapped to Wikidata yet.
<br>
<br>

[Previous](./federated.html){: .btn-primary} [Next](./novels.html){: .btn-primary}

{% include help.html %}
