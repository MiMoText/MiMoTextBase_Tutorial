---
#title: Visualizations
#keywords:
#summary:
sidebar: mydoc_sidebar_tutorial
permalink: visualizations.html
folder: queries
toc: False #True
---

### **Visualizations**

Learn more about the different types of visualisations that the Wikibase Query Service is offering. Following the [Wikidata-documentation](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/Wikidata_Query_Help/Result_Views){:target="\_blank"}, we give an overview, specifying which types of datadtypes and sometimes additional data is needed in order to display the MiMoText data.

<!--
style="width: 100%; height:auto; border: none; padding:1%; position:relative; top:0; left:0;"
 -->

### **Overview**

The Wikidata Query Service offers various options for visualising the result of queries.
There are two ways to choose a visualisation, either via the "eye" icon that will appear when you run a query or via the "default view" keyword within a query as follows: `#defaultView:[chosen view]`.

<br/>

<table style="width:100%" id="vistoc">
<colgroup>
<col width="25%"/>
<col width="25%"/>
<col width="25%"/>
<col width="25%"/>
</colgroup>
<tbody>
<tr>
<td><a href="#Table"><button style="width:100%" class="btn-primary">Table</button></a></td>
<td><a href="#ImageGrid"><button style="width:100%" class="btn-primary">Image grid</button></a></td>
<td><a href="#Map"><button style="width:100%" class="btn-primary">Map</button></a></td>
<td><a href="#Line"><button style="width:100%" class="btn-primary">Line chart</button></a></td>
</tr>
<tr>
<td><a href="#Bar"><button style="width:100%" class="btn-primary">Bar chart</button></a></td>
<td><a href="#Scatter"><button style="width:100%" class="btn-primary">Scatter chart</button></a></td>
<td><a href="#Area"><button style="width:100%" class="btn-primary">Area chart</button></a></td>
<td><a href="#Bubble"><button style="width:100%" class="btn-primary">Bubble chart</button></a></td>
</tr>
<tr>
<td><a href="#TreeMap"><button style="width:100%" class="btn-primary">Tree map</button></a></td>
<td><a href="#Tree"><button style="width:100%" class="btn-primary">Tree</button></a></td>
<td><a href="#Timeline"><button style="width:100%" class="btn-primary">Timeline</button></a></td>
<td><a href="#Dimensions"><button style="width:100%" class="btn-primary">Dimensions</button></a></td>
</tr>
<tr>
<td><a href="#Graph"><button style="width:100%" class="btn-primary">Graph</button></a></td>
</tr>
</tbody>
</table>

### <a name="Table">Table

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
    </tr>
    <tr>
      <td style="width:100%">
      <ul>
      <li>default view</li>
      <li>every data type possible</li>
      <li>every variable in SELECT is displayed in a table as column</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>variables (e.g. ?item) in SELECT clause</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>show all datatypes of the objects under item Q1053 (“Les liaisons dangereuses”) and the connecting predicates. This <a href="https://tinyurl.com/27mgzc2d" target="_blank" rel="noopener noreferrer">query</a> will result in the following visualization:</li> </ul> <lb/>
          </td>
    </tr>
    <tr>
    <td tyle="width:100%">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/27mgzc2d" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

Define all prefixes needed for the query:

```sparql
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>
```

Within <code>SELECT</code> we ask for unique objects by calling <code>DISTINCT</code>. To retrieve the datatype of the object <code>?o</code>, call <code>datatype</code> of the object and bind it to a new variable <code>?datatype</code>. Also select the item <code>?o</code>, the object label <code>?oLabel</code> and the properties <code>?p</code>

```sparql
SELECT DISTINCT (datatype(?o) as ?datatype) ?o ?oLabel ?p
```

In the <code>WHERE</code>-part, ask for a specific entity as subject <code>mmd:Q1053</code> and all properties <code>?p</code> and connected values <code>?o</code>. By using the <code>Wikibase Label Service</code>, you can retrieve the labels.
To sort the result in descending oder of <code>?datatype</code>, use <code>ORDER BY</code>.

```sparql
WHERE{
  mmd:Q1053 ?p ?o.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
} ORDER BY desc(?datatype)
```

### <a name="ImageGrid"/>Image Grid

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows image results in a grid</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>exact match (P13) for a federated query to Wikidata (as we don’t have images in our graph)</li>
      <li>image files in Wikidata for item</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    <li>
    hide variables
    </li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>show all authors in the MiMoTextBase having an exact match with Wikidata and an image, see query <a href="https://tinyurl.com/267jcm5j" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer">here</a> </li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/2djm5lax" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

Define the default view <code>#defaultView:ImageGrid</code> and the prefixes for the MiMoTextBase and for Wikidata.

```sparql
#defaultView:ImageGrid
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
```

Select the author item <code>?author</code>, the labels <code>?authorLabel</code> and the corresponding images <code>?img</code>.

```sparql
SELECT ?author ?authorLabel ?img
```

In the <code>WHERE</code>-part define authors by Items that have occupation <code>mmdt:P11</code> author <code>mmd:Q11</code>. By adding <code>mmdt:P13 ?wikiLink</code>, restrict the query to those authors that have an exact match (P13) to Wikidata and get the Wikidata links. Using the Wikidata link within `SERVICE <https://query.wikidata.org/sparql>{...} `, we now have access to all the statements within Wikidata. Keep in mind to use the defined Wikidata prefixes. Via `wdt:P18` you can now retrieve the images for the authors, where available.

```sparql
WHERE {
  ?author mmdt:P11 mmd:Q11;
          mmdt:P13 ?wikiLink.
  SERVICE <https://query.wikidata.org/sparql>{
    ?wikiLink wdt:P18 ?img.
  }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
```

#### Adding options

Hiding the image file name:
By adding `#defaultView:ImageGrid{"hide":["?img"]}` the link to the image source can be hidden, [see](https://tinyurl.com/267385k9){:target="\_blank"}.

### <a name="Map"/>Map

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows result in a map as map markers</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>location item (e.g. place of publication (P10)) having an exact match (P13) with Wikidata where location coordinates are available (P625)</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
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
     </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li> query for all publication places, their Wikidata match and geographic coordinates, see query <a href="https://tinyurl.com/22fe9fw3" target="_blank" rel="noopener noreferrer" >here</a>. </li>
    </ul>
    </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/26uoz2jn" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer" ></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

First, define the `#defaultView:Map` and the neccessary `PREFIXES` for the MiMoTextBase and Wikidata as you need these for the coordinates.

```sparql
#defaultView:Map
PREFIX wd: <http://www.wikidata.org/entity/> #wikidata wd
PREFIX wdt: <http://www.wikidata.org/prop/direct/> #wikidata wdt
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>
```

Within the `SELECT` part, you can select the desired variables, but for a map visualisation you need coordinates.
In the `WHERE` clause we now choose all `?items` that have a place of publication `mmdt:P10`. These in turn have a match to Wikidata `?loc mmdt:P13 ?WikiDataEntity`. Using a federated query we now can retrieve the coordinates of those publication places.

```sparql
SELECT DISTINCT ?item ?itemLabel ?locLabel ?WikiDataEntity ?coordinateLocation
WHERE { ?item mmdt:P10 ?loc.
  ?loc mmdt:P13 ?WikiDataEntity.
  #Federated Query -> Wikidata
  SERVICE <https://query.wikidata.org/sparql> {
    ?WikiDataEntity wdt:P625 ?coordinateLocation
  }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en" . }
}
```

#### Adding options

If you want to add a layer to your map, you can choose another variable, e.g. the tone of the novels via `?item mmdt:P38 ?tone` in the `WHERE` clause. Take the labels of the `?tone` variable and bind them to the variable `?layer` in the `SELECT` part. On the map you now get different colors for the [different tones](https://tinyurl.com/277ddf3x){:target="\_blank"}.

You also can create layers on your own by binding variables to categories. As you need a variable `?layer` within `SELECT`, you can use `BIND` to assign layer variables. See [here](https://tinyurl.com/2yfwe29h){:target="\_blank"} an example for creating an individual layer based on a variable, e.g. token count (be careful: layers can overlap, so you don’t see all of them immediately) and marker clusters.

Same example with [hidden coordinates](https://tinyurl.com/2dnrb2lp){:target="\_blank"}.

### <a name="Line"/>Line Chart

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows result as a line graph</li>
        <li>first variable will be mapped on x-axis, second on y-axis</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>at least 2 variables of the data types numbers, labels or datetime</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    <li>stacked: 3 variables needed; third variable (category or label) for displaying the categories </li>
      <li>animated line chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or label) for displaying the categories  and fourth (category or label) for animation; for an example of an animated graph, take a look in the bar chart section
</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>get the average token count for each possible narrative form per year, see query <a href="https://tinyurl.com/25dlrjt8" target="_blank" rel="noopener noreferrer">here</a> </li>
    </ul>
    <lb/>
    </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/2ctvt4zv" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

As there are multiple functions provided, we can make use of them to get the average count of numbers, in this example the token count by calling `(avg(?tokencount) as ?avgtokencount)`. As we use this function, we have to `GROUP BY` all variables called in the `SELECT` part except the one we use to calculate the average (see line 14).

For extracting the year, without showing the day and month (as these are all set to 1st of January by default in data type DateTime only having a specific year), see line 10, where we extract the year via `YEAR(?publicationdate)`, turn it into a string variable `str(YEAR(...))` and assign it to a new variable name by `BIND(str(...))`.

```sparql
#defaultView:LineChart
#title:average token count for each possible narrative form per year
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT ?year (avg(?tokencount) as ?avgtokencount) ?narrForm ?narrFormLabel
  WHERE{
    ?item mmdt:P9 ?publicationdate. # get publication date
    ?item mmdt:P40 ?tokencount. # get tokencount
    BIND(str(YEAR(?publicationdate)) as ?year). # extract year from pubdate
    ?item mmdt:P33 ?narrForm. # get narrative form
    SERVICE wikibase:label { bd:serviceParam wikibase:language "en" . }
  }
GROUP BY ?narrForm ?year ?narrFormLabel
ORDER BY ?year

```

### <a name="Bar"/>Bar Chart

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows result as a bar chart</li>
        <li>first variable will be mapped on x-axis, second on y-axis</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>at least 2 variables of datatypes numbers, labels or datetimes</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    <li>stacked: 3 variables needed; third variable (category or label) for displaying the categories </li>
      <li>animated bar chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or label) for displaying the categories  and fourth (category or label) for animation
</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>get the average token count for each possible narrative form per year, for query see <a href="https://tinyurl.com/25f4eg5v" target="_blank" rel="noopener noreferrer">here</a> </li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/274z8tg8" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

See line charts.

#### Adding options

For creating an animated bar chart, let's take another query:
Show the tonality count per intentionality and year as an animated bar chart, for query see [here](https://query.mimotext.uni-trier.de/index.html#PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%23%20%28animated%29%0A%23%20Show%20the%20tone%20count%20per%20intention%20and%20year%0A%23defaultView%3ABarChart%0ASELECT%20%3FintentionLabel%20%28COUNT%28%3Ftone%29%20AS%20%3FtoneCount%29%20%3FtoneLabel%20%3Fyear%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20wdt%3AP9%20%3Fpubdate%3B%20%23%20get%20the%20publication%20date%0A%20%20%20%20%20%20%20%20wdt%3AP38%20%3Ftone%3B%20%23%20get%20tone%20of%20work-item%0A%20%20%20%20%20%20%20%20wdt%3AP39%20%3Fintention.%20%23%20get%20intention%20of%20work-item%0A%20%20%3Ftone%20rdfs%3Alabel%20%3FtoneLabel.%20%23%20get%20the%20tonality-label%0A%20%20%3Fintention%20rdfs%3Alabel%20%3FintentionLabel.%20%23%20get%20the%20intentionality-label%0A%20%20%0A%20%20FILTER%28LANG%28%3FtoneLabel%29%20%3D%20%22en%22%29.%20%23%20filter%20for%20language%0A%20%20FILTER%28LANG%28%3FintentionLabel%29%3D%22en%22%29.%20%23%20filter%20for%20language%0A%20%20BIND%28str%28YEAR%28%3Fpubdate%29%29%20as%20%3Fyear%29.%20%23%20filter%20year%20of%20the%20publication%20date%0A%7D%0AGROUP%20BY%20%3Fyear%20%3FtoneLabel%20%3FintentionLabel%20%0A){:target="\_blank"}

<iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%23%20%28animated%29%0A%23%20Show%20the%20tone%20count%20per%20intention%20and%20year%0A%23defaultView%3ABarChart%0ASELECT%20%3FintentionLabel%20%28COUNT%28%3Ftone%29%20AS%20%3FtoneCount%29%20%3FtoneLabel%20%3Fyear%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20wdt%3AP9%20%3Fpubdate%3B%20%23%20get%20the%20publication%20date%0A%20%20%20%20%20%20%20%20wdt%3AP38%20%3Ftone%3B%20%23%20get%20tone%20of%20work-item%0A%20%20%20%20%20%20%20%20wdt%3AP39%20%3Fintention.%20%23%20get%20intention%20of%20work-item%0A%20%20%3Ftone%20rdfs%3Alabel%20%3FtoneLabel.%20%23%20get%20the%20tonality-label%0A%20%20%3Fintention%20rdfs%3Alabel%20%3FintentionLabel.%20%23%20get%20the%20intentionality-label%0A%20%20%0A%20%20FILTER%28LANG%28%3FtoneLabel%29%20%3D%20%22en%22%29.%20%23%20filter%20for%20language%0A%20%20FILTER%28LANG%28%3FintentionLabel%29%3D%22en%22%29.%20%23%20filter%20for%20language%0A%20%20BIND%28str%28YEAR%28%3Fpubdate%29%29%20as%20%3Fyear%29.%20%23%20filter%20year%20of%20the%20publication%20date%0A%7D%0AGROUP%20BY%20%3Fyear%20%3FtoneLabel%20%3FintentionLabel%20%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe>

For an animated chart we need four variables, in this case the intention, the count of the variable for the tone, the labels of the tone and the publication dates. The last one will be the variable, that the animation switched between. As we call the `COUNT(...)`, we also need to `GROUP BY` all other variables occurring in the select part.

```sparql
PREFIX mmd: <http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt: <http://data.mimotext.uni-trier.de/prop/direct/>
# (animated)
# Show the tone count per intention and year
#defaultView:BarChart
SELECT ?intentionLabel (COUNT(?tone) AS ?toneCount) ?toneLabel ?year
WHERE{
  ?item mmdt:P2 mmd:Q2; # item is instance of literary work
        mmdt:P9 ?pubdate; # get the publication date
        mmdt:P38 ?tone; # get tone of work-item
        mmdt:P39 ?intention. # get intention of work-item
  ?tone rdfs:label ?toneLabel. # get the tonality-label
  ?intention rdfs:label ?intentionLabel. # get the intentionality-label

  FILTER(LANG(?toneLabel) = "en"). # filter for language
  FILTER(LANG(?intentionLabel)="en"). # filter for language
  BIND(str(YEAR(?pubdate)) as ?year). # filter year of the publication date
}
GROUP BY ?year ?toneLabel ?intentionLabel

```

### <a name="Scatter"/>Scatter Chart

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows result as a scatter chart</li>
        <li>first variable will be mapped on x-axis, second on y-axis</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>at least 2 variables of type: Numbers, Labels or Datetimes</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
       </tr>
      <tr>
      <td style="width:100%">
    <ul>
    <li>stacked: 3 variables needed; third variable(category or Label) for displaying the categories </li>
      <li>animated line chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or Label) for displaying the categories  and fourth (category or Label) for animation; for an example of an animated graph, have a look in the Bar Chart section
</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>get the average token count from each possible narrative Form per year, for query see <a href="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3AScatterChart%0A%23%20get%20the%20average%20token%20count%20from%20each%20possible%20narrative%20Form%20per%20year%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fyear%20%28avg%28%3Ftokencount%29%20as%20%3Favgtokencount%29%20%3FnarrFormLabel%20%0A%20%20WHERE%7B%0A%20%20%20%20%3Fitem%20wdt%3AP9%20%3Fpublicationdate.%20%23%20get%20publication%20date%0A%20%20%20%20%3Fitem%20wdt%3AP40%20%3Ftokencount.%20%23%20get%20tokencount%0A%20%20%20%20BIND%28str%28YEAR%28%3Fpublicationdate%29%29%20as%20%3Fyear%29.%20%23%20extract%20year%20from%20pubdate%0A%20%20%20%20%3Fitem%20wdt%3AP33%20%3FnarrForm.%20%23%20get%20narrative%20form%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3FnarrForm%20%3Fyear%20%3FnarrFormLabel%20%0AORDER%20BY%20%3Fyear" target="_blank" rel="noopener noreferrer">here</a> </li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3AScatterChart%0A%23%20get%20the%20average%20token%20count%20from%20each%20possible%20narrative%20Form%20per%20year%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fyear%20%28avg%28%3Ftokencount%29%20as%20%3Favgtokencount%29%20%3FnarrFormLabel%20%0A%20%20WHERE%7B%0A%20%20%20%20%3Fitem%20wdt%3AP9%20%3Fpublicationdate.%20%23%20get%20publication%20date%0A%20%20%20%20%3Fitem%20wdt%3AP40%20%3Ftokencount.%20%23%20get%20tokencount%0A%20%20%20%20BIND%28str%28YEAR%28%3Fpublicationdate%29%29%20as%20%3Fyear%29.%20%23%20extract%20year%20from%20pubdate%0A%20%20%20%20%3Fitem%20wdt%3AP33%20%3FnarrForm.%20%23%20get%20narrative%20form%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7D%0AGROUP%20BY%20%3FnarrForm%20%3Fyear%20%3FnarrFormLabel%20%0AORDER%20BY%20%3Fyear" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

See explanation for LineChart.

### <a name="Area"/>Area Chart

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
         </tr>
      <tr>
      <td style="width:100%"> 
      <ul>
        <li>shows result as an area chart</li>
        <li>first variable will be mapped on x-axis, second on y-axis</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>at least 2 variables of type: Numbers, Labels or Datetimes</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    <li>stacked: 3 variables needed; third variable(category or Label) for displaying the categories </li>
      <li>animated line chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or Label) for displaying the categories  and fourth (category or Label) for animation; for an example of an animated graph, have a look in the Bar Chart section
</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>Get the occurrences of places of publication that exist at least 5 times (in total) and visualize them per year, see <a href="https://query.mimotext.uni-trier.de/index.html#%23defaultView%3AAreaChart%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fdate%20%28count%28%3FpubPlace%29%20as%20%3Fcount%29%20%3FpubPlaceLabel%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%0A%20%20%20%20%20%20%20%20wdt%3AP9%20%3Fdate%3B%0A%20%20%20%20%20%20%20%20wdt%3AP10%20%3FpubPlace.%0A%20%20%3FpubPlace%20rdfs%3Alabel%20%3FpubPlaceLabel.%0A%20%20FILTER%28LANG%28%3FpubPlaceLabel%29%20%3D%20%22en%22%29.%0A%7D%0A%0AGROUP%20BY%20%3Fdate%20%3FpubPlaceLabel%0AHAVING%20%28count%28%3FpubPlaceLabel%29%20%3E%204%29%0A%0A%0A" target="_blank" rel="noopener noreferrer">here</a>
      </li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3AAreaChart%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0ASELECT%20%3Fdate%20%28count%28%3FpubPlace%29%20as%20%3Fcount%29%20%3FpubPlaceLabel%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%0A%20%20%20%20%20%20%20%20wdt%3AP9%20%3Fdate%3B%0A%20%20%20%20%20%20%20%20wdt%3AP10%20%3FpubPlace.%0A%20%20%3FpubPlace%20rdfs%3Alabel%20%3FpubPlaceLabel.%0A%20%20FILTER%28LANG%28%3FpubPlaceLabel%29%20%3D%20%22en%22%29.%0A%7D%0A%0AGROUP%20BY%20%3Fdate%20%3FpubPlaceLabel%0AHAVING%20%28count%28%3FpubPlaceLabel%29%20%3E%204%29%0A%0A%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

As we want to visualize the count of occurrences of publication places, we need to use the `COUNT`-function for counting the publication places-variable. Therefore we need to use the `GROUP BY` on all other variables within the select part. Next, as we want to limit the occurrences to be at least 4, we can use `HAVING (count(?pubPlaceLabel) > 4)`. Another option would be to reuse the newly generated ?count variable via `HAVING (?count > 4)`

```sparql
#defaultView:AreaChart
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>

SELECT ?date (count(?pubPlace) as ?count) ?pubPlaceLabel
WHERE{
  ?item mmdt:P2 mmd:Q2;
        mmdt:P9 ?date;
        mmdt:P10 ?pubPlace.
  ?pubPlace rdfs:label ?pubPlaceLabel.
  FILTER(LANG(?pubPlaceLabel) = "en").
}

GROUP BY ?date ?pubPlaceLabel
HAVING (count(?pubPlaceLabel) > 4)
# other option:
# HAVING (?count > 4)
```

### <a name="Bubble"/>Bubble Chart

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows result as a bubble chart</li>
        <li>size of bubble represents count of variable</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
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
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>Show the thematic concepts per novel, see query <a href="https://query.mimotext.uni-trier.de/#%23defaultView%3ABubbleChart%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3FtopicLabel%20%28COUNT%28%3FtopicLabel%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%3Fitem%20wdt%3AP2%20wd%3AQ2.%20%23%20get%20all%20instances%20of%20literary%20work%0A%20%3Fitem%20wdt%3AP36%20%3Ftopic%20.%20%23%20get%20the%20thematic%20concepts%20of%20the%20items%0A%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel%20.%0A%20FILTER%28LANG%28%3FtopicLabel%29%20%3D%20%22en%22%29%20.%20%0A%7D%0AGROUP%20BY%20%3FtopicLabel%0AORDER%20BY%20desc%28%3Fcount%29" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ABubbleChart%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3FtopicLabel%20%28COUNT%28%3FtopicLabel%29%20as%20%3Fcount%29%0AWHERE%20%7B%0A%20%3Fitem%20wdt%3AP2%20wd%3AQ2.%20%23%20get%20all%20instances%20of%20literary%20work%0A%20%3Fitem%20wdt%3AP36%20%3Ftopic%20.%20%23%20get%20the%20thematic%20concepts%20of%20the%20items%0A%20%3Ftopic%20rdfs%3Alabel%20%3FtopicLabel%20.%0A%20FILTER%28LANG%28%3FtopicLabel%29%20%3D%20%22en%22%29%20.%20%0A%7D%0AGROUP%20BY%20%3FtopicLabel%0AORDER%20BY%20desc%28%3Fcount%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

To generate a Bubble Chart, one need to use the `count`-function to get the count of a desired variable, as the size of the bubbles represent the number of occurrences of that variable. That in follows means, that you have to `GROUP BY` all the other variables used in the `SELECT`-part, in this case it only concerns the `?topicLabel`. To put the largest bubbles in the center of the visualization, one can add `ORDER BY DESC([count-variable])`.

```sparql
#defaultView:BubbleChart
PREFIX mmd:<http://data.mimotext.uni-trier.de/entity/>
PREFIX mmdt:<http://data.mimotext.uni-trier.de/prop/direct/>
SELECT ?topicLabel (COUNT(?topicLabel) as ?count)
WHERE {
 ?item mmdt:P2 mmd:Q2. # get all instances of literary work
 ?item mmdt:P36 ?topic . # get the thematic concepts of the items
 ?topic rdfs:label ?topicLabel .
 FILTER(LANG(?topicLabel) = "en") .
}
GROUP BY ?topicLabel
ORDER BY desc(?count)

```

### <a name="TreeMap"/>TreeMap

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows result as tree map</li>
        <li>order of variables in SELECT will be reflected by levels of the TreeMap</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>variables of the possible DataTypes: Label, Item, Quantity</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>Thematic concepts linked to the narrative location "rural area", see query <a href="https://query.mimotext.uni-trier.de/#%23defaultView%3ATreeMap%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%23mimotext%20prefix%20for%20entity%20is%20wd%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%23mimotext%20prefix%20for%20property%20is%20wdt%0A%0ASELECT%20%3Ftheme%20%3FthemeLabel%20%3Fitem%20%3FitemLabel%20WHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2.%0A%20%20%3Fitem%20wdt%3AP36%20%3Ftheme%20.%0A%20%20%3Fitem%20wdt%3AP32%20wd%3AQ3243%20%23%20items%20with%20narrative%20location%20%28P32%29%3A%20rural%20area%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ATreeMap%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%23mimotext%20prefix%20for%20entity%20is%20wd%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%23mimotext%20prefix%20for%20property%20is%20wdt%0A%0ASELECT%20%3Ftheme%20%3FthemeLabel%20%3Fitem%20%3FitemLabel%20WHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2.%0A%20%20%3Fitem%20wdt%3AP36%20%3Ftheme%20.%0A%20%20%3Fitem%20wdt%3AP32%20wd%3AQ3243%20%23%20items%20with%20narrative%20location%20%28P32%29%3A%20rural%20area%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

In order to retrieve a TreeMap one must consider the order of the variables within the `SELECT`-part as it will reflect the hierarchy of the Tree. As we chose `theme` as the first variable, all following variables will be clustered within the corresponding theme.

### <a name="Tree"/>Tree

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows result as an expandable tree</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>variables of the possible DataTypes: Label, Item, Number</li>
      <li>special order of variables in different lines (see example). First will be the node of the Tree, the others follow as branches or leaves
      </li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    <li>using of common media: exact match (P13) needed
    </li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>Get all authors, their novels and the respective thematic concepts, for query see <a href="https://query.mimotext.uni-trier.de/#%23defaultView%3ATree%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0A%23%20get%20all%20authors%2C%20their%20works%20and%20the%20corresponding%20thematic%20concepts%0ASELECT%20%3Fauthor%20%3FauthorLabel%0A%3Fitem%20%3FitemLabel%20%0A%3Ftopic%20%3FtopicLabel%0A%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%20%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20wdt%3AP36%20%3Ftopic%3B%20%23%20item%20has%20a%20thematic%20concept%0A%20%20%20%20%20%20%20%20wdt%3AP33%20%3FnarrForm%3B%20%23%20item%20has%20a%20narrative%20form%0A%20%20%20%20%20%20%20%20wdt%3AP5%20%3Fauthor.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%0A%7DORDER%20BY%20%3FauthorLabel%0A" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ATree%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0A%23%20get%20all%20authors%2C%20their%20works%20and%20the%20corresponding%20thematic%20concepts%0ASELECT%20%3Fauthor%20%3FauthorLabel%0A%3Fitem%20%3FitemLabel%20%0A%3Ftopic%20%3FtopicLabel%0A%0AWHERE%7B%0A%20%20%3Fitem%20wdt%3AP2%20wd%3AQ2%3B%20%20%23%20item%20is%20instance%20of%20literary%20work%0A%20%20%20%20%20%20%20%20wdt%3AP36%20%3Ftopic%3B%20%23%20item%20has%20a%20thematic%20concept%0A%20%20%20%20%20%20%20%20wdt%3AP33%20%3FnarrForm%3B%20%23%20item%20has%20a%20narrative%20form%0A%20%20%20%20%20%20%20%20wdt%3AP5%20%3Fauthor.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%0A%7DORDER%20BY%20%3FauthorLabel%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

To create an expandable tree, one must select more than one variable. Within the `SELECT`-part the order of the variables will represent the hierarchy of the tree. Also each of the variables must be written in an own line (except the associated label variables).

```sparql
SELECT ?author ?authorLabel
?item ?itemLabel
?topic ?topicLabel
```

This `SELECT`-part will therefore create a tree having the authors as nodes. For each author the novels and for each novel the thematic concepts will appear if expanded.

### <a name="Timeline"/>Timeline

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows result as a timeline</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>one variables of the possible DataTypes: Label, Item, Number</li>
      <li>one variable of type DateTime
      </li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    <li>hide: as Dates are of Type point in Time, are will be a day and month added in the MiMoTextBase (1. January). Using the option hide can select the year only. 
    </li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>Visualize the point in time when authors of the MiMoTextBase received an award. See <a href="https://query.mimotext.uni-trier.de/#%23defaultView%3ATimeline%0APREFIX%20ps%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fstatement%2F%3E%0APREFIX%20pq%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fqualifier%2F%3E%0APREFIX%20p%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2F%3E%0A%0A%23%20visualize%20the%20point%20in%20time%20when%20authors%20got%20an%20award%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fitem%20%3Faward%20%3FitemLabel%20%3FawardLabel%20%3Ftime%0AWHERE%20%7B%0A%20%20%0A%20%20%3Fitem%20wdt%3AP11%20wd%3AQ11.%0A%20%20%3Fitem%20wdt%3AP13%20%3FWikiLink.%0A%20%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiLink%20p%3AP166%20%3FawardProperty.%20%23%20get%20the%20property%20%0A%20%20%20%20%3FawardProperty%20ps%3AP166%20%3Faward.%20%23%20get%20the%20statement%20of%20the%20propery%0A%20%20%20%20%3Faward%20rdfs%3Alabel%20%3FawardLabel.%20%23%20get%20the%20Label%0A%20%20%20%20FILTER%28LANG%28%3FawardLabel%29%20%3D%22en%22%29.%0A%20%20%20%20%0A%20%20%20%20OPTIONAL%7B%3FawardProperty%20pq%3AP585%20%3Ftime.%7D%20%23%20get%20the%20qualifiert%20point%20in%20time%20when%20available%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A%0A" target="_blank" rel="noopener noreferrer">here</a>. Please notice: if you switch to table view, you get more results. But as there is no point in time statement available, it is not shown in the TimeLine.</li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ATimeline%0APREFIX%20ps%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fstatement%2F%3E%0APREFIX%20pq%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fqualifier%2F%3E%0APREFIX%20p%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2F%3E%0A%0A%23%20visualize%20the%20point%20in%20time%20when%20authors%20got%20an%20award%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fitem%20%3Faward%20%3FitemLabel%20%3FawardLabel%20%3Ftime%0AWHERE%20%7B%0A%20%20%0A%20%20%3Fitem%20wdt%3AP11%20wd%3AQ11.%0A%20%20%3Fitem%20wdt%3AP13%20%3FWikiLink.%0A%20%0A%20%20%23Federated%20Query%20-%3E%20Wikidata%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiLink%20p%3AP166%20%3FawardProperty.%20%23%20get%20the%20property%20%0A%20%20%20%20%3FawardProperty%20ps%3AP166%20%3Faward.%20%23%20get%20the%20statement%20of%20the%20propery%0A%20%20%20%20%3Faward%20rdfs%3Alabel%20%3FawardLabel.%20%23%20get%20the%20Label%0A%20%20%20%20FILTER%28LANG%28%3FawardLabel%29%20%3D%22en%22%29.%0A%20%20%20%20%0A%20%20%20%20OPTIONAL%7B%3FawardProperty%20pq%3AP585%20%3Ftime.%7D%20%23%20get%20the%20qualifiert%20point%20in%20time%20when%20available%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%7D%0A%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

With this query we ask for the awards the authors within the MiMoTextBase received and when this happend to visualize it on a TimeLine. As we do not have this information in the MiMoTextBase, we can write a federated query to use the data within WikiData.
Therefore we first retrieve all possible wikidata-matches via `?item wdt:P13 ?Wikilink`. Now calling the `SERVICE <https://query.wikidata.org/sparql>` we can query statements within WikiData.
If you have a look at the property `award received`[here](https://www.wikidata.org/wiki/Q15975), you can see that the value `award received` (P166) is the Item _Fellow of the Royal Society_. This Item itself has a so called `qualifier` `point in time` with the value _26 February 1730_. This is the data that we want to receive.
In order to get all statements and qualifiers associated to a property, we first need to define new `PREFIXES`:

```sparql
PREFIX ps: <http://www.wikidata.org/prop/statement/>
PREFIX pq: <http://www.wikidata.org/prop/qualifier/>
PREFIX p: <http://www.wikidata.org/prop/>
```

Now, within in the wikidata-query, we first retrieve all values associated to `P166` (award received) via

```sparql
?WikiLink p:P166 ?awardProperty.
```

As we also want the label of the awards, we need to get the statements and the labels.

```sparql
?awardProperty ps:P166 ?award. # get the statement of the propery
?award rdfs:label ?awardLabel. # get the Label
FILTER(LANG(?awardLabel) ="en").
```

Not all og the statements have the qualifier `point in time`, so we use `OPTIONAL` to get all statement and for those, where available, a `point in time`.

```sparql
OPTIONAL{?awardProperty pq:P585 ?time.} # get the qualifiert point in time when available

```

### <a name="Dimensions"/>Dimensions

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows variables as parallel axes with the possible values and draws connections between them if they exist</li>
        <li>possible Data Types are: Label, Numbers and DateTime</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>at least two variables to show their connection
      </li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    <li>using of common media: exact match (P13) needed
    </li>
    </ul>
    </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>Get the dimension between token count and narrative form, see query <a href="https://query.mimotext.uni-trier.de/index.html#%23defaultView%3ADimensions%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3Ftokencount%20%3FformLabel%20WHERE%20%7B%0A%20%20%3Fnovel%20wdt%3AP40%20%3Ftokencount.%0A%20%20%3Fnovel%20wdt%3AP33%20%3Fform.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D%0A%0A%0A" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3ADimensions%0Aprefix%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%20%0Aprefix%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0ASELECT%20%3Ftokencount%20%3FformLabel%20WHERE%20%7B%0A%20%20%3Fnovel%20wdt%3AP40%20%3Ftokencount.%0A%20%20%3Fnovel%20wdt%3AP33%20%3Fform.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D%0A%0A%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

As the variables within `SELECT`are represented as dimension axes, the order will also be represented.

### <a name="Graph"/>Graph

<table>
<colgroup>
<col width="15%"/>
<col width="85%"/>
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
        <li>shows result as an interactive graph</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>one variable of type ITEM that will be the Node</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
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
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>Show a <a href="https://tinyurl.com/2czkacxz" target="_blank" rel="noopener noreferrer">graph</a> of the authors within the MiMoTextBase connected by the organisations they were members of. You can zoom in to view the labels:</li>
      </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/2czkacxz" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

With this query we want to get all organisations of which the authors in the MiMoTextBase were members. This is an information we don't find in the MiMoTextBase, therefore we can use a federated query to WikiData to retrieve it. Asking for `item mmdt:P13 ?WikiLink` we get the wikidata-matches of the authors. Using this variable, we can now call ` SERVICE <https://query.wikidata.org/sparql>` to query wikidata. Via `?WikiLink wdt:P463 ?memberOf.` we get all organizations connected to the authors.
In the graph, now edges occur between the authors and the associated organizations.

#### Adding options

Now we can constrain the least number of members that were at the same organization to 2 and get the images of the authors where available. See [here](https://query.mimotext.uni-trier.de/#%23defaultView%3AGraph%0A%23%20get%20all%20authors%20that%20are%20a%20member%20of%20any%20organization%20having%20at%20least%20two%20members%20in%20the%20MiMotextBase%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0APREFIX%20wd%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%20%0A%0ASELECT%20%3Fauthor%20%3FauthorLabel%20%3Fimg%20%3FmemberOf%20%3FmemberOfLabel%20%0AWHERE%20%7B%0A%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11.%20%0A%20%20%3Fauthor%20wdt%3AP13%20%3FWikiLink.%0A%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FWikiLink%20widt%3AP463%20%3FmemberOf.%0A%20%20%20%20%3FmemberOf%20rdfs%3Alabel%20%3FmemberOfLabel.%0A%20%20%20%20OPTIONAL%7B%3FWikiLink%20widt%3AP18%20%3Fimg%7D.%0A%20%20%20%20FILTER%28LANG%28%3FmemberOfLabel%29%3D%22en%22%29.%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%7B%20%0A%20%20%20%20SELECT%20%3FmemberOf%20%28COUNT%28%3Fauthor%29%20as%20%3Fcountmember%29%20%0A%20%20%20%20WHERE%20%7B%0A%20%20%20%20%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11.%0A%20%20%20%20%20%20%3Fauthor%20wdt%3AP13%20%3FWikiLink.%0A%20%20%20%20%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%20%20%20%20%3FWikiLink%20widt%3AP463%20%3FmemberOf.%0A%20%20%20%20%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20%20%20%7D%0A%20%20GROUP%20BY%20%3FmemberOf%0A%20%20HAVING%20%28%3Fcountmember%20%3E%201%29%0A%20%20%7D%0A%7D%0A%0A%0A){:target="\_blank"}

To filter the result to those organizations that have at least two members from the MiMoTextBase, we can expand the query above by a second query within the first as nested query. After the first query, but before closing it, we are going to copy the same query with the exception that we add the `COUNT(?author)` to the `SELECT`-part. Therefore we need to add the `GROUP BY` to the end of the query. Via `HAVING ([count-variable] > 1)` we now can filter for those organizations having at least two members.
