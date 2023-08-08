---
title: Queries used in different publications
#keywords:
#summary: Queries used in different publications
sidebar: false
permalink: queries_patterns.html
folder: queries
toc: true
---
### Patterns

#### 2.1 Basic triple patterns and their combinations
Query 1: Narrative locations of literary works
- as [Tiny-URL](https://tinyurl.com/26emfn9h)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3A%20Narrative%20locations%20of%20literary%20works%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3FnarrativeLoc%20%3FnarrativeLocLabel%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP32%20%3FnarrativeLoc.%20%23item%20has%20narrative%20location%28s%29%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%20%20%7D%0A)

Query 2: Novels set in 'imaginary place'

- as [Tiny-URL](https://tinyurl.com/2bl9u6hc)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3A%20Novels%20set%20in%20%27imaginary%20place%27%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP32%20mmd%3AQ3371.%20%23%20item%20has%20narrative%20location%20%27imaginary%20place%27%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%20%20%0A%0A%7D%0A)

Query 3: Novels that have theme 'miracle'

- as [Tiny-URL](https://tinyurl.com/22fy4d7x)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3ANovels%20that%20have%20theme%20%27miracle%27%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP36%20mmd%3AQ2990.%20%23%20item%20is%20about%20miracle%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%20%20%0A%0A%7D%0A)

Query 4: Novels published in Paris between 1780 and 1790 that have theme 'philosophy' 

- as [Tiny-URL](https://tinyurl.com/26z8dbc6)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3ANovels%20published%20in%20Paris%20between%201780%20and%201790%20that%20have%20theme%20%27philosophy%27%20%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fyear%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP10%20mmd%3AQ3521%3B%20%23item%20was%20published%20in%20Paris%0A%20%20%20%20%20%20%20%20mmdt%3AP36%20mmd%3AQ3039%3B%20%23item%20is%20about%20philosophy%0A%20%20%20%20%20%20%20%20mmdt%3AP9%20%3Fdate.%20%23item%20has%20publication%20date.%0A%0A%20%20FILTER%28%3Fdate%20%3E%3D%20%221780%22%5E%5Exsd%3AdateTime%20%26%26%20%3Fdate%20%3C%3D%20%221790%22%5E%5Exsd%3AdateTime%29.%0A%20%20BIND%28YEAR%28%3Fdate%29%20as%20%3Fyear%29.%0A%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%20%20%0A%0A%7D%0A)

Query: Query to retrieve some data about the MiMoTextBase such as Authors, Novels, publicationyears, tonality etc.

- as [Tiny-URL](https://tinyurl.com/2bpl7qa6)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AQuery%20to%20retrieve%20some%20data%20about%20the%20MiMoTextBase%20such%20as%20Authors%2C%20Novels%2C%20publicationyears%2C%20tonality%20etc.%0Aprefix%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fbgrf%20%3Fitem%20%3Fauthorlabel%20%3FitemLabel%20%3Fyear%20%3Fnarrpers%20%3Ftonality%20%3Fpages%20%3Fdist_format%20%3Fnormalized%20WHERE%20%7B%0A%20%3Fitem%20mmdt%3AP5%20%3Fauthor%3B%20%23%20who%20is%20the%20author%3F%0A%20%20%20%20%20%20%20mmdt%3AP4%20%3Ftitle%3B%20%23%20what%20is%20the%20title%3F%0A%20%20%20%20%20%20%20mmdt%3AP22%20%3Fbgrf%3B%20%20%23%20what%20is%20the%20identifier%20in%20the%20bibliographic%20metadata%3F%0A%20%20%20%20%20%20%20mmdt%3AP9%20%3Fdate%3B%20%23%20what%20is%20the%20publication%20date%3F%0A%20OPTIONAL%20%7B%20%3Fitem%20mmdt%3AP27%20%3Fnarrpers%7D%20%0A%20OPTIONAL%20%7B%20%3Fitem%20mmdt%3AP31%20%3Ftonality%7D%0A%20OPTIONAL%20%7B%20%3Fitem%20mmdt%3AP25%20%3Fpages%7D%0A%20OPTIONAL%20%7B%20%3Fitem%20mmdt%3AP26%20%3Fdist_format%7D%0A%20BIND%28YEAR%28%3Fdate%29%20as%20%3Fyear%29.%0A%20BIND%28if%28bound%28%3Fnarrpers%29%2C%20%3Fnarrpers%2C%20%22unbekannt%22%29%20as%20%3Fnormalized%29%0A%20%3Fauthor%20rdfs%3Alabel%20%3Fauthorlabel.%0A%20FILTER%28LANG%28%3Fauthorlabel%29%20%3D%20%22en%22%29%0A%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2C%20fr%22.%20%7D%0A%7D%20ORDER%20BY%20%3Fyear)

Query 5 / Fig. 7: 13 Most frequent themes per novel 
[alt]!!
- as [Tiny-URL](https://tinyurl.com/23lx8qxg)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3A13%20Most%20frequent%20themes%20per%20novel%0A%23defaultView%3ABubbleChart%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0ASELECT%20%3Ftheme%20%28sample%28%3FthemeLabel%29%20as%20%3Fname%29%20%28count%28%2a%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%20%20%20%20%20%3Fitem%20mmdt%3AP36%20%3Ftheme%20.%20%23themes%20per%20novel%0A%20%20%20%20%20%20%3Ftheme%20rdfs%3Alabel%20%3FthemeLabel%20.%0A%20%20%20%20%20%20FILTER%20%28LANG%28%3FthemeLabel%29%20%3D%20%22en%22%29%20.%0A%7D%0AGROUP%20BY%20%3Ftheme%0AORDER%20BY%20DESC%28%3Fcount%29%0ALIMIT%2013%20%2313%20most%20common%20themes%0A)

Query 5 / Fig. 7 [neu]: Themes occuring in novels of intention satire

- as [Tiny-URL](https://tinyurl.com/25v4f8wb)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AThemes%20occuring%20in%20novels%20of%20intention%20satire%0A%23defaultView%3ABubbleChart%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0ASELECT%20%3FthemeLabel%20%28SAMPLE%28%3FthemeLabel%29%20as%20%3Ftheme%29%20%20%28count%28%2a%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20mmdt%3AP39%20mmd%3AQ3906%3B%20%23novel%20has%20intention%20satire%0A%20%20%20%20%20%20%20%20mmdt%3AP36%20%3Ftheme.%20%23novel%20has%20theme%0A%20%20%20%20%20%20%3Ftheme%20rdfs%3Alabel%20%3FthemeLabel%20.%0A%20%20%20%20%20%20FILTER%20%28LANG%28%3FthemeLabel%29%20%3D%20%22en%22%29%20.%0A%7D%0AGROUP%20BY%20%3FthemeLabel%0AORDER%20BY%20DESC%28%3Fcount%29%0A%0A)


Query 6: Ratio of the theme 'nature' over time

- as [Tiny-URL](https://tinyurl.com/24l4ptg7)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3ARatio%20of%20the%20theme%20%27nature%27%20over%20time%0A%23%20count%20of%20%27nature%27%20%28countNature%29%20as%20a%20novel%20theme%20in%20relation%20to%20the%20number%20of%20novels%20published%20per%20year%20%28countAll%29%3B%20ratio%2C%20as%20novel%20production%20is%20rising%20strongly%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0ASELECT%20%3Fdate%20%3FcountNature%20%3FcountAll%20%28%3FcountNature%20%2F%20%3FcountAll%20AS%20%3Frel%29%20WHERE%20%7B%0A%20%20%7B%0A%09SELECT%20%3Fdate%20%28COUNT%28%2a%29%20AS%20%3FcountNature%29%20WHERE%20%7B%0A%20%20%09%3Fitem%20mmdt%3AP9%20%3Fdate%3B%0A%20%20%20%20%20%20mmdt%3AP36%20%3Ftopic.%0A%20%20%09%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel.%0A%20%20%09FILTER%28%28LANG%28%3FtopicLabel%29%29%20%3D%20%22en%22%29%0A%20%20%09FILTER%28%28LCASE%28%3FtopicLabel%29%29%20%3D%20%22nature%22%40en%29%0A%09%7D%0A%09GROUP%20BY%20%3Fdate%0A%20%20%7D%0A%20%20%7B%0A%09SELECT%20%3Fdate%20%28COUNT%28%2a%29%20AS%20%3FcountAll%29%20WHERE%20%7B%0A%20%20%09%3Fitem%20mmdt%3AP9%20%3Fdate%3B%0A%20%20%20%20%09mmdt%3AP36%20%3Ftopic.%0A%20%20%09%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel.%0A%20%20%09FILTER%28%28LANG%28%3FtopicLabel%29%29%20%3D%20%22en%22%29%0A%09%7D%0A%09GROUP%20BY%20%3Fdate%0A%20%20%7D%0A%7D%0A)

Query 7: Thematic concepts of novels referenced by ‘Topic Modeling’

- as [Tiny-URL](https://tinyurl.com/2774mnpz)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AThematic%20concepts%20of%20novels%20referenced%20by%20%E2%80%98Topic%20Modeling%E2%80%99%0A%23defaultView%3ABubbleChart%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0APREFIX%20mmpr%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Freference%2F%3E%0APREFIX%20mmps%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fstatement%2F%3E%0APREFIX%20prov%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fprov%23%3E%0A%0ASELECT%20%3FthemeLabel%20%28COUNT%28%2a%29%20AS%20%3Fcount%29%20WHERE%20%7B%0A%20%20%3Fstatement%20mmps%3AP36%20%3Ftheme%3B%0A%09prov%3AwasDerivedFrom%20%3Frefnode.%0A%20%20%3Frefnode%20mmpr%3AP18%20mmd%3AQ21.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D%0AGROUP%20BY%20%3FthemeLabel%0A)


Query 8a: Thematic statements referenced by ‘topic modeling’ and the bibliography (fig. 8)

- as [Tiny-URL](https://tinyurl.com/29jd9hy6)
- as [Full-URL](https://query.mimotext.uni-trier.de/index.html#%23title%3AThematic%20statements%20referenced%20by%20%E2%80%98topic%20modeling%E2%80%99%20and%20the%20bibliography%0A%23Statements%20on%20consistent%20topics%20in%20novels%20from%20both%20sources%3A%20Topic%20Modeling%20%26%20bibliographic%20metadata%0Aprefix%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0Aprefix%20mmps%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fstatement%2F%3E%0Aprefix%20mmpr%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Freference%2F%3E%0APREFIX%20mmp%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2F%3E%0A%0ASELECT%20%20%20%3FnovelLabel%20%3FtopicLabel%20%3Frefnode%0AWHERE%0A%7B%20%20%20%0A%20%20%20%20%3Fnovel%20mmp%3AP36%20%3Fstatement.%0A%20%20%20%20%3Fstatement%20mmps%3AP36%20%3Ftopic%20.%0A%20%20%20%20%3Fstatement%20prov%3AwasDerivedFrom%20%3Frefnode.%20%23statement%20has%20a%20reference%0A%20%20%20%20%3Frefnode%20mmpr%3AP18%20mmd%3AQ21.%20%20%23reference%20statement%20uses%20%27P18%27%3D%27stated%20in%27%20topic%20modeling%0A%20%20%0A%20%20%20%20%3Fstatement%20prov%3AwasDerivedFrom%20%3FrefnodeB.%0A%20%20%20%20%3FrefnodeB%20mmpr%3AP18%20mmd%3AQ1%20.%23reference%20statement%20uses%20%27P18%27%3D%27stated%20in%27%20bibliographie%0A%20%20%20%20%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D)

Query 8b (Vorschlag ohne Ref-Knoten, sondern mit topicLabel und BGRF-plot_theme):

- as [Tiny-URL](https://tinyurl.com/2dgkv4j3)
- as [Full-URL](https://query.mimotext.uni-trier.de/index.html#%23title%3AThematic%20statements%20referenced%20by%20%E2%80%98topic%20modeling%E2%80%99%20and%20the%20bibliography%0A%23Statements%20on%20consistent%20topics%20in%20novels%20from%20both%20sources%3A%20Topic%20Modeling%20%26%20bibliographic%20metadata%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0APREFIX%20mmps%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fstatement%2F%3E%0APREFIX%20mmpr%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Freference%2F%3E%0APREFIX%20mmp%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2F%3E%0ASELECT%20%3Fnovel%20%3FnovelLabel%20%3FtopicLabel%20%3FBGRF_plot_theme%0AWHERE%0A%7B%20%20%20%0A%20%20%20%20%3Fnovel%20mmp%3AP36%20%3Fstatement.%0A%20%20%20%20%3Fstatement%20mmps%3AP36%20%3Ftopic%20.%0A%20%20%20%20%3Fstatement%20prov%3AwasDerivedFrom%20%3Frefnode.%20%23statement%20has%20a%20reference%0A%20%20%20%20%3Frefnode%20mmpr%3AP18%20mmd%3AQ21.%20%20%23reference%20statement%20uses%20%27P18%27%3D%27stated%20in%27%20topic%20modeling%0A%20%20%0A%20%20%20%20%3Fstatement%20prov%3AwasDerivedFrom%20%3FrefnodeB.%0A%20%20%20%20%3FrefnodeB%20mmpr%3AP18%20mmd%3AQ1%20.%23reference%20statement%20uses%20%27P18%27%3D%27stated%20in%27%20bibliographie%0A%20%20%20%0A%20%20%20%20%3Fnovel%20mmdt%3AP30%20%3FBGRF_plot_theme.%20%23statement%20in%20the%20BGRF%20about%20the%20plot%20theme.%0A%20%20%20%20%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D)


Query ### : Overview over controlled vocabularies

- as [Tiny-URL](https://tinyurl.com/26zkbn9j)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3AOverview%20over%20controlled%20vocabularies%0A%23%20Query%20to%20retrieve%20the%20different%20controlled%20vocabularies%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fvoc%20%3FvocLabel%20%28COUNT%28%3FvocLabel%29%20as%20%3Fcount%29%20%28COUNT%28%3Fwikimatch%29%20as%20%3Fwikimatch%29%0AWHERE%20%7B%0A%20%20%20%3Fitem%20mmdt%3AP37%20%3Fvoc.%0A%20%20%20%3Fvoc%20mmdt%3AP2%2Fmmdt%3AP1%20mmd%3AQ17.%0A%20%20%20OPTIONAL%7B%0A%20%20%20%20%20values%20%3Fwiki%20%7Bmmdt%3AP13%20mmdt%3AP16%7D%0A%20%20%20%20%20%3Fitem%20%3Fwiki%20%3Fwikimatch%7D%0A%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3Fvoc%20%3FvocLabel%0AORDER%20BY%20DESC%28%3Fcount%29%0A%20%20)


Query ###: Combinations of narrative Form and intention per year

- as [Full-URL](https://query.mimotext.uni-trier.de/index.html#%23title%3ACombinations%20of%20narrative%20Form%20and%20intention%20per%20year%0A%23defaultView%3ABarChart%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fyear%20%28COUNT%28%2a%29%20as%20%3Fcount%29%20%3FnarrFormTone%0A%20%20WHERE%7B%0A%20%20%20%20%3Fitem%20mmdt%3AP9%20%3Fpublicationdate.%20%23%20get%20publication%20date%0A%20%20%20%20%3Fitem%20mmdt%3AP38%20%3Ftone.%20%23%20get%20tokencount%0A%20%20%20%20BIND%28str%28YEAR%28%3Fpublicationdate%29%29%20as%20%3Fyear%29.%20%23%20extract%20year%20from%20pubdate%0A%20%20%20%20%3Fitem%20mmdt%3AP33%20%3FnarrForm.%20%23%20get%20narrative%20form%0A%20%20%20%20%0A%20%20%20%20%3Ftone%20rdfs%3Alabel%20%3FtoneLabel.%0A%20%20%20%20FILTER%28LANG%28%3FtoneLabel%29%20%3D%20%22en%22%29.%0A%20%20%20%20%3FnarrForm%20rdfs%3Alabel%20%3F%20%3FnarrFormLabel.%0A%20%20%20%20FILTER%28LANG%28%3FnarrFormLabel%29%20%3D%20%22en%22%29.%20%0A%20%20%20%20%0A%20%20%20%20BIND%28CONCAT%28STR%28%3FnarrFormLabel%29%2C%20%22%20--%20%22%20%2C%20STR%28%3FtoneLabel%29%20%29%20as%20%3FnarrFormTone%29.%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3FnarrFormLabel%20%3Fyear%20%3FtoneLabel%20%3FnarrFormTone%0AHAVING%20%28COUNT%28%2a%29%20%3E%201%29%0AORDER%20BY%20%3Fyear)


Queries ### : Topic labels in English, French and German

1. 
- as [Tiny-URL](https://tinyurl.com/2avufdfo)
- as [FULL-URL](https://query.mimotext.uni-trier.de/#%23title%3ATopic%20labels%20in%20English%2C%20French%20and%20German%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0A%0ASELECT%20DISTINCT%20%3Ftopic%20%3FtopicLabel_EN%20%3FtopicLabel_FR%20%3FtopicLabel_DE%20WHERE%20%7B%0A%20%20%0A%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%0A%20%20%20%20%20%20%20%20mmdt%3AP36%20%3Ftopic.%0A%20%0A%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_EN.%0A%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_FR.%0A%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_DE.%0A%20%20%0A%20%20FILTER%28LANG%28%3FtopicLabel_EN%29%20%3D%20%22en%22%29.%0A%20%20FILTER%28LANG%28%3FtopicLabel_FR%29%20%3D%20%22fr%22%29.%0A%20%20FILTER%28LANG%28%3FtopicLabel_DE%29%20%3D%20%22de%22%29.%0A%0A%7D)

2. 
- as [Tiny-URL](https://tinyurl.com/23vmyjo6)
- as [Full-URL](https://query.mimotext.uni-trier.de/#%23title%3A%20Topic%20labels%20in%20English%2C%20French%20and%20German%0APREFIX%20mmd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20DISTINCT%20%3Ftopic%20%3FtopicLabel_EN%20%3FtopicLabel_FR%20%3FtopicLabel_DE%0A%20%20%20WHERE%20%7B%0A%20%20%20%3Fitem%20mmdt%3AP2%20mmd%3AQ2%3B%20%0A%20%20%20%20%20%20%20%20%20mmdt%3AP36%20%3Ftopic.%20%20%0A%20%20%20%20%20%0A%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_EN.%0A%20%20%20%20%20%7D%0A%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22de%22.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_DE.%0A%20%20%20%20%20%7D%20%0A%20%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22fr%22.%0A%20%20%20%20%20%20%20%20%20%20%20%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel_FR.%0A%20%20%20%20%20%7D%20%0A%20%20%20%0A%20%20%20%7D)


Query ###: Labels entered on wikidata-entry 'Voltaire'

- as [Tiny-URL](https://tinyurl.com/23pv9yu7)
- as [Full-URL](https://query.mimotext.uni-trier.de/index.html#%23title%3ALabels%20entered%20on%20wikidata-entry%20%27Voltaire%27%0APREFIX%20mmd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20mmdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%28LANG%28%3FVoltaireLabels%29%20as%20%3Flang%29%20%3FVoltaireLabels%20%0AWHERE%20%7B%20%0A%20%20%0A%20%20mmd%3AQ981%20mmdt%3AP13%20%3FwikiDataEntity.%20%23%20Voltaire%20has%20a%20wikidata%20match.%0A%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%3FwikiDataEntity%20rdfs%3Alabel%20%3FVoltaireLabels.%0A%20%20%7D%20%20%20%20%20%20%09%20%0A%7D%0AORDER%20BY%20%3Flang)

Query 9 Narrative location with geo coordinate locations via federated query (fig. 9) 
#defaultView:Map{"markercluster":"true"}
PREFIX wid: <http://www.wikidata.org/entity/> #wikidata wd
PREFIX widt: <http://www.wikidata.org/prop/direct/> #wikidata wdt
PREFIX wd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX wdt:<http://data.mimotext.uni-trier.de/prop/direct/>
SELECT DISTINCT ?item ?itemLabel ?narr_loc ?narr_locLabel ?WikiDataEntity ?coordinateLocation
WHERE { ?item wdt:P32 ?narr_loc.
  ?narr_loc wdt:P13 ?WikiDataEntity.
  #Federated Query -> Wikidata
  SERVICE <https://query.wikidata.org/sparql> {
	?WikiDataEntity widt:P625 ?coordinateLocation
  }      	 
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en" . }
}


Query 10, Alternative Labels of author names via ‘federated’ queries’
PREFIX wd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX wdt:<http://data.mimotext.uni-trier.de/prop/direct/>
PREFIX wid:<http://www.wikidata.org/entity/> #wikidata entity
PREFIX widt:<http://www.wikidata.org/prop/direct/> #wikidata property

SELECT DISTINCT ?author ?authorLabel ?wikidataEntity ?altname
WHERE {
	 ?item wdt:P5 ?author.
      ?author wdt:P13 ?wikidataEntity.  #exact match
 
 
      #Federated Query -> Wikidata
      
SERVICE <https://query.wikidata.org/sparql> {
   	 ?wikidataEntity skos:altLabel ?altname
      }     
 		 
      SERVICE wikibase:label {
   	 bd:serviceParam wikibase:language "en" .
      }
}
LIMIT 1000


Query 11: Influence networks of authors via ‘federated query’ (fig. 10)
defaultView:Graph
PREFIX wid:<http://www.wikidata.org/entity/> #wikidata entity
PREFIX widt:<http://www.wikidata.org/prop/direct/> #wikidata property

PREFIX wd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX wdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT DISTINCT ?item ?itemLabel ?authorLabel ?influencedby ?image ?name
WHERE {
      ?item wdt:P5 ?author.
      ?author wdt:P13 ?WikidataEntity.  #exact match
      
#Federated Query -> Wikidata
      SERVICE <https://query.wikidata.org/sparql> {
   	 ?WikidataEntity widt:P737/widt:P737 ?influencedby.
     	 # ?influencedby widt:P734 ?name.  
  		 OPTIONAL {  ?influencedby widt:P18 ?image.}
      }     
 		 
      SERVICE wikibase:label {
   	 bd:serviceParam wikibase:language "en" .
      }
}


Query 12 Proportions of different narrative perspectives (all novels) (fig 11., left)
#defaultView:BarChart
PREFIX wd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX wdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT ?topLabel (count(*) as ?count)
WHERE {
	 ?item wdt:P33 ?top . #narrative perspective
	 ?top rdfs:label ?topLabel .
	 FILTER(LANG(?topLabel) = "en")
}
GROUP BY ?topLabel
ORDER BY desc(?count)




Query 13: Finding Identifiers on other Knowledge Graphs, for example Bibliothèque nationale de France ID https://tinyurl.com/27ckm7y5 
 


# MiMoText novels with URL to Bibliothèque nationale de France
#defaultView:ImageGrid
PREFIX wid: <http://www.wikidata.org/entity/> #wikidata prefix definition for entity
PREFIX widt: <http://www.wikidata.org/prop/direct/> #wikidata prefix definition for property
PREFIX wd:<http://data.mimotext.uni-trier.de/entity/> #mimotext prefix for entity is wd
PREFIX wdt:<http://data.mimotext.uni-trier.de/prop/direct/> #mimotext prefix for property is wdt

SELECT ?item ?itemLabel ?wikidata ?bnfurl ?image
WHERE {
  ?item wdt:P2 wd:Q2.
  ?item wdt:P13 ?wikidata.
  ?item rdfs:label ?itemLabel .
  FILTER(lang(?itemLabel) = "en")
  SERVICE <https://query.wikidata.org/sparql> {
	?wikidata widt:P268 ?bnfid.
	OPTIONAL{ ?wikidata widt:P18 ?image.}
   OPTIONAL{ wid:P268 widt:P1630 ?formatterurl.}
   BIND(IRI(REPLACE(?bnfid, '^(.+)$', ?formatterurl)) AS ?bnfurl).
  }    	 
}

