---
#title: Tutorial
tags: # add
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: up_to_you.html
folder: tutorial
toc: false
---

### **Now it is up to you**



Take this query as a starting point:

[Query to retrieve the theme 'travel' over time in French novels 1750-1800](https://tinyurl.com/y6r5qf69)

Open the [SPARQL endpoint](http://query.mimotext.uni-trier.de) by clicking on the link above. Now you can try out changing the query. We have a closer look at line 11:

 <code>filter(lcase(?topicLabel) = "travel"@en)</code>

 Here you could erase  <code>“travel”</code> and type in another theme, for example <code>“melancholia”</code>. Make sure the theme you enter is in lower case.

Now hit the “Play”-Button and you can explore the change over time of the theme of <code>“melancholia”</code> in French novels in the second half of the 18th Century.  For a full list of possible thematic concepts see this query.

 [Query to retrieve the themes in our graph](https://tinyurl.com/2osfhnd6)

 You could try out for example <code>“sentiment”</code>, <code>“philosophy”</code>, <code>“education”</code> and so on.  

[Previous](./comparing.html){: .btn-primary}
