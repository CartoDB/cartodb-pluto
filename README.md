PLUTO Data Service
==================

To help jumpstart some interesting analysis and visualization built on the PLUTO dataset, we have created a CartoDB instance dedicated to hosting this data for you. 


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

## Maps

![default maps](http://i.imgur.com/PDUeTIU.png)

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


## Contact

Andrew Hill
[@andrewxhill](http://twitter.com/andrewxhill)
andrew@vizzuality.com 


