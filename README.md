# osmx-web

A lightweight web server for submitting jobs to an OSM Express database.

## API

GET `/`

Returns:

- the last updated timestamp
- the nodes limit for the server

GET `/nodes.png`

POST `/`

API endpoint for submitting jobs.

- `RegionType` - one of `bbox`, `geojson`

`bbox`: 

`geojson`: a GeoJSON Geometry, either a Polygon or MultiPolygon 

* up to the configured nodes limit of the server.
* Limit on the number of vertices in the input polygon.

Returns a UUID.

Returns an error message

GET `/{uuid}` : get a JSON API response for a task submitted in the last 24 hours.

Returns a Progress object:

```js
{
  "Timestamp": 
  "CellsProg": "",
  "CellsTotal": "",
  "NodesProg": "",
  "NodesTotal": "",
  "ElemsProg": "",
  "ElemsTotal":"",
  "SizeBytes":"",
  "Elapsed":"",
  "Complete":""
}
```

## File Server

GET `/{uuid}_region.json` - get the GeoJSON submitted for this task.

```json
{
  "Uuid":"",
  "SanitizedName": "abcd",
  "SanitizedRegionType":"",
  "SanitizedRegionData":""
}
```

GET `/{uuid}.osm.pbf` - download the file. This appears once the API reports `Completed`.

##

```
GOOS=linux GOARCH=arm64 go build main.go
```