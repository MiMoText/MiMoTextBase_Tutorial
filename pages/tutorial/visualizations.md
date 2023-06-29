---
#title: Visualizations 
#keywords:
#summary: 
sidebar: mydoc_sidebar_tutorial
permalink: visualizations.html
folder: queries
toc: True
---

### **Visualizations**

Learn more about the different types of visualizations that the WikibaseQueryService is offering. Following the [Wikidata-documentation](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/Wikidata_Query_Help/Result_Views){:target="_blank"}, we give an overview, specifying which types of Datatypes and sometimes additional data is needed in order to display the MiMoText-Data.

<!--
style="width: 100%; height:auto; border: none; padding:1%; position:relative; top:0; left:0;"
 -->

### **Overview**

The DockerWikibaseQueryService offers various options for visualising the result of queries. 
There are two options to do so: Either via the eye-Icon that will appear when you run a query. Or one uses the default view keyword within a query as follows: `#defaultView:[chosen view]`. 



### Table

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
<!-- <col width="60%"> -->
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2">
      <ul>
      <li>default view</li>
      <li>every data type possible</li>
      <li>every variable in SELECT is displayed in a table as column
</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td>
      <ul>
      <li>variables (e.g. ?item) in SELECT clause</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td ><ul>
      <li>show all datatypes of the objects that Item Q1053 (“Les liaisons dangereuses”) has as well as the connecting predicates. This <a href="https://query.mimotext.uni-trier.de/#PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0A%23%20show%20datatypes%20of%20objects%20that%20%22Les%20liaisons%20dangereuses%22%20%28Q1053%29%20has%20and%20their%20predicates.%0ASELECT%20DISTINCT%20%28datatype%28%3Fo%29%20as%20%3Fdatatype%29%20%3Fo%20%3FoLabel%20%3Fp%0AWHERE%7B%0A%20%20wd%3AQ1053%20%3Fp%20%3Fo.%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7DORDER%20BY%20desc%28%3Fdatatype%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer">query</a> will result in the following visualization:</li> </ul> <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:250px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0A%23%20show%20datatypes%20of%20objects%20that%20%22Les%20liaisons%20dangereuses%22%20%28Q1053%29%20has%20and%20their%20predicates.%0ASELECT%20DISTINCT%20%28datatype%28%3Fo%29%20as%20%3Fdatatype%29%20%3Fo%20%3FoLabel%20%3Fp%0AWHERE%7B%0A%20%20wd%3AQ1053%20%3Fp%20%3Fo.%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7DORDER%20BY%20desc%28%3Fdatatype%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query
Define all Prefixes needed for the query:
```sparql
PREFIX wd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX wdt: <http://data.mimotext.uni-trier.de/prop/direct/>
```
Within <code>SELECT</code> we ask for unique objects by calling <code>DISTINCT</code>. To retrieve the Datatype of the object <code>?o</code>, call <code>datatype</code> of the object and bind it to a new variable <code>?datatype</code>. Also select the item <code>?o</code>, the object label <code>?oLabel</code> and the properties <code>?p</code>

```sparql
SELECT DISTINCT (datatype(?o) as ?datatype) ?o ?oLabel ?p
```
In the <code>WHERE</code>-part, ask for a specific entity as subject <code>wd:Q1053</code> and all properties <code>?p</code> and connected values <code>?o</code>. By using the <code>Wikibase Label Service</code>, you can retrieve the labels.
To sort the result in descending oder of <code>?datatype</code>, use <code>ORDER BY</code>.
```sparql
WHERE{
  wd:Q1053 ?p ?o.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
} ORDER BY desc(?datatype)
```

### Image Grid

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result images as a grid</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>exact match (P13) for a federated query to wikidata (as we don’t have images in our graph)</li>
      <li>image files in wikidata for item</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>
    hide variables
    </li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>show all authors in the MiMoTextBase having an exact match to wikidata where an image is available, see query <a href="https://query.mimotext.uni-trier.de/index.html#%23defaultView%3AImageGrid%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0A%0A%23%20show%20all%20author%20images%20that%20have%20an%20exact%20match%20with%20wikidata%20and%20where%20it%20contains%20images%0ASELECT%20%3Fauthor%20%3FauthorLabel%20%3Fimg%0AWHERE%20%7B%0A%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP13%20%3FwikiLink.%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%7B%0A%20%20%3FwikiLink%20widt%3AP18%20%3Fimg.%0A%20%20%7D%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer">here</a> </li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3AImageGrid%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0A%23%20show%20all%20author%20images%20that%20have%20an%20exact%20match%20with%20wikidata%20and%20where%20it%20contains%20images%0A%0ASELECT%20%3Fauthor%20%3FauthorLabel%20%3Fimg%0AWHERE%20%7B%0A%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP13%20%3FwikiLink.%0A%20%20%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FwikiLink%20widt%3AP18%20%3Fimg.%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%20%20%20%20%20%20%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

Define the default view <code>#defaultView:ImageGrid</code> and the Prefixes for the MiMoTextBase and for Wikidata.

```sparql
#defaultView:ImageGrid
PREFIX wd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX wdt: <http://data.mimotext.uni-trier.de/prop/direct/>
PREFIX wid: <http://www.wikidata.org/entity/> #wikidata wd
PREFIX widt: <http://www.wikidata.org/prop/direct/> #wikidata wdt
```
Select the author-Item <code>?author</code>, the labels <code>?authorLabel</code> and the corresponding images <code>?img</code>.

```sparql
SELECT ?author ?authorLabel ?img
```
In the <code>WHERE</code>-part define authors by Items that have occupation <code>wdt:P11</code> author <code>wd:Q11</code>. By adding <code>wdt:P13 ?wikiLink</code>, restrict the query to those authors that have an exact match (P13) to wikidata and get the wikidata-Links. Using the Wikidata-Link within `SERVICE <https://query.wikidata.org/sparql>{...} `, you have now access to all the statements within Wikidata. Keep in mind to use the defined wikidata-Prefixes. Via `widt:P18` you can now retrieve the images for the authors, where available.  

```sparql
WHERE {
  ?author wdt:P11 wd:Q11;
          wdt:P13 ?wikiLink.
  SERVICE <https://query.wikidata.org/sparql>{
    ?wikiLink widt:P18 ?img.
  } 
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
```
#### Adding options
Example with hiding the file name:
By adding `#defaultView:ImageGrid{"hide":["?img"]}` the Link to the image source is now hidden, [see](https://query.mimotext.uni-trier.de/#%23defaultView%3AImageGrid%7B%22hide%22%3A%5B%22%3Fimg%22%5D%7D%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0A%23%20show%20all%20author%20images%20that%20have%20an%20exact%20match%20with%20wikidata%20and%20where%20it%20contains%20images%0A%0ASELECT%20%3Fauthor%20%3FauthorLabel%20%3Fimg%0AWHERE%20%7B%0A%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP13%20%3FwikiLink.%0A%20%20%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FwikiLink%20widt%3AP18%20%3Fimg.%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%20%20%20%20%20%20%0A%7D){:target="_blank"}.

### Map

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result in a map as map markers</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>location-Item (e.g. place of publication (P10)) having an exact match (P13) to wikidata where coordinates are available (P625)</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>possible variables: ?layer: shows layers of specific properties</li>
    <li>markercluster (boolean or object, for more information <a href="https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/Wikidata_Query_Help/Result_Views#Map" target="_blank" rel="noopener noreferrer">see</a>)
    </li>
    <li>hide</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li> query for all publication places, their Wikidata match and geographic coordinates, see query <a href="https://query.mimotext.uni-trier.de/#%23query%20for%20all%20publication%20places%2C%20their%20Wikidata%20match%20and%20geographic%20coordinates%20%0A%23defaultView%3AMap%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3FlocLabel%20%3FWikiDataEntity%20%3FcoordinateLocation%0AWHERE%20%7B%20%3Fitem%20wdt%3AP10%20%3Floc.%0A%20%20%3Floc%20wdt%3AP13%20%3FWikiDataEntity.%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiDataEntity%20widt%3AP625%20%3FcoordinateLocation%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A" target="_blank" rel="noopener noreferrer" >here</a>. </li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23query%20for%20all%20publication%20places%2C%20their%20Wikidata%20match%20and%20geographic%20coordinates%20%0A%23defaultView%3AMap%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3FlocLabel%20%3FWikiDataEntity%20%3FcoordinateLocation%0AWHERE%20%7B%20%3Fitem%20wdt%3AP10%20%3Floc.%0A%20%20%3Floc%20wdt%3AP13%20%3FWikiDataEntity.%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiDataEntity%20widt%3AP625%20%3FcoordinateLocation%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer" ></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

First, define the `#defaultView:Map` and the neccessary `PREFIXES` for the MiMoTextBase and Wikidata as you need it for the coordinates.

```sparql
#defaultView:Map
PREFIX wid: <http://www.wikidata.org/entity/> #wikidata wd
PREFIX widt: <http://www.wikidata.org/prop/direct/> #wikidata wdt
PREFIX wd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX wdt:<http://data.mimotext.uni-trier.de/prop/direct/> 
```
Within the `SELECT`-part, you can select the desired variables, but for a Map-visualization you need coordinates.
In the `WHERE`-clause we now choose all `?items`that have a place of publication `wdt:P10`. These in turn have a match to Wikidata `?loc wdt:P13 ?WikiDataEntity`. Using a federated query we now can retrieve the coordinates of those publication places.

```sparql
SELECT DISTINCT ?item ?itemLabel ?locLabel ?WikiDataEntity ?coordinateLocation
WHERE { ?item wdt:P10 ?loc.
  ?loc wdt:P13 ?WikiDataEntity.
  #Federated Query -> Wikidata
  SERVICE <https://query.wikidata.org/sparql> {
    ?WikiDataEntity widt:P625 ?coordinateLocation
  }           
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en" . }
}
```
#### Adding options

If you want to add a layer to your map, you can choose another variable, e.g. the tonality of the novels via `?item wdt:P38 ?tonaliy` in the `WHERE`-clause. Take the labels of the `?tonality`-variable and bind them to the variable `?layer` in the `SELECT`-part. In the map you now have different colors for the different tonalities, see example [here](https://query.mimotext.uni-trier.de/#%23query%20for%20all%20publication%20places%2C%20their%20Wikidata%20match%20and%20geographic%20coordinates%20%0A%23defaultView%3AMap%7Bmarkercluster%22%3A%22True%22%7D%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3FlocLabel%20%3FWikiDataEntity%20%3FcoordinateLocation%20%3FtonalityLabel%20%28%3FtonalityLabel%20as%20%3Flayer%29%20%0AWHERE%20%7B%20%3Fitem%20wdt%3AP10%20%3Floc.%0A%20%20%3Floc%20wdt%3AP13%20%3FWikiDataEntity.%0A%20%20%20%20%20%20%20%3Fitem%20wdt%3AP38%20%3Ftonality.%0A%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiDataEntity%20widt%3AP625%20%3FcoordinateLocation%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A){:target="_blank"}


You also can create layers on your own by binding variables to categories. Example for creating own layer based on a variable, eg. tokencount (be careful: layers can overlap, so you don’t see all of them immediately) and markerclusters [see](https://query.mimotext.uni-trier.de/#%23query%20for%20all%20publication%20places%2C%20their%20Wikidata%20match%20and%20geographic%20coordinates%20%0A%23defaultView%3AMap%7Bmarkercluster%22%3A%22True%22%7D%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3FlocLabel%20%3FWikiDataEntity%20%3FcoordinateLocation%20%3Flayer%20%3Ftokencount%0AWHERE%20%7B%20%3Fitem%20wdt%3AP10%20%3Floc.%0A%20%20%3Floc%20wdt%3AP13%20%3FWikiDataEntity.%0A%20%20%20%20%20%20%20%3Fitem%20wdt%3AP40%20%3Ftokencount.%0A%20%20%20%20%20%20%20%0A%20%20BIND%28%0A%20%20%20%20IF%28%3Ftokencount%20%3C%3D%2050000%2C%20%22short%22%2C%0A%20%20%20%20%20%20%20%20%09IF%28%3Ftokencount%20%3C%3D%20150000%2C%20%22medium%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%09%22long%22%29%29%0A%20%20%20%20%20%09AS%20%3Flayer%29.%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiDataEntity%20widt%3AP625%20%3FcoordinateLocation%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A){:target="_blank"}


Example with hiding coordinates, [see](https://query.mimotext.uni-trier.de/#%23query%20for%20all%20publication%20places%2C%20their%20Wikidata%20match%20and%20geographic%20coordinates%20%0A%23defaultView%3AMap%7B%22hide%22%3A%22%3FcoordinateLocation%22%2C%20%22markercluster%22%3A%22True%22%7D%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3FlocLabel%20%3FWikiDataEntity%20%3FcoordinateLocation%20%3Flayer%20%3Ftokencount%0AWHERE%20%7B%20%3Fitem%20wdt%3AP10%20%3Floc.%0A%20%20%3Floc%20wdt%3AP13%20%3FWikiDataEntity.%0A%20%20%20%20%20%20%20%3Fitem%20wdt%3AP40%20%3Ftokencount.%0A%20%20%20%20%20%20%20%0A%20%20BIND%28%0A%20%20%20%20IF%28%3Ftokencount%20%3C%3D%2050000%2C%20%22short%22%2C%0A%20%20%20%20%20%20%20%20%09IF%28%3Ftokencount%20%3C%3D%20150000%2C%20%22medium%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%09%22long%22%29%29%0A%20%20%20%20%20%09AS%20%3Flayer%29.%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiDataEntity%20widt%3AP625%20%3FcoordinateLocation%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A){:target="_blank"}




### Line Chart
<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result as a line graph</li>
        <li>first variable will be mapped on x-axis, second on y-axis</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>at least 2 variables of type: Numbers, Labels or Datetimes</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>stacked: 3 variables needed; third variable(category or Label) for displaying the categories </li>
      <li>animated line chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or Label) for displaying the categories  and fourth (category or Label) for animation; for an example of an animated graph, have a look in the Bar Chart section
</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>get the average token count from each possible narrative Form per year </li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ALineChart%0A%23%20get%20the%20average%20token%20count%20from%20each%20possible%20narrative%20Form%20per%20year%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fyear%20%28avg%28%3Ftokencount%29%20as%20%3Favgtokencount%29%20%3FnarrForm%20%3FnarrFormLabel%0A%20%20WHERE%7B%0A%20%20%20%20%3Fitem%20wdt%3AP9%20%3Fpublicationdate.%20%23%20get%20publication%20date%0A%20%20%20%20%3Fitem%20wdt%3AP40%20%3Ftokencount.%20%23%20get%20tokencount%0A%20%20%20%20BIND%28str%28YEAR%28%3Fpublicationdate%29%29%20as%20%3Fyear%29.%20%23%20extract%20year%20from%20pubdate%0A%20%20%20%20%3Fitem%20wdt%3AP33%20%3FnarrForm.%20%23%20get%20narrative%20form%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3FnarrForm%20%3Fyear%20%3FnarrFormLabel%0AORDER%20BY%20%3Fyear" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

### Bar Chart
<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result as a bar chart</li>
        <li>first variable will be mapped on x-axis, second on y-axis</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>at least 2 variables of type: Numbers, Labels or Datetimes</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>stacked: 3 variables needed; third variable(category or Label) for displaying the categories </li>
      <li>animated bar chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or Label) for displaying the categories  and fourth (category or Label) for animation
</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>get the average token count from each possible narrative Form per year, for query see <a href="https://query.mimotext.uni-trier.de/index.html#%23defaultView%3ABarChart%0A%23%20get%20the%20average%20token%20count%20from%20each%20possible%20narrative%20Form%20per%20year%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fyear%20%28avg%28%3Ftokencount%29%20as%20%3Favgtokencount%29%20%3FnarrFormLabel%0A%20%20WHERE%7B%0A%20%20%20%20%3Fitem%20wdt%3AP9%20%3Fpublicationdate.%20%23%20get%20publication%20date%0A%20%20%20%20%3Fitem%20wdt%3AP40%20%3Ftokencount.%20%23%20get%20tokencount%0A%20%20%20%20BIND%28str%28YEAR%28%3Fpublicationdate%29%29%20as%20%3Fyear%29.%20%23%20extract%20year%20from%20pubdate%0A%20%20%20%20%3Fitem%20wdt%3AP33%20%3FnarrForm.%20%23%20get%20narrative%20form%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3FnarrForm%20%3Fyear%20%3FnarrFormLabel%0AORDER%20BY%20%3Fyear" target="_blank" rel="noopener noreferrer">here</a> </li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ABarChart%0A%23%20get%20the%20average%20token%20count%20from%20each%20possible%20narrative%20Form%20per%20year%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fyear%20%28avg%28%3Ftokencount%29%20as%20%3Favgtokencount%29%20%3FnarrFormLabel%0A%20%20WHERE%7B%0A%20%20%20%20%3Fitem%20wdt%3AP9%20%3Fpublicationdate.%20%23%20get%20publication%20date%0A%20%20%20%20%3Fitem%20wdt%3AP40%20%3Ftokencount.%20%23%20get%20tokencount%0A%20%20%20%20BIND%28str%28YEAR%28%3Fpublicationdate%29%29%20as%20%3Fyear%29.%20%23%20extract%20year%20from%20pubdate%0A%20%20%20%20%3Fitem%20wdt%3AP33%20%3FnarrForm.%20%23%20get%20narrative%20form%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3FnarrForm%20%3Fyear%20%3FnarrFormLabel%0AORDER%20BY%20%3Fyear" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      <ul>
      <li>
      Show the tonality count per intentionality and year as an animated bar chart, for query see <a href="https://query.mimotext.uni-trier.de/index.html#PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%23%20%28animated%29%0A%23%20Show%20the%20tonality%20count%20per%20intentionality%20and%20year%0A%23defaultView%3ABarChart%0ASELECT%20%3FintentionalityLabel%20%28COUNT%28%3Ftonality%29%20AS%20%3FtonalityCount%29%20%3FtonalityLabel%20%28SAMPLE%28%3Fyear%29%20AS%20%3FYEAR%29%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20wdt%3AP9%20%3Fpubdate%3B%20%23%20get%20the%20publication%20date%0A%20%20%20%20%20%20%20%20wdt%3AP38%20%3Ftonality%3B%20%23%20get%20tonality%20of%20work-item%0A%20%20%20%20%20%20%20%20wdt%3AP39%20%3Fintentionality.%20%23%20get%20intentionality%20of%20work-item%0A%20%20%3Ftonality%20rdfs%3Alabel%20%3FtonalityLabel.%20%23%20get%20the%20tonality-label%0A%20%20%3Fintentionality%20rdfs%3Alabel%20%3FintentionalityLabel.%20%23%20get%20the%20intentionality-label%0A%20%20%0A%20%20FILTER%28LANG%28%3FtonalityLabel%29%20%3D%20%22en%22%29.%20%23%20filter%20for%20language%0A%20%20FILTER%28LANG%28%3FintentionalityLabel%29%3D%22en%22%29.%20%23%20filter%20for%20language%0A%20%20BIND%28str%28YEAR%28%3Fpubdate%29%29%20as%20%3Fyear%29.%20%23%20filter%20year%20of%20the%20publication%20date%0A%7D%0AGROUP%20BY%20%3Fpubdate%20%3FtonalityLabel%20%3FintentionalityLabel%20%0A" target="_blank" rel="noopener noreferrer">here</a>
      </li><lb/>
      </ul>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%23%20%28animated%29%0A%23%20Show%20the%20tonality%20count%20per%20intentionality%20and%20year%0A%23defaultView%3ABarChart%0ASELECT%20%3FintentionalityLabel%20%28COUNT%28%3Ftonality%29%20AS%20%3FtonalityCount%29%20%3FtonalityLabel%20%28SAMPLE%28%3Fyear%29%20AS%20%3FYEAR%29%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20wdt%3AP9%20%3Fpubdate%3B%20%23%20get%20the%20publication%20date%0A%20%20%20%20%20%20%20%20wdt%3AP38%20%3Ftonality%3B%20%23%20get%20tonality%20of%20work-item%0A%20%20%20%20%20%20%20%20wdt%3AP39%20%3Fintentionality.%20%23%20get%20intentionality%20of%20work-item%0A%20%20%3Ftonality%20rdfs%3Alabel%20%3FtonalityLabel.%20%23%20get%20the%20tonality-label%0A%20%20%3Fintentionality%20rdfs%3Alabel%20%3FintentionalityLabel.%20%23%20get%20the%20intentionality-label%0A%20%20%0A%20%20FILTER%28LANG%28%3FtonalityLabel%29%20%3D%20%22en%22%29.%20%23%20filter%20for%20language%0A%20%20FILTER%28LANG%28%3FintentionalityLabel%29%3D%22en%22%29.%20%23%20filter%20for%20language%0A%20%20BIND%28str%28YEAR%28%3Fpubdate%29%29%20as%20%3Fyear%29.%20%23%20filter%20year%20of%20the%20publication%20date%0A%7D%0AGROUP%20BY%20%3Fpubdate%20%3FtonalityLabel%20%3FintentionalityLabel%20%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

### Scatter Chart
<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result as a scatter chart</li>
        <li>first variable will be mapped on x-axis, second on y-axis</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>at least 2 variables of type: Numbers, Labels or Datetimes</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>stacked: 3 variables needed; third variable(category or Label) for displaying the categories </li>
      <li>animated line chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or Label) for displaying the categories  and fourth (category or Label) for animation; for an example of an animated graph, have a look in the Bar Chart section
</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>get the average token count from each possible narrative Form per year, for query see <a href="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3AScatterChart%0A%23%20get%20the%20average%20token%20count%20from%20each%20possible%20narrative%20Form%20per%20year%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fyear%20%28avg%28%3Ftokencount%29%20as%20%3Favgtokencount%29%20%3FnarrFormLabel%20%0A%20%20WHERE%7B%0A%20%20%20%20%3Fitem%20wdt%3AP9%20%3Fpublicationdate.%20%23%20get%20publication%20date%0A%20%20%20%20%3Fitem%20wdt%3AP40%20%3Ftokencount.%20%23%20get%20tokencount%0A%20%20%20%20BIND%28str%28YEAR%28%3Fpublicationdate%29%29%20as%20%3Fyear%29.%20%23%20extract%20year%20from%20pubdate%0A%20%20%20%20%3Fitem%20wdt%3AP33%20%3FnarrForm.%20%23%20get%20narrative%20form%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3FnarrForm%20%3Fyear%20%3FnarrFormLabel%20%0AORDER%20BY%20%3Fyear" target="_blank" rel="noopener noreferrer">here</a> </li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3AScatterChart%0A%23%20get%20the%20average%20token%20count%20from%20each%20possible%20narrative%20Form%20per%20year%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fyear%20%28avg%28%3Ftokencount%29%20as%20%3Favgtokencount%29%20%3FnarrFormLabel%20%0A%20%20WHERE%7B%0A%20%20%20%20%3Fitem%20wdt%3AP9%20%3Fpublicationdate.%20%23%20get%20publication%20date%0A%20%20%20%20%3Fitem%20wdt%3AP40%20%3Ftokencount.%20%23%20get%20tokencount%0A%20%20%20%20BIND%28str%28YEAR%28%3Fpublicationdate%29%29%20as%20%3Fyear%29.%20%23%20extract%20year%20from%20pubdate%0A%20%20%20%20%3Fitem%20wdt%3AP33%20%3FnarrForm.%20%23%20get%20narrative%20form%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3FnarrForm%20%3Fyear%20%3FnarrFormLabel%20%0AORDER%20BY%20%3Fyear" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query
### Area Chart

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result as an area chart</li>
        <li>first variable will be mapped on x-axis, second on y-axis</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>at least 2 variables of type: Numbers, Labels or Datetimes</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>stacked: 3 variables needed; third variable(category or Label) for displaying the categories </li>
      <li>animated line chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or Label) for displaying the categories  and fourth (category or Label) for animation; for an example of an animated graph, have a look in the Bar Chart section
</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>Get the occurrences of places of publication that exist at least 5 times (in total) and visualize them per year, see <a href="https://query.mimotext.uni-trier.de/index.html#%23defaultView%3AAreaChart%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fdate%20%28count%28%3FpubPlace%29%20as%20%3Fcount%29%20%3FpubPlaceLabel%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%0A%20%20%20%20%20%20%20%20wdt%3AP9%20%3Fdate%3B%0A%20%20%20%20%20%20%20%20wdt%3AP10%20%3FpubPlace.%0A%20%20%3FpubPlace%20rdfs%3Alabel%20%3FpubPlaceLabel.%0A%20%20FILTER%28LANG%28%3FpubPlaceLabel%29%20%3D%20%22en%22%29.%0A%7D%0A%0AGROUP%20BY%20%3Fdate%20%3FpubPlaceLabel%0AHAVING%20%28count%28%3FpubPlaceLabel%29%20%3E%204%29%0A%0A%0A" target="_blank" rel="noopener noreferrer">here</a>
      </li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3AAreaChart%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fdate%20%28count%28%3FpubPlace%29%20as%20%3Fcount%29%20%3FpubPlaceLabel%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%0A%20%20%20%20%20%20%20%20wdt%3AP9%20%3Fdate%3B%0A%20%20%20%20%20%20%20%20wdt%3AP10%20%3FpubPlace.%0A%20%20%3FpubPlace%20rdfs%3Alabel%20%3FpubPlaceLabel.%0A%20%20FILTER%28LANG%28%3FpubPlaceLabel%29%20%3D%20%22en%22%29.%0A%7D%0A%0AGROUP%20BY%20%3Fdate%20%3FpubPlaceLabel%0AHAVING%20%28count%28%3FpubPlaceLabel%29%20%3E%204%29%0A%0A%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>


#### Explanation of the query

### Bubble Chart

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result as a bubble chart</li>
        <li>size of bubble represents count of variable</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>variables of the possible DataTypes: Label, Item, Quantity
        </li>
      <li>(count(?variable) as ?count) to count a variable within select part</li>
      <li>GROUP BY all other variables that are in the select part
      </li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>Show the thematic concepts per novel</li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ABubbleChart%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3FtopLabel%20%28count%28%2a%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%3Fitem%20wdt%3AP36%20%3Ftop%20.%0A%20%3Ftop%20rdfs%3Alabel%20%3FtopLabel%20.%0A%20filter%28lang%28%3FtopLabel%29%20%3D%20%22en%22%29%0A%7D%0AGROUP%20BY%20%3FtopLabel%0AORDER%20BY%20desc%28%3Fcount%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

### TreeMap

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result as tree map</li>
        <li>order of variables in SELECT will be reflected by levels of the TreeMap</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>variables of the possible DataTypes: Label, Item, Quantity</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>Thematic concepts linked to the narrative location "rural area", see query <a href="https://query.mimotext.uni-trier.de/#%23defaultView%3ATreeMap%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%23mimotext%20prefix%20for%20entity%20is%20wd%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%23mimotext%20prefix%20for%20property%20is%20wdt%0A%0ASELECT%20%3Ftheme%20%3FthemeLabel%20%3Fitem%20%3FitemLabel%20WHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP36%20%3Ftheme%20.%0A%20%20%3Fitem%20wdt%3AP32%20wd%3AQ3243%20%23%20items%20with%20narrative%20location%20%28P32%29%3A%20rural%20area%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ATreeMap%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%23mimotext%20prefix%20for%20entity%20is%20wd%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%23mimotext%20prefix%20for%20property%20is%20wdt%0A%0ASELECT%20%3Ftheme%20%3FthemeLabel%20%3Fitem%20%3FitemLabel%20WHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP36%20%3Ftheme%20.%0A%20%20%3Fitem%20wdt%3AP32%20wd%3AQ3243%20%23%20items%20with%20narrative%20location%20%28P32%29%3A%20rural%20area%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

### Tree

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result as an expandable tree</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>variables of the possible DataTypes: Label, Item, Number</li>
      <li>special order of variables in different lines (see example). First will be the node of the Tree, the others follow as branches or leaves
      </li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>using of common media: exact match (P13) needed
    </li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>Get all authors, their novels and the respective thematic concepts, for query see <a href="https://query.mimotext.uni-trier.de/#%23defaultView%3ATree%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0A%23%20get%20all%20authors%2C%20their%20works%20and%20the%20corresponding%20thematic%20concepts%0ASELECT%20%3Fauthor%20%3FauthorLabel%0A%3Fitem%20%3FitemLabel%20%0A%3Ftopic%20%3FtopicLabel%0A%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%20%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20wdt%3AP36%20%3Ftopic%3B%20%23%20item%20has%20a%20thematic%20concept%0A%20%20%20%20%20%20%20%20wdt%3AP33%20%3FnarrForm%3B%20%23%20item%20has%20a%20narrative%20form%0A%20%20%20%20%20%20%20%20wdt%3AP5%20%3Fauthor.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%0A%7DORDER%20BY%20%3FauthorLabel%0A" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ATree%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0A%23%20get%20all%20authors%2C%20their%20works%20and%20the%20corresponding%20thematic%20concepts%0ASELECT%20%3Fauthor%20%3FauthorLabel%0A%3Fitem%20%3FitemLabel%20%0A%3Ftopic%20%3FtopicLabel%0A%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%20%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20wdt%3AP36%20%3Ftopic%3B%20%23%20item%20has%20a%20thematic%20concept%0A%20%20%20%20%20%20%20%20wdt%3AP33%20%3FnarrForm%3B%20%23%20item%20has%20a%20narrative%20form%0A%20%20%20%20%20%20%20%20wdt%3AP5%20%3Fauthor.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%0A%7DORDER%20BY%20%3FauthorLabel%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

### Timeline

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result as a timeline</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>one variables of the possible DataTypes: Label, Item, Number</li>
      <li>one variable of type DateTime
      </li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>hide: as Dates are of Type point in Time, are will be a day and month added in the MiMoTextBase (1. January). Using the option hide can select the year only. 
    </li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>Visualize the point in time when authors of the MiMoTextBase received an ward. See <a href="https://query.mimotext.uni-trier.de/#PREFIX%20pq%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fqualifier%2F%3E%0APREFIX%20p%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2F%3E%0A%23defaultView%3ATimeline%0A%23%20visualize%20the%20point%20in%20time%20when%20authors%20got%20an%20award%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0A%0A%0ASELECT%20%3Fitem%20%3Faward%20%3FitemLabel%20%3FawardLabel%20%3FWikiLink%20%3Fpit%20%3Ftime%0AWHERE%20%7B%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20%20%3Fitem%20wdt%3AP11%20wd%3AQ11.%0A%20%20%3Fitem%20wdt%3AP13%20%3FWikiLink.%0A%20%20%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiLink%20p%3AP166%20%3FawardStatement.%0A%20%20%20%20%3FWikiLink%20widt%3AP166%20%3Faward.%0A%20%20%20%20%3Faward%20rdfs%3Alabel%20%3FawardLabel.%0A%20%20%20%20FILTER%28LANG%28%3FawardLabel%29%3D%22en%22%29.%0A%20%20%20%20OPTIONAL%7B%3FawardStatement%20pq%3AP585%20%3Ftime.%7D%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A%0A" target="_blank" rel="noopener noreferrer">here</a>. Please notice: if you switch to table view, you get more results. But as there is no point in time statement available, it is not shown in the TimeLine.</li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#PREFIX%20pq%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fqualifier%2F%3E%0APREFIX%20p%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2F%3E%0A%23defaultView%3ATimeline%0A%23%20visualize%20the%20point%20in%20time%20when%20authors%20got%20an%20award%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0A%0A%0ASELECT%20%3Fitem%20%3Faward%20%3FitemLabel%20%3FawardLabel%20%3FWikiLink%20%3Fpit%20%3Ftime%0AWHERE%20%7B%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20%20%3Fitem%20wdt%3AP11%20wd%3AQ11.%0A%20%20%3Fitem%20wdt%3AP13%20%3FWikiLink.%0A%20%20%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiLink%20p%3AP166%20%3FawardStatement.%0A%20%20%20%20%3FWikiLink%20widt%3AP166%20%3Faward.%0A%20%20%20%20%3Faward%20rdfs%3Alabel%20%3FawardLabel.%0A%20%20%20%20FILTER%28LANG%28%3FawardLabel%29%3D%22en%22%29.%0A%20%20%20%20OPTIONAL%7B%3FawardStatement%20pq%3AP585%20%3Ftime.%7D%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query


### Dimensions


<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows variables as parallel axes with the possible values and draws connections between them if they exist</li>
        <li>possible Data Types are: Label, Numbers and DateTime</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>
      </li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>using of common media: exact match (P13) needed
    </li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>Get the dimension between token count and narrative form, see query <a href="https://query.mimotext.uni-trier.de/index.html#%23defaultView%3ADimensions%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3Ftokencount%20%3FformLabel%20WHERE%20%7B%0A%20%20%3Fnovel%20wdt%3AP40%20%3Ftokencount.%0A%20%20%3Fnovel%20wdt%3AP33%20%3Fform.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D%0A%0A%0A" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ADimensions%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3Ftokencount%20%3FformLabel%20WHERE%20%7B%0A%20%20%3Fnovel%20wdt%3AP40%20%3Ftokencount.%0A%20%20%3Fnovel%20wdt%3AP33%20%3Fform.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D%0A%0A%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query


### Graph


<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td> 
      <ul>
        <li>shows result as an interactive graph</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td >
      <ul>
      <li>one variable of type ITEM that will be the Node</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td>
    <ul>
    <li>possible additional DataTypes. Label for showing the ITEM label</li>
    <li>Image for Node-Item if ITEM has exact match (P13) to wikidata and there is a Image available</li>
    <li>Node-Size when DataType Number is given
    </li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td>
      <ul>
      <li>Show a graph of the authors within the MiMoTextBase connected by the organizations they were members of. See query <a href="https://query.mimotext.uni-trier.de/#%23defaultView%3AGraph%0A%23%20get%20all%20authors%20that%20are%20a%20member%20of%20any%20organization%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fitem%20%3FmemberOf%20%3FitemLabel%20%20%3FmemberOfLabel%0AWHERE%20%7B%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20%20%3Fitem%20wdt%3AP11%20wd%3AQ11.%0A%20%20%3Fitem%20wdt%3AP13%20%3FWikiLink.%0A%20%20%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiLink%20widt%3AP463%20%3FmemberOf.%0A%20%20%20%20%3FmemberOf%20rdfs%3Alabel%20%3FmemberOfLabel.%0A%20%20%20%20FILTER%28LANG%28%3FmemberOfLabel%29%3D%22en%22%29.%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A%0A" target="_blank" rel="noopener noreferrer">here</a>. You can zoom in to see the labels.</li>
      </ul>
    <lb/>
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:280px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3AGraph%0A%23%20get%20all%20authors%20that%20are%20a%20member%20of%20any%20organization%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fitem%20%3FmemberOf%20%3FitemLabel%20%20%3FmemberOfLabel%0AWHERE%20%7B%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20%20%3Fitem%20wdt%3AP11%20wd%3AQ11.%0A%20%20%3Fitem%20wdt%3AP13%20%3FWikiLink.%0A%20%20%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiLink%20widt%3AP463%20%3FmemberOf.%0A%20%20%20%20%3FmemberOf%20rdfs%3Alabel%20%3FmemberOfLabel.%0A%20%20%20%20FILTER%28LANG%28%3FmemberOfLabel%29%3D%22en%22%29.%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      <ul><li>Now we can constrain the least number of members that were at the same organization to 2 and get the images of the authors where available. See <a href="https://query.mimotext.uni-trier.de/#%23defaultView%3AGraph%0A%23%20get%20all%20authors%20that%20are%20a%20member%20of%20any%20organization%20having%20at%20least%20two%20members%20in%20the%20MiMotextBase%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fauthor%20%3FauthorLabel%20%3Fimg%20%3FmemberOf%20%3FmemberOfLabel%20%0AWHERE%20%7B%0A%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11.%20%0A%20%20%3Fauthor%20wdt%3AP13%20%3FWikiLink.%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiLink%20widt%3AP463%20%3FmemberOf.%0A%20%20%20%20%3FmemberOf%20rdfs%3Alabel%20%3FmemberOfLabel.%0A%20%20%20%20OPTIONAL%7B%3FWikiLink%20widt%3AP18%20%3Fimg%7D.%0A%20%20%20%20FILTER%28LANG%28%3FmemberOfLabel%29%3D%22en%22%29.%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7B%20%0A%20%20%20%20SELECT%20%3FmemberOf%20%28COUNT%28%3Fauthor%29%20as%20%3Fcountmember%29%20%0A%20%20%20%20WHERE%20%7B%0A%20%20%20%20%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11.%0A%20%20%20%20%20%20%3Fauthor%20wdt%3AP13%20%3FWikiLink.%0A%20%20%20%20%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%20%20%20%20%3FWikiLink%20widt%3AP463%20%3FmemberOf.%0A%20%20%20%20%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20%20%20%7D%0A%20%20GROUP%20BY%20%3FmemberOf%0A%20%20HAVING%20%28%3Fcountmember%20%3E%201%29%0A%20%20%7D%0A%7D%0A%0A%0A" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
      </td>
    </tr>
  </tbody>
</table>

