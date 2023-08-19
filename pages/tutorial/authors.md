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

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/227vucqe" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe>
                </p>

Via changing the `SELECT` part to `SELECT (count(?authorName) as ?count)` you can get the total count of the authors represented in the graph: [Query to retrieve the count of authors](https://tinyurl.com/2d9h5k2o){:target="\_blank" rel="noopener"}.

You can also get authors with the most publications of novels during 1751-1800 (top 20):

<p><iframe style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/28lvys7q" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms" ></iframe></p>

To get more information on the authors like dates of birth and death or people who influenced them, you can use [federated queries](./federated.html) to query Wikidata.

But first of all, it is important to get an idea of how many of the authors within MiMoTextBase do actually have a mapping with Wikidata: [Query to retrieve the number of authors having a wikidata-match](https://tinyurl.com/2278ch48){:target="\_blank" rel="noopener"}.

To compare how many authors have a mapping with Wikidata and how many don’t, you can run the following query: [Comparison of wikidata matches vs. no matches on authors](https://tinyurl.com/27s3wglf){:target="\_blank" rel="noopener"}

### **A timeline**

As described in the section above, federated queries allow querying several knowledge graphs at once. We can explore federated queries by querying the MiMoText graph and the Wikidata knowledge graph, making use of the Wikidata property date of birth and of the property image which allows us to see the date of birth of the authors in a timeline.

[Timeline of authors, their Wikidata matches and birth dates](https://tinyurl.com/2ygvbqgl){:target="\_blank" rel="noopener"}

<p><img src="images/timeline_authors.PNG" alt="timeline" height="600" width="800"/></p>
<br>
Please note that only the authors of the full text corpus are mapped to Wikidata yet.
<br>
<br>

[Previous](./federated.html){: .btn-primary} [Next](./novels.html){: .btn-primary}

{% include help.html %}
