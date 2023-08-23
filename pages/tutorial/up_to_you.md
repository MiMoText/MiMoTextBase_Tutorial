---
#title: Tutorial
tags: # add
keywords:
summary:
sidebar: mydoc_sidebar_tutorial
permalink: up_to_you.html
folder: tutorial
toc: false
#topnav: topnav_tut
---

### **Now it is up to you!**

Take this query as a starting point:

[Evolution of "travel" theme in French novels 1750-1800](https://tinyurl.com/2a5ar4zg){:target="\_blank", rel: "noopener noreferrer"}

Open the SPARQL endpoint by clicking on the link above. Now you can try editing the query. Let's take a closer look at line 13:

<code>filter(lcase(?topicLabel) = "travel"@en)</code>

Here you could delete <code>“travel”</code> and type in another theme, for example <code>“melancholia”</code>. Make sure to enter the theme in lower case.

Now hit the “play” button and explore the change over time of the theme of <code>“melancholia”</code> in French novels in the second half of the 18th Century. For a full list of possible thematic concepts run this query:

[All themes in our graph](https://tinyurl.com/28wyuswn){:target="\_blank", rel: "noopener noreferrer"}

<p><iframe  style="width:100%;max-width:100%;height:450px" frameborder="0" allowfullscreen src="https://tinyurl.com/28wyuswn" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups allow-forms"></iframe></p>

You could also try out <code>“sentiment”</code>, <code>“philosophy”</code>, <code>“education”</code>, for example.

[Previous](./comparing.html){: .btn-primary}

{% include help.html %}
