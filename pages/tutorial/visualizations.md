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

In <code>WHERE</code>, ask for a specific entity as subject <code>mmd:Q1053</code> and all properties <code>?p</code> and connected values <code>?o</code>. By using the <code>Wikibase Label Service</code>, you can retrieve the labels.
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

In <code>WHERE</code>, define authors by items that have occupation <code>mmdt:P11</code> author <code>mmd:Q11</code>. By adding <code>mmdt:P13 ?wikiLink</code>, restrict the query to those authors that have an exact match (P13) to Wikidata and get the Wikidata links. Using the Wikidata link within `SERVICE <https://query.wikidata.org/sparql>{...} `, we now have access to all the statements within Wikidata. Keep in mind to use the defined Wikidata prefixes. Via `wdt:P18` you can now retrieve the images for the authors, where available.

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

Within `SELECT`, you can select the desired variables, but for a map visualisation you need coordinates.
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

If you want to add a layer to your map, you can choose another variable, e.g. the tone of the novels via `?item mmdt:P38 ?tone` in the `WHERE` clause. Take the labels of the `?tone` variable and bind them to the variable `?layer` in `SELECT`. On the map you now get different colors for the [different tones](https://tinyurl.com/277ddf3x){:target="\_blank"}.

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

As there are multiple functions provided, we can make use of them to get the average count of numbers, in this example the token count by calling `(avg(?tokencount) as ?avgtokencount)`. As we use this function, we have to `GROUP BY` all variables called in `SELECT`, except the one we use to calculate the average (see line 14).

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
Count of different tones per intention and year as animated bar chart, see [here](https://tinyurl.com/2xkuu9xy){:target="\_blank"}

<iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/288heaej" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe>

For an animated chart we need four variables, in this case the intention, the count of the variable for the tone, the labels of the tone and the publication dates. The last one will be the variable the animation switches between. As we call the `COUNT(...)`, we also need to `GROUP BY` all other variables occurring in `SELECT`.

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
      <li>animated scatter chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or label) for displaying the categories  and fourth (category or label) for animation; for an example of an animated graph, take a look in the bar chart section
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
      <li>get the average token count for each possible narrative form per year, see query <a href="https://tinyurl.com/2749qduy" target="_blank" rel="noopener noreferrer">here</a> </li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/2yufgqbn" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

See line chart.

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
      <li>animated area chart: 4 variables needed, first is on x-axis, second on y-axis, third (category or label) for displaying the categories  and fourth (category or label) for animation; for an example of an animated graph, have a look in the bar chart section
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
      <li>Show publication places that occurr at least 5 times per year, see <a href="https://tinyurl.com/265ob5w7" target="_blank" rel="noopener noreferrer">here</a>
      </li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/26pdavmf" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

As we want to visualise the count of occurrences of publication places, we need to use the `COUNT` function for counting the publication places variable. Therefore we need to use the `GROUP BY` on all other variables within `SELECT`. Next, as we want to limit the occurrences to be at least 4, we can use `HAVING (count(?pubPlaceLabel) > 4)`. Another option would be to reuse the newly generated ?count variable via `HAVING (?count > 4)`

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
      <li>variables of the possible datatypes label, item, quantity
        </li>
      <li>`(count(?variable) as ?count)` to count a variable within SELECT</li>
      <li>GROUP BY all other variables that are in SELECT
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
      <li>Show the thematic concepts per novel, see query <a href="https://tinyurl.com/2xmwmvon" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/25wa753s" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

To generate a bubble chart, you need to use the `count` function to get the count of a desired variable, as the size of the bubbles represent the number of occurrences of that variable. This also means that you have to `GROUP BY` all the other variables used in `SELECT`, in this case it only concerns the `?topicLabel`. To put the largest bubbles in the center of the visualisation, you can add `ORDER BY DESC([count-variable])`.

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

### <a name="Tree Map"/>TreeMap

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
        <li>order of variables in SELECT will be reflected by levels of the tree map</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      </tr>
      <tr>
      <td style="width:100%">
      <ul>
      <li>variables of the possible data types label, item or quantity</li>
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
      <li>Thematic concepts linked to the narrative location "rural area", see query <a href="https://tinyurl.com/2b8fakrv" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/2as99wyy" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

In order to retrieve a tree map you must consider the order of the variables within `SELECT` as it will reflect the hierarchy of the tree. As we chose `theme` as the first variable, all following variables will be clustered within the corresponding theme.

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
      <li>variables of the possible data types label, item or number</li>
      <li>special order of variables in different lines (see example): the first will be the node of the tree, the others follow as branches or leaves
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
    <li>for using common media: exact match (P13) needed
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
      <li>Get all authors, their novels and the respective thematic concepts, for query see <a href="https://tinyurl.com/24np5opg" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/2284vy66" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

To create an expandable tree, we must select more than one variable. Within `SELECT` the order of the variables will represent the hierarchy of the tree. Also each of the variables must be written on a separate line (except the associated label variables).

```sparql
SELECT ?author ?authorLabel
?item ?itemLabel
?topic ?topicLabel
```

`SELECT` will therefore create a tree with the authors as nodes. When expanded, the novels of each author and the thematic concepts of each novel will appear.

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
      <li>one variable of data type label, item or number</li>
      <li>one variable of data type datetime
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
    <li>hide: as dates are of type `point in time`, there will be a default day and month in the MiMoTextBase (1. January). Using the option hide shows the year only. 
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
      <li>Visualise the points in time when authors of the MiMoTextBase received an award, see query <a href="https://tinyurl.com/29letq5z" target="_blank" rel="noopener noreferrer">here</a>. 
      Please note: If you switch to table view, you get more results. But as there is no point in time statement available, it is not shown in the timeline.</li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/24gds3z8" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

We query for the awards the authors of the MiMoTextBase have received and the dates they were awared and visualise the result as a timeline. Since we do not have this information in the MiMoTextBase, we formulate a federated query to retrieve Wikidata.

Therefore we first retrieve all possible Wikidata matches via `?item mmdt:P13 ?Wikilink`. Now calling the `SERVICE <https://query.wikidata.org/sparql>` we can query statements within Wikidata.
If you have a look at the property `award received` <a href="https://www.wikidata.org/wiki/Q15975" target="_blank" rel="noopener noreferrer">e.g. of this item</a>, you can see that the value `award received` (P166) has the item _Fellow of the Royal Society_. This item itself has a so called `qualifier` `point in time` for the value _26 February 1730_. This is the data that we want to receive.

In order to get all statements and qualifiers associated to a property, we first need to define new `PREFIXES`:

```sparql
PREFIX ps: <http://www.wikidata.org/prop/statement/>
PREFIX pq: <http://www.wikidata.org/prop/qualifier/>
PREFIX p: <http://www.wikidata.org/prop/>
```

Now, within in the Wikidata query, we first retrieve all values associated with `P166` (`award received`) via

```sparql
?WikiLink p:P166 ?awardProperty.
```

As we also want the label of the awards, we need to get the statements and the labels.

```sparql
?awardProperty ps:P166 ?award. # get the statement of the propery
?award rdfs:label ?awardLabel. # get the Label
FILTER(LANG(?awardLabel) ="en").
```

Not all of the statements have the qualifier `point in time`, so we use `OPTIONAL` to get all statements and, where available, a `point in time`.

```sparql
OPTIONAL{?awardProperty pq:P585 ?time.} # get the qualifier 'point in time' where available

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
        <li>possible data types are label, numbers and datetime</li>
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
    <li>for use of common media: exact match (P13) needed
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
      <li>Get the dimension between token count and narrative form, see query <a href="https://tinyurl.com/29dzsmkc" target="_blank" rel="noopener noreferrer">here</a></li>
    </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/28a8zvtz" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

Since the variables within `SELECT`are represented as dimension axes, the order will also be represented.

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
      <li>one variable of type item as node</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    </tr>
      <tr>
      <td style="width:100%">
    <ul>
    <li>possible additional data types: label for showing the item name</li>
    <li>image for node item if item has exact match (P13) with Wikidata and there is an image available</li>
    <li>node size when data type number is given
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
      <li>Show a <a href="https://tinyurl.com/2czkacxz" target="_blank" rel="noopener noreferrer">graph</a> of the authors within the MiMoTextBase connected with the organisations they were members of. You can zoom in to view the labels:</li>
      </ul>
    <lb/>
        </td>
    </tr>
    <tr>
    <td colspan="2">
      <iframe style="width: 100%; max-width:100%; max-height:100%; height:370px; border: none; padding:1%; position:relative; top:0; left:0;" src="https://tinyurl.com/284mz8zc" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" target="_blank" rel="noopener noreferrer"></iframe> <lb/>
      </td>
    </tr>
  </tbody>
</table>

#### Explanation of the query

With this query we want to get all organisations of which the authors in the MiMoTextBase were members. This is an information we don't find in the MiMoTextBase, therefore we use a federated query to retrieve Wikidata. Asking for `item mmdt:P13 ?WikiLink` we get the Wikidata matches of the authors. Using this variable, we can now call `SERVICE` <https://query.wikidata.org/sparql> to query Wikidata. Via `?WikiLink wdt:P463 ?memberOf` we get all organisations connected to the authors. In the graph, edges occur between the authors and their associated organisations.

#### Adding options

We can add the condition that only authors of organisations with at least 2 members are shown and retrieve the images of the authors where available, see [here](https://tinyurl.com/2b5r4s96){:target="\_blank"}.

To limit the result to those organisations that have at least two members from the MiMoTextBase, we can expand the query above by a second query within the first as nested query. After the first query, but before closing it, we are going to copy the same query with the exception of adding `COUNT(?author)` to `SELECT`. Therefore we need to add the `GROUP BY` to the end of the query. Via `HAVING ([count-variable] > 1)` we now can filter for those organisations having at least two members.
