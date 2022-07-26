---
#title: Tutorial
tags: # add
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: up_to_you.html
folder: tutorial
toc: false
topnav: topnav_tut
---

### **Now it is up to you**



Take this query as a starting point:

[Query to retrieve the theme 'travel' over time in French novels 1750-1800](https://tinyurl.com/2cab44h4){:target="\_blank", rel: "noopener noreferrer"}

Open the [SPARQL endpoint](http://query.mimotext.uni-trier.de) by clicking on the link above. Now you can try out changing the query. We have a closer look at line 11:

 <code>filter(lcase(?topicLabel) = "travel"@en)</code>

 Here you could erase  <code>“travel”</code> and type in another theme, for example <code>“melancholia”</code>. Make sure the theme you enter is in lower case.

Now hit the “Play”-Button and you can explore the change over time of the theme of <code>“melancholia”</code> in French novels in the second half of the 18th Century.  For a full list of possible thematic concepts see this query.

 [Query to retrieve the themes in our graph](https://tinyurl.com/25cjjpom){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://query.mimotext.uni-trier.de/#%23%20Query%20to%20retrieve%20the%20theme%20%27travel%27%20over%20time%20in%20French%20novels%201750-1800%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASelect%20%3FthemeLabel%0A%20%20%20WHERE%7B%0A%20%20%20%3Fitem%20wdt%3AP36%20%3Ftheme.%0A%20%20%20%3Ftheme%20rdfs%3Alabel%20%3FthemeLabel%20.%0A%20%20%20FILTER%28lang%28%3FthemeLabel%29%20%3D%20%22en%22%29%0A%20%20%20BIND%28str%28year%28%3Fdate%29%29%20as%20%3Fyear%29%0A%20%20%20SERVICE%20wikibase%3Alabel%20%7Bbd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%7D%0A%20%20%7D%0A%0AGROUP%20BY%20%3FthemeLabel%20" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe></p>

 You could try out for example <code>“sentiment”</code>, <code>“philosophy”</code>, <code>“education”</code> and so on.  

[Previous](./comparing.html){: .btn-primary}

{% include help.html %}