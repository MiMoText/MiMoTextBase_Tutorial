---
#title: Tutorial
#tags: # add
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: change_over_time.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **Change Over Time**

The MiMoText graph contains information on first publication dates of all of the work items (novels) referenced by the _Bibliographie du Genre Romanesque Français_ (Martin, Mylne, and Frautschi 1977). This enables us to retrieve change over time, optionally combining it with other properties.

Let’s start with a simple example: The following query shows the `first publication date` (`P9`) of all the novel items in the corpus.

[Query to retrieve the first publication dates of all French novels 1750-1800](https://tinyurl.com/25n6xwyr){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23%20Query%20to%20retrieve%20the%20first%20publication%20dates%20of%20all%20French%20novels%201750-1800%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%28str%28SAMPLE%28year%28%3Fdate%29%29%29%20as%20%3Fyear%29%20%28COUNT%28%2a%29%20AS%20%3Fcount%29%0AWHERE%20%7B%0A%20%20%20%3Fitem%20wdt%3AP9%20%3Fdate%20.%0A%7D%0AGROUP%20BY%20%3Fdate%0AORDER%20BY%20DESC%28%3Fcount%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe></p>

We can observe an [augmentation of novel production](https://tinyurl.com/2xonar28){:target="\_blank", rel: "noopener noreferrer"} in the later decades, a finding also backed by secondary literature (see for example Franco Moretti on the rise of the novel: Moretti 2005: 9).

Furthermore, we can also combine information on first publication dates and a certain topic. Let's see how the thematic concept "travel" evolved over time:

[Query to retrieve the theme 'travel' over time in French novels 1751-1800](https://tinyurl.com/2429zfwe){:target="\_blank", rel: "noopener noreferrer"}

We could also have a look at all the themes in the corpus and their evolution over time, optionally filtering out themes with no or only one occurrence per year (?countyear > 1).

[Query to retrieve themes in French novels 1751-1800](https://tinyurl.com/2y4jhf42){:target="\_blank", rel: "noopener noreferrer"}
![themes_french](images/change_themes_french.png)

Please note that these include topics generated by Topic Modeling, so some topic labels may seem odd to you (topics with low semantic coherence are labeled using the three top topic words). If you are interested in how we generated the topics, see our paper on Topic Modeling French novels 1750-1800 (Röttgermann and Klee accepted).

We can also query for narrative form in a diachronic perspective:

[How have narrative forms changed over time?](https://tinyurl.com/2azx95vl){:target="\_blank", rel: "noopener noreferrer"}
![nar_form](images/change_nar_forms.png)

[Previous](./themes.html){: .btn-primary} [Next](./comparing.html){: .btn-primary}

{% include help.html %}
