---
#title: Tutorial
#tags: # add
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: comparing.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **Comparing**

Comparing is a central methodological and epistemological paradigm in the (digital) humanities. The MiMoText graph enables us to compare different parameters in the queries.

For instance, we can compare different narrative perspectives and narrative places:

[Where are epistolary novels set?](https://tinyurl.com/2ccjscbs){:target="\_blank", rel: "noopener noreferrer"}

[Where are heterodiegetic novels set?](https://tinyurl.com/2yfvdp23){:target="\_blank", rel: "noopener noreferrer"}

There are some dominant narrative places (France/England/rural area) and differences between the types of novels: epistolary novels are more often set in Switzerland than heterodiegetic novels, whereas heterodiegetic novels are more often set in imaginary places than epistolary novels.

Moreover, as we use different sources of data, we can have a look at thematic statements referenced by `Topic Modeling` (`Q21`) vs. thematic statements referenced by the `bibliographic metadata` (`Q1`).

For example, concerning the narrative locations, we have two complementary sources: bibliographic metadata and named entity recognition of location entities mining the full texts.

![didero](./images/comparing_nar_loc.png)

<cite>Fig.: Narrative locations in Diderots novel _La Religieuse_ (1796), referenced by different sources.</cite>

If you are interested in comparing the different sources (`Q21` for `Topic Modeling` / `Q1` for _`Bibliographie du genre romanesque français`_ / `Q27` for `NER_novels locations`) of RDF statements within the graph, for example concerning thematic statements, the following queries might be a starting point:

[Most common topics in novels, referenced by topic modeling](https://tinyurl.com/2arvhawr){:target="\_blank", rel: "noopener noreferrer"}

[Most common topics in novels, referenced by the Bibliographie du genre romanesque français, 1751-1800 (Martin, Mylne, und Frautschi 1977)](https://tinyurl.com/29ztc9dw){:target="\_blank", rel: "noopener noreferrer"}

Or, we could also ask for statements referenced by both sources at the same time:

[Statements on consistent topics in novels from both sources: Topic Modeling & bibliographic metadata](https://tinyurl.com/2y4e7rbq){:target="\_blank", rel: "noopener noreferrer"}

![biblio](./images/comparing_biblio.png)

For _Émile ou de l’éducation_ (1762), the topic modeling algorithm and the metadata agree, that the novel is about education or for _Claire d’Albe_ (1799) both sources agree that the novel is about sentiment.

[Previous](./change_over_time.html){: .btn-primary} [Next](./up_to_you.html){: .btn-primary}

{% include help.html %}
