---
#title: Help
keywords:
summary:
sidebar: mydoc_sidebar
permalink: help.html
folder: mydoc
toc: false
---

### **FAQs**

> MiMoTextBase: [data.mimotext.uni-trier.de](http://data.mimotext.uni-trier.de/wiki/Main_Page)

> SPARQL-Endpoint: [query.mimotext.uni-trier.de](http://query.mimotext.uni-trier.de/)

> MiMoText project site: [mimotext.uni-trier.de](https://mimotext.uni-trier.de)

### **_Am I right here or Where do I start?_**

If you are new to SPARQL, you can begin the (short) Tutorial [LINK], which will give you an overview of how to write basic queries based on examples in the MiMoTextBase. It’s supposed to help newbies to get an introduction on SPARQL, but it cannot give you a deep knowledge of SPARQL; maybe the helpful resources [LINK] can help you with that.
If you are interested in the MiMoTextBase and its content on the authors, novels, spaces or themes of the French novel in 1751-1800 with already some SPARQL knowledge, you can have a look here: [LINKS].
Within [GOING FURTHER] there are some queries on the data containing overviews of items like dates of publication or themes changing over time and comparing the different sources of the data in the MiMoTextBase together with some interpretation on the outcome which could show the potential of initial questions on further research.
I f you want more detailed information about the structure and the aims of our tutorial, you can find it in the introduction of the tutorial [LINK].Information on the infrastructure and the models behind the MiMoTextBase, you can find here [LINK zu “Our sources and modeling approaches”]

### **_I have no results. What can I do?_**

Having no results in the result table can have different reasons. A simple solution is to check whether you have written the variables the same in the SELECT and the WHERE part of the query.
Another reason could be being too specific in the query. Not all items in the MiMoTextBase contain all information on all properties due to its sources. So it can be helpful to add the OPTIONAL function on some of the properties in your query [LINK zu OPTIONAL].

### **_Error message: Bad aggregate_**

If you run into this error message, you probably have to group items. In the example below, we use the count function, but did not add GROUP BY.

### **_Query to retrieve count of published works per author_**

The solution is easy: We have to aggregate ?authorName by grouping. We now can order the results descending via order by desc(?count) and set a limit of 20 to get the top 20.

[Query to retrieve authors with most novels published (top 20)](https://tinyurl.com/2fp2hf7d)

### **_I have too many results. What can I do?_**

Sometimes you can get many results on a query which can slow down the result generation or impair the readability of some visualizations. In those cases you could add the LIMIT-operation [LINK] to only get the TOP x-items or the HAVING COUNT-operation [LINK] if you want only results that lie above a certain threshold. If some of the items appear more often in the results than they should, make sure that you filter all labels for one language (FR, EN, DE) separately as the graph is multilingual and the output will represent all languages within the graph [LINK zu The simplest query].

### **_How to find the right item / right property?_**

You might look for the right identifier concerning the properties, novels, authors, themes or locations. The simplest way is to go on data.mimotext.uni-trier.de and use the search function typing in the label (for example “London” or “about” or “philosophy”). The numerical identifier of the property or the item is visible in the URL or behind the name of the item or the property:

For your ease, we also provide you here with lists of themes, locations and properties and their numerical identifier in the knowledge graph.

#### List of properties

Query: [This is a list of all the properties used in this graph](https://tinyurl.com/2pjvgwle)

#### List of themes

For a list of all thematic concepts in the graph, see this query which lists all thematic concepts and their Q-Identifier, ordered by occurence.

Query: [Show all themes with corresponding Q-Identifier and occurence in the graph]()

- <http://zora.uni-trier.de:11000/entity/Q3063> sentimentalism 401
- <http://zora.uni-trier.de:11000/entity/Q3065> sentiment 357
- <http://zora.uni-trier.de:11000/entity/Q3104> travel 247
- <http://zora.uni-trier.de:11000/entity/Q2757> love 208
- <http://zora.uni-trier.de:11000/entity/Q2958> unhappiness 187
- <http://zora.uni-trier.de:11000/entity/Q2899> gallantary 160
- <http://zora.uni-trier.de:11000/entity/Q3018>
  philosophy
  78
- <http://zora.uni-trier.de:11000/entity/Q3098>
  virtue
  78
- <http://zora.uni-trier.de:11000/entity/Q2887>
  family
  73
- <http://zora.uni-trier.de:11000/entity/Q3027>
  politics
  61
- <http://zora.uni-trier.de:11000/entity/Q2964>
  melancholia
  54
- <http://zora.uni-trier.de:11000/entity/Q3128>
  court
  54
- <http://zora.uni-trier.de:11000/entity/Q2970>
  miracle
  48
- <http://zora.uni-trier.de:11000/entity/Q2785>
  happiness
  35
- <http://zora.uni-trier.de:11000/entity/Q2985>
  nature
  34
- <http://zora.uni-trier.de:11000/entity/Q2949>
  libertinism
  34
- <http://zora.uni-trier.de:11000/entity/Q2876>
  eroticism
  32
- <http://zora.uni-trier.de:11000/entity/Q2863>
  education
  30
- <http://zora.uni-trier.de:11000/entity/Q2978>
  morality
  30
- <http://zora.uni-trier.de:11000/entity/Q2932>
  interaction
  28
- <http://zora.uni-trier.de:11000/entity/Q3004>
  passion
  26
- <http://zora.uni-trier.de:11000/entity/Q2845>
  mourning
  25
- <http://zora.uni-trier.de:11000/entity/Q2992>
  night
  25
- <http://zora.uni-trier.de:11000/entity/Q2771>
  attraction
  24
- <http://zora.uni-trier.de:11000/entity/Q3013>
  personality
  24
- <http://zora.uni-trier.de:11000/entity/Q2910>
  war
  23
- <http://zora.uni-trier.de:11000/entity/Q2979>
  death
  18
- <http://zora.uni-trier.de:11000/entity/Q2798>
  chivalry
  17
- <http://zora.uni-trier.de:11000/entity/Q2986>
  shipwrecking
  17
- <http://zora.uni-trier.de:11000/entity/Q2825>
  correspondence
  13
- <http://zora.uni-trier.de:11000/entity/Q2829>
  crime
  12
- <http://zora.uni-trier.de:11000/entity/Q3043>
  romantic relationship
  11
- <http://zora.uni-trier.de:11000/entity/Q3048>
  revolution
  11

#### List of locations

For a list of all narrative places in the graph, see this query which lists all narrative places and their Q-Identifier, ordered by occurence.

Query: [Show all narrative locations with corresponding Q-Identifier & occurrence](https://tinyurl.com/29w2ulyv)

Q-Identifier
place
count

- <http://zora.uni-trier.de:11000/entity/Q3508>
  Paris
  367
- <http://zora.uni-trier.de:11000/entity/Q3179>
  France
  246
- <http://zora.uni-trier.de:11000/entity/Q3223>
  rural area
  219
- <http://zora.uni-trier.de:11000/entity/Q3255>
  England
  133
- <http://zora.uni-trier.de:11000/entity/Q3350>
  Italy
  49
- <http://zora.uni-trier.de:11000/entity/Q3495>
  London
  39
- <http://zora.uni-trier.de:11000/entity/Q3305>
  Spain
  35
- <http://zora.uni-trier.de:11000/entity/Q3367>
  Greece
  29
- <http://zora.uni-trier.de:11000/entity/Q3233>
  Germany
  29
- <http://zora.uni-trier.de:11000/entity/Q3355>
  imaginary place
  25
- <http://zora.uni-trier.de:11000/entity/Q3267>
  Rome
  22
- <http://zora.uni-trier.de:11000/entity/Q3213>
  Constantinople
  20
- <http://zora.uni-trier.de:11000/entity/Q3356>
  Switzerland
  19
- <http://zora.uni-trier.de:11000/entity/Q3492>
  Americas
  18
- <http://zora.uni-trier.de:11000/entity/Q3345>
  Persis
  17
- <http://zora.uni-trier.de:11000/entity/Q3457>
  India
  15
- <http://zora.uni-trier.de:11000/entity/Q3481>
  Egypte
  15
- <http://zora.uni-trier.de:11000/entity/Q3384>
  Lyon
  14
- <http://zora.uni-trier.de:11000/entity/Q3201>
  Normandy
  12
- <http://zora.uni-trier.de:11000/entity/Q3130>
  fictional country
  12
- <http://zora.uni-trier.de:11000/entity/Q3385>
  Europe
  12

These queries list themes or locations ordered by occurence. We would recommend items or properties which have a certain number of connections in the graph, in order to get good results (with enough data points in it).

### **The query is very slow or there is a time out. What can I do?**

There are several possibilities for a slowdown or a time out of your query. It could be that the quantity of results is very high, so you might limit the results to check if the syntax of the query is ok. This is done by using the LIMIT parameter [LINK]. The `LIMIT` tells the algorithm where to stop, so if you insert for example `LIMIT 100` at the end of your query, it will stop after 100 results. This can be helpful for debugging.
Parameters which potentially slow down the query are `DISTINCT` or `ORDER BY`. A strategy might be to comment them out to see if these slow down your query.
