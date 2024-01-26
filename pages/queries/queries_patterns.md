---
#title: Queries used in different publications
#keywords:
#summary: Queries used in different publications
sidebar: false
permalink: queries_patterns.html
folder: queries
toc: False
---
#### Patterns in modeling and querying a knowledge graph for literary history

Here you can find the queries that are shown in the paper "Patterns in modeling and querying a knowledge graph for literary history" (in print).


Query 0, Fig 3: [Authors (here: ‘Voltaire’) and works (here: ‘Le Micromégas’) in subject position shown as Graph](https://purl.org/mmt/patterns/query0){:target="_blank"}
<!-- 
as Tiny URL: http://tinyurl.com/yq96bxrz
as FUll URL: https://query.mimotext.uni-trier.de/#PREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0A%0A%23defaultView%3AGraph%0ASELECT%20%3Fitem1%20%3Fitem1Label%20%3Fitem2%20%3Fitem2Label%20%3FedgeLabel%20%0AWITH%20%7B%0A%20%20SELECT%20%3Fitem1%20WHERE%20%7B%0A%20%20%20%20VALUES%20%3Fitem1%20%7B%20mmd%3AQ1011%20mmd%3AQ981%20mmd%3AQ2%20mmd%3AQ3039%20mmd%3AQ38%20mmd%3AQ3126%20mmd%3AQ3335%20mmd%3AQ3259%20mmd%3AQ3906%7D%0A%20%20%7D%0A%7D%20AS%20%25item1%0AWITH%20%7B%0A%20%20SELECT%20%28%3Fitem1%20AS%20%3Fitem2%29%20WHERE%20%7B%0A%20%20%20%20INCLUDE%20%25item1.%0A%20%20%7D%0A%7D%20AS%20%25item2%0AWHERE%20%7B%0A%20%20INCLUDE%20%25item1.%0A%20%20INCLUDE%20%25item2.%0A%20%20%3Fitem1%20%3Fwdt%20%3Fitem2.%0A%20%20%3Fedge%20wikibase%3AdirectClaim%20%3Fwdt%3B%0A%20%20%20%20%20%20%20%20a%20wikibase%3AProperty.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D
-->
```sparql
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

#defaultView:Graph
SELECT ?item1 ?item1Label ?item2 ?item2Label ?edgeLabel 
WITH {
  SELECT ?item1 WHERE {
    VALUES ?item1 { mmd:Q1011 mmd:Q981 mmd:Q2 mmd:Q3039 mmd:Q38 mmd:Q3126 mmd:Q3335 mmd:Q3259 mmd:Q3906}
  }
} AS %item1
WITH {
  SELECT (?item1 AS ?item2) WHERE {
    INCLUDE %item1.
  }
} AS %item2
WHERE {
  INCLUDE %item1.
  INCLUDE %item2.
  ?item1 ?wdt ?item2.
  ?edge wikibase:directClaim ?wdt;
        a wikibase:Property.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}

```

Query 1: [Count of novels, authors, thematic concepts and spatial concepts](https://purl.org/mmt/patterns/query1){:target="_blank"}

```sparql
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIx mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>
SELECT ?subject (COUNT(?o) as ?counts)
WHERE {
  VALUES (?p ?o) { (mmdt:P2 mmd:Q2) (mmdt:P11 mmd:Q11) (mmdt:P2 mmd:Q20) (mmdt:P2 mmd:Q26) }
  ?item ?p ?o.
  BIND(IF(?o = mmd:Q2, "novels", 
          IF(?o = mmd:Q11, "authors",
             IF(?o = mmd:Q20, "thematic concepts",
               IF(?o = mmd:Q26, "spatial concepts", "none")
           )
          )
         ) as ?subject)
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}GROUP BY ?o ?subject
```

#### 3.1 Basic triple patterns and their combinations
Query 2: [Narrative locations of literary works](https://purl.org/mmt/patterns/query2){:target="_blank"}

<!-- 
- as [Tiny-URL](https://tinyurl.com/26emfn9h){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3A%20Narrative%20locations%20of%20literary%20works%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3FnarrativeLoc%20%3FnarrativeLocLabel%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP32%20%3FnarrativeLoc.%20%23item%20has%20narrative%20location%28s%29%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%20%20%7D%0A){:target="_blank"}
-->

```sparql
#title: Narrative locations of literary works
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>

SELECT ?item ?itemLabel ?narrativeLoc ?narrativeLocLabel
WHERE {
  ?item mmdt:P2 mmd:Q2; #item is instance of literary work
        mmdt:P32 ?narrativeLoc. #item has narrative location(s)
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
  }
```


Query 3: [Novels set in 'imaginary place'](https://purl.org/mmt/patterns/query3){:target="_blank"}

<!-- 
- as [Tiny-URL](https://tinyurl.com/2bl9u6hc){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3A%20Novels%20set%20in%20%27imaginary%20place%27%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP32%20mmd%3AQ3371.%20%23%20item%20has%20narrative%20location%20%27imaginary%20place%27%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%20%20%0A%0A%7D%0A){:target="_blank"}
-->
```sparql
#title: Novels set in 'imaginary place'
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>

SELECT DISTINCT ?item ?itemLabel
WHERE {
  ?item mmdt:P2 mmd:Q2; #item is instance of literary work
        mmdt:P32 mmd:Q3371. # item has narrative location 'imaginary place'
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }  

}
```

Query 4: [Novels that have theme 'miracle'](https://purl.org/mmt/patterns/query4){:target="_blank"}

<!-- 
- as [Tiny-URL](https://tinyurl.com/22fy4d7x){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3ANovels%20that%20have%20theme%20%27miracle%27%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP36%20mmd%3AQ2990.%20%23%20item%20is%20about%20miracle%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%20%20%0A%0A%7D%0A){:target="_blank"}
-->

```sparql
#title:Novels that have theme 'miracle'
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>

SELECT DISTINCT ?item ?itemLabel
WHERE {
  ?item mmdt:P2 mmd:Q2; #item is instance of literary work
        mmdt:P36 mmd:Q2990. # item is about miracle
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }  

}
```

Query 5: [Novels published in Paris between 1780 and 1790 that have theme 'philosophy'](https://purl.org/mmt/patterns/query5){:target="_blank"} 

<!-- 
- as [Tiny-URL](https://tinyurl.com/26z8dbc6){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3ANovels%20published%20in%20Paris%20between%201780%20and%201790%20that%20have%20theme%20%27philosophy%27%20%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fyear%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP10%20mmd%3AQ3521%3B%20%23item%20was%20published%20in%20Paris%0A%20%20%20%20%20%20%20%20mmdt%3AP36%20mmd%3AQ3039%3B%20%23item%20is%20about%20philosophy%0A%20%20%20%20%20%20%20%20mmdt%3AP9%20%3Fdate.%20%23item%20has%20publication%20date.%0A%0A%20%20FILTER%28%3Fdate%20%3E%3D%20%221780%22%5E%5Exsd%3AdateTime%20%26%26%20%3Fdate%20%3C%3D%20%221790%22%5E%5Exsd%3AdateTime%29.%0A%20%20BIND%28YEAR%28%3Fdate%29%20as%20%3Fyear%29.%0A%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%20%20%0A%0A%7D%0A){:target="_blank"}
-->

```sparql
#title:Novels published in Paris between 1780 and 1790 that have theme 'philosophy' 
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>

SELECT ?item ?itemLabel ?year
WHERE {
  ?item mmdt:P2 mmd:Q2; #item is instance of literary work
        mmdt:P10 mmd:Q3521; #item was published in Paris
        mmdt:P36 mmd:Q3039; #item is about philosophy
        mmdt:P9 ?date. #item has publication date.

  FILTER(?date >= "1780"^^xsd:dateTime && ?date <= "1790"^^xsd:dateTime).
  BIND(YEAR(?date) as ?year).

  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }  

}
```

#### 3.2 Further analysis and exploration

Query 6: [Query to retrieve some data about the MiMoTextBase such as Authors, Novels, publicationyears, tonality etc.](https://purl.org/mmt/patterns/query6){:target="_blank"}

<!--
- as [Tiny-URL](https://tinyurl.com/2bpl7qa6){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AQuery%20to%20retrieve%20some%20data%20about%20the%20MiMoTextBase%20such%20as%20Authors%2C%20Novels%2C%20publicationyears%2C%20tonality%20etc.%0Aprefix%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fbgrf%20%3Fitem%20%3Fauthorlabel%20%3FitemLabel%20%3Fyear%20%3Fnarrpers%20%3Ftonality%20%3Fpages%20%3Fdist_format%20%3Fnormalized%20WHERE%20%7B%0A%20%3Fitem%20mmdt%3AP5%20%3Fauthor%3B%20%23%20who%20is%20the%20author%3F%0A%20%20%20%20%20%20%20mmdt%3AP4%20%3Ftitle%3B%20%23%20what%20is%20the%20title%3F%0A%20%20%20%20%20%20%20mmdt%3AP22%20%3Fbgrf%3B%20%20%23%20what%20is%20the%20identifier%20in%20the%20bibliographic%20metadata%3F%0A%20%20%20%20%20%20%20mmdt%3AP9%20%3Fdate%3B%20%23%20what%20is%20the%20publication%20date%3F%0A%20OPTIONAL%20%7B%20%3Fitem%20mmdt%3AP27%20%3Fnarrpers%7D%20%0A%20OPTIONAL%20%7B%20%3Fitem%20mmdt%3AP31%20%3Ftonality%7D%0A%20OPTIONAL%20%7B%20%3Fitem%20mmdt%3AP25%20%3Fpages%7D%0A%20OPTIONAL%20%7B%20%3Fitem%20mmdt%3AP26%20%3Fdist_format%7D%0A%20BIND%28YEAR%28%3Fdate%29%20as%20%3Fyear%29.%0A%20BIND%28if%28bound%28%3Fnarrpers%29%2C%20%3Fnarrpers%2C%20%22unbekannt%22%29%20as%20%3Fnormalized%29%0A%20%3Fauthor%20rdfs%3Alabel%20%3Fauthorlabel.%0A%20FILTER%28LANG%28%3Fauthorlabel%29%20%3D%20%22en%22%29%0A%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2C%20fr%22.%20%7D%0A%7D%20ORDER%20BY%20%3Fyear){:target="_blank"}

-->

```sparql
#title:Query to retrieve some data about the MiMoTextBase such as Authors, Novels, publicationyears, tonality etc.
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT ?bgrf ?item ?itemLabel ?authorLabel ?year ?narrpers ?tonality ?pages ?dist_format WHERE {
  ?item mmdt:P2 mmd:Q2. #item is instance of literary work
  OPTIONAL { ?item mmdt:P5 ?author} #item has author (optionally)
  OPTIONAL { ?item mmdt:P4 ?title} #item has title (optionally)
  OPTIONAL { ?item mmdt:P22 ?bgrf}  #item has identifier in the bibliographic metadata? (optionally)
  OPTIONAL { ?item mmdt:P9 ?date} #item has publication date (optionally)
  OPTIONAL { ?item mmdt:P27 ?narrpers} #item has narrative form (optionally)
  OPTIONAL { ?item mmdt:P31 ?tonality} #item has tonality (optionally)
  OPTIONAL { ?item mmdt:P25 ?pages} #item has page information (optionally)
  OPTIONAL { ?item mmdt:P26 ?dist_format} #item has distribution format (optionally)
  BIND(YEAR(?date) as ?year)
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE], fr". }
} ORDER BY ?year
```

Query 7, Fig. 5: [Themes occuring in novels of intention satire](https://purl.org/mmt/patterns/query7){:target="_blank"}

<!-- 
- as [Tiny-URL](https://tinyurl.com/2bye4vtg){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AThemes%20occuring%20in%20novels%20of%20intention%20satire%0A%23defaultView%3ABubbleChart%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0ASELECT%20%3Ftheme%20%28SAMPLE%28%3FthemeLabel%29%20as%20%3Fname%29%20%20%28count%28%2a%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP39%20mmd%3AQ3906%3B%20%23novel%20has%20intention%20satire%0A%20%20%20%20%20%20%20%20mmdt%3AP36%20%3Ftheme.%20%23novel%20has%20theme%0A%20%20%20%20%20%20%3Ftheme%20rdfs%3Alabel%20%3FthemeLabel%20.%0A%20%20%20%20%20%20FILTER%20%28LANG%28%3FthemeLabel%29%20%3D%20%22en%22%29%20.%0A%7D%0AGROUP%20BY%20%3Ftheme%0AORDER%20BY%20DESC%28%3Fcount%29%0A%0A){:target="_blank"}

-->

```sparql
#title:Themes occuring in novels of intention satire
#defaultView:BubbleChart
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>
SELECT ?theme (SAMPLE(?themeLabel) as ?name)  (count(*) as ?count)
WHERE {
  ?item mmdt:P2 mmd:Q2; # item is instance of literary work
        mmdt:P39 mmd:Q3906; #novel has intention satire
        mmdt:P36 ?theme. #novel has theme
      ?theme rdfs:label ?themeLabel .
      FILTER (LANG(?themeLabel) = "en") .
}
GROUP BY ?theme
ORDER BY DESC(?count)
```

Query 8: [Ratio of the theme 'nature' over time](https://purl.org/mmt/patterns/query8){:target="_blank"}

<!-- 

- as [Tiny-URL](https://tinyurl.com/24l4ptg7){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3ARatio%20of%20the%20theme%20%27nature%27%20over%20time%0A%23%20count%20of%20%27nature%27%20%28countNature%29%20as%20a%20novel%20theme%20in%20relation%20to%20the%20number%20of%20novels%20published%20per%20year%20%28countAll%29%3B%20ratio%2C%20as%20novel%20production%20is%20rising%20strongly%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0ASELECT%20%3Fdate%20%3FcountNature%20%3FcountAll%20%28%3FcountNature%20%2F%20%3FcountAll%20AS%20%3Frel%29%20WHERE%20%7B%0A%20%20%7B%0A%09SELECT%20%3Fdate%20%28COUNT%28%2a%29%20AS%20%3FcountNature%29%20WHERE%20%7B%0A%20%20%09%3Fitem%20mmdt%3AP9%20%3Fdate%3B%0A%20%20%20%20%20%20mmdt%3AP36%20%3Ftopic.%0A%20%20%09%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel.%0A%20%20%09FILTER%28%28LANG%28%3FtopicLabel%29%29%20%3D%20%22en%22%29%0A%20%20%09FILTER%28%28LCASE%28%3FtopicLabel%29%29%20%3D%20%22nature%22%40en%29%0A%09%7D%0A%09GROUP%20BY%20%3Fdate%0A%20%20%7D%0A%20%20%7B%0A%09SELECT%20%3Fdate%20%28COUNT%28%2a%29%20AS%20%3FcountAll%29%20WHERE%20%7B%0A%20%20%09%3Fitem%20mmdt%3AP9%20%3Fdate%3B%0A%20%20%20%20%09mmdt%3AP36%20%3Ftopic.%0A%20%20%09%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel.%0A%20%20%09FILTER%28%28LANG%28%3FtopicLabel%29%29%20%3D%20%22en%22%29%0A%09%7D%0A%09GROUP%20BY%20%3Fdate%0A%20%20%7D%0A%7D%0A){:target="_blank"}

-->

```sparql
#defaultView:BarChart
#title:Ratio of the theme 'nature' over time
#count of 'nature' (countNature) as a novel theme in relation to the number of novels published per year (countAll); ratio, as novel production is rising strongly
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>
SELECT ?date (?countNature / ?countAll AS ?rel)  ?countNature ?countAll  WHERE {
  {
	SELECT ?date (COUNT(*) AS ?countNature) WHERE {
  	?item mmdt:P9 ?date;
          mmdt:P36 mmd:Q3005.
    BIND(YEAR(?date) as ?year)
	}
	GROUP BY ?date
  }
  {
	SELECT ?date (COUNT(*) AS ?countAll) WHERE {
  	?item mmdt:P9 ?date;
    	  mmdt:P36 ?topic.
	}
	GROUP BY ?date
  }
}
```

Query 9: [Thematic concepts of novels referenced by ‘Topic Modeling’](https://purl.org/mmt/patterns/query9){:target="_blank"}

<!-- 

- as [Tiny-URL](https://tinyurl.com/2774mnpz){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AThematic%20concepts%20of%20novels%20referenced%20by%20%E2%80%98Topic%20Modeling%E2%80%99%0A%23defaultView%3ABubbleChart%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0APREFIX%20mmpr%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Freference%2F%3E%0APREFIX%20mmps%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fstatement%2F%3E%0APREFIX%20prov%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fprov%23%3E%0A%0ASELECT%20%3FthemeLabel%20%28COUNT%28%2a%29%20AS%20%3Fcount%29%20WHERE%20%7B%0A%20%20%3Fstatement%20mmps%3AP36%20%3Ftheme%3B%0A%09prov%3AwasDerivedFrom%20%3Frefnode.%0A%20%20%3Frefnode%20mmpr%3AP18%20mmd%3AQ21.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D%0AGROUP%20BY%20%3FthemeLabel%0A){:target="_blank"}

-->

```sparql
#title:Thematic concepts of novels referenced by ‘Topic Modeling’
#defaultView:BubbleChart
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>
PREFIX mmpr:<http://data.mimotext.uni-trier.de/prop/reference/>
PREFIX mmps:<http://data.mimotext.uni-trier.de/prop/statement/>
PREFIX prov: <http://www.w3.org/ns/prov#>

SELECT ?themeLabel (COUNT(*) AS ?count) WHERE {
  ?statement mmps:P36 ?theme;
	prov:wasDerivedFrom ?refnode.
  ?refnode mmpr:P18 mmd:Q21.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
GROUP BY ?themeLabel
```

Query 10, Fig. 6: [Thematic statements referenced by ‘topic modeling’ and the bibliography](https://purl.org/mmt/patterns/query10){:target="_blank"}

<!-- 

- as [Tiny-URL](https://tinyurl.com/2dgkv4j3){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/index.html#%23title%3AThematic%20statements%20referenced%20by%20%E2%80%98topic%20modeling%E2%80%99%20and%20the%20bibliography%0A%23Statements%20on%20consistent%20topics%20in%20novels%20from%20both%20sources%3A%20Topic%20Modeling%20%26%20bibliographic%20metadata%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0APREFIX%20mmps%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fstatement%2F%3E%0APREFIX%20mmpr%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Freference%2F%3E%0APREFIX%20mmp%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2F%3E%0ASELECT%20%3Fnovel%20%3FnovelLabel%20%3FtopicLabel%20%3FBGRF_plot_theme%0AWHERE%0A%7B%20%20%20%0A%20%20%20%20%3Fnovel%20mmp%3AP36%20%3Fstatement.%0A%20%20%20%20%3Fstatement%20mmps%3AP36%20%3Ftopic%20.%0A%20%20%20%20%3Fstatement%20prov%3AwasDerivedFrom%20%3Frefnode.%20%23statement%20has%20a%20reference%0A%20%20%20%20%3Frefnode%20mmpr%3AP18%20mmd%3AQ21.%20%20%23reference%20statement%20uses%20%27P18%27%3D%27stated%20in%27%20topic%20modeling%0A%20%20%0A%20%20%20%20%3Fstatement%20prov%3AwasDerivedFrom%20%3FrefnodeB.%0A%20%20%20%20%3FrefnodeB%20mmpr%3AP18%20mmd%3AQ1%20.%23reference%20statement%20uses%20%27P18%27%3D%27stated%20in%27%20bibliographie%0A%20%20%20%0A%20%20%20%20%3Fnovel%20mmdt%3AP30%20%3FBGRF_plot_theme.%20%23statement%20in%20the%20BGRF%20about%20the%20plot%20theme.%0A%20%20%20%20%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D){:target="_blank"}

-->

```sparql
#title:Thematic statements derived from ‘topic modeling’ and the bibliography
#Statements on consistent topics in novels from both sources: Topic Modeling & bibliographic metadata
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/> 
PREFIX mmps:<http://data.mimotext.uni-trier.de/prop/statement/>
PREFIX mmpr: <http://data.mimotext.uni-trier.de/prop/reference/>
PREFIX mmp: <http://data.mimotext.uni-trier.de/prop/>

SELECT ?novel ?novelLabel ?topicLabel ?BGRF_plot_theme WHERE
{   
    ?novel mmp:P36 ?statement.
    ?statement mmps:P36 ?topic.
    ?statement prov:wasDerivedFrom/mmpr:P18 mmd:Q21. #reference statement uses 'P18'='stated in' topic modeling
    ?statement prov:wasDerivedFrom/mmpr:P18 mmd:Q1. #reference statement uses 'P18'='stated in' bibliographie  
    ?novel mmdt:P30 ?BGRF_plot_theme. #statement in the BGRF about the plot theme.
    SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```


Query 11: [Overview over controlled vocabularies](https://purl.org/mmt/patterns/query11){:target="_blank"}

<!-- 

- as [Tiny-URL](https://tinyurl.com/26zkbn9j){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AOverview%20over%20controlled%20vocabularies%0A%23%20Query%20to%20retrieve%20the%20different%20controlled%20vocabularies%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fvoc%20%3FvocLabel%20%28COUNT%28%3FvocLabel%29%20as%20%3Fcount%29%20%28COUNT%28%3Fwikimatch%29%20as%20%3Fwikimatch%29%0AWHERE%20%7B%0A%20%20%20%3Fitem%20mmdt%3AP37%20%3Fvoc.%0A%20%20%20%3Fvoc%20mmdt%3AP2%2Fmmdt%3AP1%20mmd%3AQ17.%0A%20%20%20OPTIONAL%7B%0A%20%20%20%20%20values%20%3Fwiki%20%7Bmmdt%3AP13%20mmdt%3AP16%7D%0A%20%20%20%20%20%3Fitem%20%3Fwiki%20%3Fwikimatch%7D%0A%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3Fvoc%20%3FvocLabel%0AORDER%20BY%20DESC%28%3Fcount%29%0A%20%20){:target="_blank"}

-->

```sparql
#title:Overview over controlled vocabularies
# Query to retrieve the different controlled vocabularies
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>

SELECT ?voc ?vocLabel (COUNT(?vocLabel) as ?count) (COUNT(?wikimatch) as ?wikimatch)
WHERE {
   ?item mmdt:P37 ?voc.
   ?voc mmdt:P2/mmdt:P1 mmd:Q17.
   OPTIONAL{
     values ?wiki {mmdt:P13 mmdt:P16}
     ?item ?wiki ?wikimatch}
   SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
  }
GROUP BY ?voc ?vocLabel
ORDER BY DESC(?count)
  
```


Query 12: [Combinations of narrative Form and intention per year](https://purl.org/mimotext/pattern/query12){:target="_blank"}

<!-- 

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23%20get%20combinations%20of%20narrative%20Form%20and%20intention%20per%20year%0A%23defaultView%3ABarChart%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fyear%20%28COUNT%28%2a%29%20as%20%3Fcount%29%20%3FnarrFormTone%0A%20%20WHERE%7B%0A%20%20%20%20%3Fitem%20mmdt%3AP9%20%3Fpublicationdate.%20%23%20get%20publication%20date%0A%20%20%20%20%3Fitem%20mmdt%3AP38%20%3Ftone.%20%23%20get%20intention%0A%20%20%20%20BIND%28str%28YEAR%28%3Fpublicationdate%29%29%20as%20%3Fyear%29.%20%23%20extract%20year%20from%20pubdate%0A%20%20%20%20%3Fitem%20mmdt%3AP33%20%3FnarrForm.%20%23%20get%20narrative%20form%20%20%20%0A%20%20%20%20%3Ftone%20rdfs%3Alabel%20%3FtoneLabel.%0A%20%20%20%20FILTER%28LANG%28%3FtoneLabel%29%20%3D%20%22en%22%29.%0A%20%20%20%20%3FnarrForm%20rdfs%3Alabel%20%3FnarrFormLabel.%0A%20%20%20%20FILTER%28LANG%28%3FnarrFormLabel%29%20%3D%20%22en%22%29.%20%0A%20%20%20%20BIND%28CONCAT%28STR%28%3FnarrFormLabel%29%2C%20%22%20--%20%22%20%2C%20STR%28%3FtoneLabel%29%29%20as%20%3FnarrFormTone%29.%0A%20%20%7D%0AGROUP%20BY%20%3Fyear%20%3FnarrFormTone%0AHAVING%20%28%3Fcount%20%3E%201%29%0AORDER%20BY%20%3Fyear){:target="_blank"}

-->

```sparql
# get combinations of narrative Form and intention per year
#defaultView:BarChart
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/> 

SELECT ?year (COUNT(*) as ?count) ?narrFormTone
  WHERE{
    ?item mmdt:P9 ?publicationdate. # get publication date
    ?item mmdt:P38 ?tone. # get intention
    BIND(str(YEAR(?publicationdate)) as ?year). # extract year from pubdate
    ?item mmdt:P33 ?narrForm. # get narrative form   
    ?tone rdfs:label ?toneLabel.
    FILTER(LANG(?toneLabel) = "en").
    ?narrForm rdfs:label ?narrFormLabel.
    FILTER(LANG(?narrFormLabel) = "en"). 
    BIND(CONCAT(STR(?narrFormLabel), " -- " , STR(?toneLabel)) as ?narrFormTone).
  }
GROUP BY ?year ?narrFormTone
HAVING (?count > 1)
ORDER BY ?year
```



Query 13: [Topic labels in English, French and German using rdfs:label and Filter](https://purl.org/mmt/patterns/query13){:target="_blank"}

<!-- 
- as [FULL-URL](https://query.mimotext.uni-trier.de/#%23title%3ATopic%20labels%20in%20English%2C%20French%20and%20German%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0A%0ASELECT%20DISTINCT%20%3Ftopic%20%3FtopicLabel_EN%20%3FtopicLabel_FR%20%3FtopicLabel_DE%20WHERE%20%7B%0A%20%20%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%0A%20%20%20%20%20%20%20%20mmdt%3AP36%20%3Ftopic.%0A%20%0A%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_EN.%0A%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_FR.%0A%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_DE.%0A%20%20%0A%20%20FILTER%28LANG%28%3FtopicLabel_EN%29%20%3D%20%22en%22%29.%0A%20%20FILTER%28LANG%28%3FtopicLabel_FR%29%20%3D%20%22fr%22%29.%0A%20%20FILTER%28LANG%28%3FtopicLabel_DE%29%20%3D%20%22de%22%29.%0A%0A%7D){:target="_blank"}

--> 


```sparql
#title:Topic labels in English, French and German
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>

SELECT DISTINCT ?topic ?topicLabel_EN ?topicLabel_FR ?topicLabel_DE WHERE {
  
  ?item mmdt:P2 mmd:Q2;
        mmdt:P36 ?topic.
 
  ?topic rdfs:label ?topicLabel_EN.
  ?topic rdfs:label ?topicLabel_FR.
  ?topic rdfs:label ?topicLabel_DE.
  
  FILTER(LANG(?topicLabel_EN) = "en").
  FILTER(LANG(?topicLabel_FR) = "fr").
  FILTER(LANG(?topicLabel_DE) = "de").

}
```
Query 14: [Topic labels in English, French and German using Wikibase Label Service](https://purl.org/mmt/patterns/query14){:target="_blank"}

<!-- 

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3A%20Topic%20labels%20in%20English%2C%20French%20and%20German%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20DISTINCT%20%3Ftopic%20%3FtopicLabel_EN%20%3FtopicLabel_FR%20%3FtopicLabel_DE%0A%20%20%20WHERE%20%7B%0A%20%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%0A%20%20%20%20%20%20%20%20%20mmdt%3AP36%20%3Ftopic.%20%20%0A%20%20%20%20%20%0A%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_EN.%0A%20%20%20%20%20%7D%0A%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22de%22.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_DE.%0A%20%20%20%20%20%7D%20%0A%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22fr%22.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_FR.%0A%20%20%20%20%20%7D%20%0A%20%20%20%0A%20%20%20%7D){:target="_blank"}

-->

```sparql
#title: Topic labels in English, French and German
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>

SELECT DISTINCT ?topic ?topicLabel_EN ?topicLabel_FR ?topicLabel_DE
   WHERE {
   ?item mmdt:P2 mmd:Q2; 
         mmdt:P36 ?topic.  
     
     SERVICE wikibase:label { bd:serviceParam wikibase:language "en".
            ?topic rdfs:label ?topicLabel_EN.
     }
     SERVICE wikibase:label { bd:serviceParam wikibase:language "de".
            ?topic rdfs:label ?topicLabel_DE.
     } 
     SERVICE wikibase:label { bd:serviceParam wikibase:language "fr".
            ?topic rdfs:label ?topicLabel_FR.
     } 
   
   }
```




Query 15: [Labels entered on wikidata-entry 'Voltaire'](https://purl.org/mmt/patterns/query15){:target="_blank"}

<!-- 

- as [Tiny-URL](https://tinyurl.com/23pv9yu7){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/index.html#%23title%3ALabels%20entered%20on%20wikidata-entry%20%27Voltaire%27%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%28LANG%28%3FVoltaireLabels%29%20as%20%3Flang%29%20%3FVoltaireLabels%20%0AWHERE%20%7B%20%0A%20%20%0A%20%20mmd%3AQ981%20mmdt%3AP13%20%3FwikiDataEntity.%20%23%20Voltaire%20has%20a%20wikidata%20match.%0A%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%3FwikiDataEntity%20rdfs%3Alabel%20%3FVoltaireLabels.%0A%20%20%7D%20%20%20%20%20%20%09%20%0A%7D%0AORDER%20BY%20%3Flang){:target="_blank"}

-->

```sparql
#title:Labels entered on wikidata-entry 'Voltaire'
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT (LANG(?VoltaireLabels) as ?lang) ?VoltaireLabels 
WHERE { 
  
  mmd:Q981 mmdt:P13 ?wikiDataEntity. # Voltaire has a wikidata match.

  #Federated Query -> Wikidata
  SERVICE <https://query.wikidata.org/sparql> {
  ?wikiDataEntity rdfs:label ?VoltaireLabels.
  }      	 
}
ORDER BY ?lang
```

#### 3.3 Federated Queries

Query 16, Fig. 9: [Narrative location with geo coordinate locations via federated query](https://purl.org/mmt/patterns/query16){:target="_blank"}

<!-- 
- as [Tiny-URL](https://tinyurl.com/24djgul3){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3ANarrative%20locations%20of%20the%20novels%20on%20a%20map%0A%23defaultView%3AMap%7B%22markercluster%22%3A%22true%22%7D%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3Fnarr_loc%20%3Fnarr_locLabel%20%3FWikiDataEntity%20%3FcoordinateLocation%0AWHERE%20%7B%20%3Fitem%20mmdt%3AP32%20%3Fnarr_loc.%0A%20%20%3Fnarr_loc%20mmdt%3AP13%20%3FWikiDataEntity.%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%09%3FWikiDataEntity%20wdt%3AP625%20%3FcoordinateLocation%0A%20%20%7D%20%20%20%20%20%20%09%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A){:target="_blank"}

-->

```sparql
#title:Narrative locations of the novels on a map
#defaultView:Map{"markercluster":"true"}
PREFIX wd: <http://www.wikidata.org/entity/> #wikidata wd
PREFIX wdt: <http://www.wikidata.org/prop/direct/> #wikidata wdt
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>
SELECT DISTINCT ?item ?itemLabel ?narr_loc ?narr_locLabel ?WikiDataEntity ?coordinateLocation
WHERE { ?item mmdt:P32 ?narr_loc.
  ?narr_loc mmdt:P13 ?WikiDataEntity.
  #Federated Query -> Wikidata
  SERVICE <https://query.wikidata.org/sparql> {
	?WikiDataEntity wdt:P625 ?coordinateLocation
  }      	 
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en" . }
}
```

Query 17: [Alternative Labels of author names via ‘federated’ queries’](https://purl.org/mmt/patterns/query17){:target="_blank"}

<!-- 

- as [Tiny-URL](https://tinyurl.com/22qcoc8m){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AAlternative%20Labels%20of%20author%20names%20via%20%E2%80%98federated%E2%80%99%20queries%E2%80%99%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20DISTINCT%20%3Fauthor%20%3FauthorLabel%20%3FwikidataEntity%20%3Faltname%0AWHERE%20%7B%0A%09%20%3Fitem%20mmdt%3AP5%20%3Fauthor.%0A%20%20%20%20%20%20%3Fauthor%20mmdt%3AP13%20%3FwikidataEntity.%20%20%23exact%20match%0A%20%0A%20%20%20%20%20%20%23Federated%20Query%20-%3E%20Wikidata%0ASERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%09%20%3FwikidataEntity%20skos%3AaltLabel%20%3Faltname%0A%20%20%20%20%20%20%7D%20%20%20%20%20%0A%20%09%09%20%0A%20%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%0A%20%20%20%09%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%0A%20%20%20%20%20%20%7D%0A%7D%0ALIMIT%201000%0A){:target="_blank"}

-->

```sparql
#title:Alternative Labels of author names via ‘federated’ queries’
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT DISTINCT ?author ?authorLabel ?wikidataEntity ?altname
WHERE {
	 ?item mmdt:P5 ?author.
      ?author mmdt:P13 ?wikidataEntity.  #exact match
 
      #Federated Query -> Wikidata
SERVICE <https://query.wikidata.org/sparql> {
   	 ?wikidataEntity skos:altLabel ?altname
      }     
 		 
      SERVICE wikibase:label {
   	 bd:serviceParam wikibase:language "en" .
      }
}
LIMIT 1000
```



Query 18, Fig. 10: [Finding Identifiers on other Knowledge Graphs, for example Bibliothèque nationale de France ID](https://purl.org/mmt/patterns/query18){:target="_blank"}

<!-- 

- as [Tiny-URL](https://tinyurl.com/28jllv6x){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AMiMoText%20novels%20with%20URL%20to%20Biblioth%C3%A8que%20nationale%20de%20France%20%0A%23defaultView%3AImageGrid%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20prefix%20definition%20for%20entity%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20prefix%20definition%20for%20property%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%23mimotext%20prefix%20for%20entity%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%23mimotext%20prefix%20for%20property%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fwikidata%20%3Fbnfurl%20%3Fimage%20%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2.%0A%20%20%3Fitem%20mmdt%3AP13%20%3Fwikidata.%0A%20%20%3Fitem%20rdfs%3Alabel%20%3FitemLabel%20.%0A%20%20FILTER%28lang%28%3FitemLabel%29%20%3D%20%22en%22%29%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3Fwikidata%20wdt%3AP268%20%3Fbnfid.%0A%20%20%20%20OPTIONAL%7B%20%3Fwikidata%20wdt%3AP18%20%3Fimage.%7D%0A%20%20%20OPTIONAL%7B%20wd%3AP268%20wdt%3AP1630%20%3Fformatterurl.%7D%0A%20%20%20BIND%28IRI%28REPLACE%28%3Fbnfid%2C%20%27%5E%28.%2B%29%24%27%2C%20%3Fformatterurl%29%29%20AS%20%3Fbnfurl%29.%0A%20%20%7D%20%20%20%20%20%20%20%20%20%0A%7D%0A%0A){:target="_blank"}

-->

```sparql
#title:MiMoText novels with URL to Bibliothèque nationale de France 
#defaultView:ImageGrid
PREFIX wd: <http://www.wikidata.org/entity/> #wikidata prefix definition for entity
PREFIX wdt: <http://www.wikidata.org/prop/direct/> #wikidata prefix definition for property
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/> #mimotext prefix for entity
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/> #mimotext prefix for property

SELECT ?item ?itemLabel ?wikidata ?bnfurl ?image 
WHERE {
  ?item mmdt:P2 mmd:Q2.
  ?item mmdt:P13 ?wikidata.
  ?item rdfs:label ?itemLabel .
  FILTER(lang(?itemLabel) = "en")
  SERVICE <https://query.wikidata.org/sparql> {
    ?wikidata wdt:P268 ?bnfid.
    OPTIONAL{ ?wikidata wdt:P18 ?image.}
   OPTIONAL{ wd:P268 wdt:P1630 ?formatterurl.}
   BIND(IRI(REPLACE(?bnfid, '^(.+)$', ?formatterurl)) AS ?bnfurl).
  }         
}
```


Query 19, Fig. 11: [Influence networks of authors via ‘federated query’](https://purl.org/mmt/patterns/query19){:target="_blank"}

<!-- 

- as [Tiny-URL](https://tinyurl.com/2aup2tfr){:target="_blank"}

- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AInfluence%20networks%20of%20authors%20via%20%27federated%20query%27%0A%23defaultView%3AGraph%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20entity%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20property%0A%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3FauthorLabel%20%3Finfluencedby%20%3Fimage%20%3Fname%0AWHERE%20%7B%0A%20%20%20%20%20%20%3Fitem%20mmdt%3AP5%20%3Fauthor.%0A%20%20%20%20%20%20%3Fauthor%20mmdt%3AP13%20%3FWikidataEntity.%20%20%23exact%20match%0A%20%20%20%20%20%20%0A%23Federated%20Query%20-%3E%20Wikidata%0A%20%20%20%20%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%09%20%3FWikidataEntity%20wdt%3AP737%2Fwdt%3AP737%20%3Finfluencedby.%0A%20%20%20%20%20%09%20%23%20%3Finfluencedby%20widt%3AP734%20%3Fname.%20%20%0A%20%20%09%09%20OPTIONAL%20%7B%20%20%3Finfluencedby%20wdt%3AP18%20%3Fimage.%7D%0A%20%20%20%20%20%20%7D%20%20%20%20%20%0A%20%09%09%20%0A%20%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%0A%20%20%20%09%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%0A%20%20%20%20%20%20%7D%0A%7D%0A%0A){:target="_blank"}

-->

```sparql
#title:Influence networks of authors via 'federated query'
#defaultView:Graph
PREFIX wd:<http://www.wikidata.org/entity/> #wikidata entity
PREFIX wdt:<http://www.wikidata.org/prop/direct/> #wikidata property

PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT DISTINCT ?item ?itemLabel ?authorLabel ?influencedby ?image ?name
WHERE {
      ?item mmdt:P5 ?author.
      ?author mmdt:P13 ?WikidataEntity.  #exact match
      
#Federated Query -> Wikidata
      SERVICE <https://query.wikidata.org/sparql> {
   	 ?WikidataEntity wdt:P737/wdt:P737 ?influencedby.
     	 # ?influencedby widt:P734 ?name.  
  		 OPTIONAL {  ?influencedby wdt:P18 ?image.}
      }     
 		 
      SERVICE wikibase:label {
   	 bd:serviceParam wikibase:language "en" .
      }
}

```

