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

Learn more about the different types of visualizations that the WikibaseQueryService is offering. Following the [Wikidata-documentation](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/Wikidata_Query_Help/Result_Views), we give an overview, specifying which types of Datatypes and sometimes additional data is needed in order to display the MiMoText-Data.

<!--
style="width: 100%; height:auto; border: none; padding:1%; position:relative; top:0; left:0;"
 -->

### Table

<table>
<colgroup>
<col width="15%"/>
<col width="25%"/>
<col width="60%">
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
      <td colspan="2">
      <ul>
      <li>variables (e.g. ?item) in SELECT clause</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Example in the MiMoTextBase</th>
      <td > show all datatypes of the objects that Item Q1053 (“Les liaisons dangereuses”) has as well as the connecting predicates.</td>
      <td><iframe style="width: 100%; height:auto; border: none; padding:1%; position:relative; top:0; left:0;" src="https://query.mimotext.uni-trier.de/embed.html#PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0A%0A%23%20show%20datatypes%20of%20objects%20that%20%22Les%20liaisons%20dangereuses%22%20%28Q1053%29%20has%20and%20their%20predicates.%0ASELECT%20DISTINCT%20%28datatype%28%3Fo%29%20as%20%3Fdatatype%29%20%3Fo%20%3FoLabel%20%3Fp%0AWHERE%7B%0A%20%20wd%3AQ1053%20%3Fp%20%3Fo.%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7DORDER%20BY%20desc%28%3Fdatatype%29" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe></td>
    </tr>
  </tbody>
</table>

### Image Grid

<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2"> 
      <ul>
        <li>shows result images as a grid</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">
      <ul>
      <li>exact match (P13) for a federated query to wikidata (as we don’t have images in our graph)</li>
      <li>image files in wikidata for item</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">hide variables
    </td>
    </tr>
    <tr>
      <th rowspan="2">Example in the MiMoTextBase</th>
      <td>show all authors in the MiMoTextBase having an exact match to wikidata where an image is available</td>
      <td><iframe style="width: 100%; height:auto; border: none; padding:1%; position:relative; top:0; left:0; zoom:0.015;" src="https://query.mimotext.uni-trier.de/embed.html#%23defaultView%3AImageGrid%0APREFIX%20wd%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fdata.mimotext.uni-trier.de%2Fprop%2Fdirect%2F%3E%0APREFIX%20wid%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%20%23wikidata%20wd%0APREFIX%20widt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%20%23wikidata%20wdt%0A%23%20show%20all%20author%20images%20that%20have%20an%20exact%20match%20with%20wikidata%20and%20where%20it%20contains%20images%0A%0ASELECT%20%3Fauthor%20%3FauthorLabel%20%3Fimg%0AWHERE%20%7B%0A%20%20%3Fauthor%20wdt%3AP11%20wd%3AQ11%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP13%20%3FwikiLink.%0A%20%20%20%20SERVICE%20%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E%20%7B%0A%20%20%20%20%3FwikiLink%20widt%3AP18%20%3Fimg.%0A%20%20%7D%20%20%20%20%20%20%20%20%20%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%20%7D%0A%20%20%20%20%20%20%20%20%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe></td>
      <td>
      <tr>
      <td>example with hiding the file name</td>
      <td>https://tinyurl.com/2n48bxhb</td>
      </tr>
      </td>
    </tr>
  </tbody>
</table>


### Map

<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2">
      <ul>
      <li>shows result in a map as map markers</li>
      </ul>
      </td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">
      <ul>
      <li>location-Item (e.g. place of publication (P10)) having an exact match (P13) to wikidata where coordinates are available (P625)</li>
      </ul>
      </td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">
    <ul>
    <li>possible variables: ?layer</li>
    </ul>
    </td>
    </tr>
    <tr>
      <th rowspan="3">Example in the MiMoTextBase</th>
      <td>Query for all publication places, their Wikidata match and geographic coordinates</td>
      <td>https://tinyurl.com/2myscfk8</td>
    <td>
     <tr>
        <td>tonality layer</td>
        <td>https://tinyurl.com/2e7selk2</td>
    </tr>
    <tr>
        <td>create own layer based on tokencount (be careful: layers can overlap, so you don’t see all of them immediately)</td>
        <td>https://tinyurl.com/2e8ebb5b</td>
    </tr>
    </td>
    </tr>
  </tbody>
</table>

### Line Chart

<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2"> here comes the des.</td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">whats meeded   ssdsdgfsdfgsdgdfgsdfasdfasdfddkfgsdkgjksdgfjldsgjksdjglksdgjskdgjldkgjskdgjdkffgdfgsd</td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">dgfdgdg
    </td>
    </tr>
    <tr>
      <th>Example in MiMoTextBase</th>
      <td>sflksjgklfj</td>
      <td></td>
    </tr>
  </tbody>
</table>

### Bar Chart

<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2"> here comes the des.</td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">whats meeded   ssdsdgfsdfgsdgdfgsdfasdfasdfddkfgsdkgjksdgfjldsgjksdjglksdgjskdgjldkgjskdgjdkffgdfgsd</td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">dgfdgdg
    </td>
    </tr>
    <tr>
      <th>Example in MiMoTextBase</th>
      <td>sflksjgklfj</td>
      <td></td>
    </tr>
  </tbody>
</table>

### Scatter Chart

<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2"> here comes the des.</td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">whats meeded   ssdsdgfsdfgsdgdfgsdfasdfasdfddkfgsdkgjksdgfjldsgjksdjglksdgjskdgjldkgjskdgjdkffgdfgsd</td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">dgfdgdg
    </td>
    </tr>
    <tr>
      <th>Example in MiMoTextBase</th>
      <td>sflksjgklfj</td>
      <td></td>
    </tr>
  </tbody>
</table>

### Area Chart

<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2"> here comes the des.</td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">whats meeded   ssdsdgfsdfgsdgdfgsdfasdfasdfddkfgsdkgjksdgfjldsgjksdjglksdgjskdgjldkgjskdgjdkffgdfgsd</td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">dgfdgdg
    </td>
    </tr>
    <tr>
      <th>Example in MiMoTextBase</th>
      <td>sflksjgklfj</td>
      <td></td>
    </tr>
  </tbody>
</table>

### Bubble Chart

<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2"> here comes the des.</td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">whats meeded   ssdsdgfsdfgsdgdfgsdfasdfasdfddkfgsdkgjksdgfjldsgjksdjglksdgjskdgjldkgjskdgjdkffgdfgsd</td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">dgfdgdg
    </td>
    </tr>
    <tr>
      <th>Example in MiMoTextBase</th>
      <td>sflksjgklfj</td>
      <td></td>
    </tr>
  </tbody>
</table>

### TreeMap

<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2"> here comes the des.</td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">whats meeded   ssdsdgfsdfgsdgdfgsdfasdfasdfddkfgsdkgjksdgfjldsgjksdjglksdgjskdgjldkgjskdgjdkffgdfgsd</td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">dgfdgdg
    </td>
    </tr>
    <tr>
      <th>Example in MiMoTextBase</th>
      <td>sflksjgklfj</td>
      <td></td>
    </tr>
  </tbody>
</table>

### Tree

<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2"> here comes the des.</td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">whats meeded   ssdsdgfsdfgsdgdfgsdfasdfasdfddkfgsdkgjksdgfjldsgjksdjglksdgjskdgjldkgjskdgjdkffgdfgsd</td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">dgfdgdg
    </td>
    </tr>
    <tr>
      <th>Example in MiMoTextBase</th>
      <td>sflksjgklfj</td>
      <td></td>
    </tr>
  </tbody>
</table>

### Timeline


<table>
<colgroup>
<col width="20%"/>
<col width="30%"/>
<col width="50%">
</colgroup>
  <tbody>
    <tr>
      <th>Description</th>
      <td colspan="2"> here comes the des.</td>
    </tr>
    <tr>
      <th>Needed</th>
      <td colspan="2">whats meeded   ssdsdgfsdfgsdgdfgsdfasdfasdfddkfgsdkgjksdgfjldsgjksdjglksdgjskdgjldkgjskdgjdkffgdfgsd</td>
    </tr>
    <tr>
    <th>Options</th>
    <td colspan="2">dgfdgdg
    </td>
    </tr>
    <tr>
      <th>Example in MiMoTextBase</th>
      <td>sflksjgklfj</td>
      <td></td>
    </tr>
  </tbody>
</table>
