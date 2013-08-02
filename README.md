PLUTO Data Service
==================

To help jumpstart some interesting analysis and visualizations built on the PLUTO dataset, we have created a CartoDB instance dedicated to hosting this data for you. 


## Versions

* **Current** - 13.1
* **Available**
  * 13.1

## Data

Data is stored on CartoDB as individual tables in the same way that the [NYC.gov](http://www.nyc.gov/html/dcp/html/bytes/dwn_pluto_mappluto.shtml) website provides them. The naming schema is as follows

#### Table naming

File ```bk_mappluto_13v1.zip``` contains two shapefiles, ```BXMapPLUTO.shp``` and ```BX_Dcp_Mappinglot.shp```. They becomes two tables on CartoDB in the naming pattern {burrough code}_{file root}_{version}. For example,

|filename             |tablename         |
|---------------------|:-----------------|
|BXMapPLUTO.shp       |bx_mappluto_13v1  |
|BX_Dcp_Mappinglot.shp|bx_mappinglot_13v1|

#### Boroughs

[NYC.gov](http://www.nyc.gov/html/dcp/html/bytes/dwn_pluto_mappluto.shtml)  provides 5 files just like ```bk_mappluto_13v1.zip``` described above, one for each of the boroughs with codes as follows, ```qn, bk, si, bx, mn```.

## Filter & Query Data

You can use the SQL API to quickly query and filter data in any of the tables listed above. The SQL API takes [PostgreSQL](http://www.postgresql.org/docs/9.2/static/sql-syntax.html) and [PostGIS](postgis.refractions.net/docs/) SQL statements. This means you can query by distance, perform intersections, or full-text searches. A basic query would be as follows,

```sql
SELECT * FROM bk_mappluto_13v1 LIMIT 10
```

To access the result through the SQL API, you would use the URL, https://pluto.cartodb.com/api/v2/sql and pass it the `q=` parameter with your URL encoded SQL statement. The result of the above example would be,

[https://pluto.cartodb.com/api/v2/sql?q=SELECT%20*%20FROM%20bk_mappluto_13v1%20LIMIT%2010](https://pluto.cartodb.com/api/v2/sql?q=SELECT%20*%20FROM%20bk_mappluto_13v1%20LIMIT%2010)

#### Result format

If you want to use the data in a programming language such as Javascript or Python, the default JSON format will be handy. If you want to create client-side maps with Javascript (e.g. D3), you can get the results in GeoJSON by adding a parameter, ```&format=GeoJSON``` to your URL. Finally, if you want to filter and then download the results, you can get results formatted as CSV, ```&format=CSV```

## Maps

[![default maps](http://i.imgur.com/IGWCYNx.png)](http://cdb.io/12MBFlO)

Maps are available for each of the latest versions of the PLUTO datasets.

|dataset              |URL                     |
|---------------------|:-----------------------|
|bx_mappluto_13v1     |[http://cdb.io/12MBFlO](http://cdb.io/12MBFlO) |
|mn_mappluto_13v1     |[http://cdb.io/12MBK9d](http://cdb.io/12MBK9d) |
|bk_mappluto_13v1     |[http://cdb.io/12MBOpi](http://cdb.io/12MBOpi) |
|qn_mappluto_13v1     |[http://cdb.io/12MBPtn](http://cdb.io/12MBPtn) |
|si_mappluto_13v1     |[http://cdb.io/12MBS8q](http://cdb.io/12MBS8q) |

#### Use maps as [Leaflet](http://leafletjs.com/) map layers

You can build your own maps from these layers quickly and easily using [CartoDB.js](https://github.com/CartoDB/cartodb.js). The quickest example for creating a new map layer from ```mn_mappluto_13v1``` is as follows

```js
  var map = L.map('map').setView([40.77499462,-73.98909694], 12);

  // set a base layer 
  L.tileLayer('http://a.tile.stamen.com/toner/{z}/{x}/{y}.png', {
    attribution: 'stamen http://maps.stamen.com/'
  }).addTo(map);

  // add the cartodb layer
  var layerUrl = 'http://pluto.cartodb.com/api/v2/viz/e21b7338-fbb7-11e2-a0ed-7128c9850036/viz.json';
  cartodb.createLayer(map, layerUrl).addTo(map);
```

You can get more details on customizing the maps on the [CartoDB.js](https://github.com/CartoDB/cartodb.js) website. The [API documentation](https://github.com/CartoDB/cartodb.js/blob/develop/doc/API.md) will tell you how to customize styling and apply filters on the fly.

See this [working example](http://andrewxhill.github.io/cartodb-pluto/examples/basic.html) to get started.

##### Viz.JSON

To change use any of the datasets in the CartoDB.js visualizations, you need to change the ```layerUrl``` parameter in the example to the correct one for the desired dataset. Below are the dataset viz.json URLs,

|dataset              | Viz.json               |
|---------------------|:-----------------------|
|bx_mappluto_13v1     | http://pluto.cartodb.com/api/v2/viz/19652da8-fbb7-11e2-a75b-6139856afd6d/viz.json |
|mn_mappluto_13v1     |http://pluto.cartodb.com/api/v2/viz/e21b7338-fbb7-11e2-a0ed-7128c9850036/viz.json |
|bk_mappluto_13v1     |http://pluto.cartodb.com/api/v2/viz/09adeda4-fbb8-11e2-9ea5-15cfc813f31e/viz.json |
|qn_mappluto_13v1     |http://pluto.cartodb.com/api/v2/viz/4a335440-fbb8-11e2-8ac4-3f21906cb20f/viz.json |
|si_mappluto_13v1     |http://pluto.cartodb.com/api/v2/viz/5c8e6b3e-fbb8-11e2-a9af-619e94a2c50b/viz.json |

##### Client-side SQL

You can use SQL statements to filter the data on your maps or to access JSON or GeoJSON formatted data for building content or visualizations. For examples of each see

 * [Filtered maps](https://github.com/CartoDB/cartodb.js/blob/develop/doc/API.md#example-3)
 * [JSON request](https://github.com/CartoDB/cartodb.js/blob/develop/doc/API.md#getting-data-with-sql)

##### Style on the fly

[![owner type](http://i.imgur.com/GdLFlIx.png)](http://andrewxhill.github.io/cartodb-pluto/examples/owner_type.html)

You can style the maps on the fly using the Javascript library. Above is an example of the Bronx styled by the ```ownertype``` column. Click the image to see the live example. 

## Contact

Andrew Hill | [@andrewxhill](http://twitter.com/andrewxhill) | andrew@vizzuality.com 

Hosting provided by [CartoDB](http://cartodb.com)

