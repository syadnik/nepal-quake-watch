# nepal-quake-watch
SSCI 591 Project 3
**Live map:** https://syadnik.github.io/nepal-quake-watch/

## a. What this map shows
This map shows recent earthquakes in and around Nepal, pulled live from the USGS Earthquake Catalog. I chose Nepal because of the debris avalanche and flash flood that began on 26 August 2026 in Langtang National Park and travelled about 100 km downstream. The map highlights the two seismic signals that USGS linked to that event and draws a 100 km reference ring around the first one. Visitors can filter earthquakes by time window and magnitude, and click the map to count events within 50, 100, or 200 km.

## b. Starting sample
I started from the [GeoJSONLayer with dynamic URL](https://developers.arcgis.com/javascript/latest/sample-code/layers-geojson-refresh/) sample in the ArcGIS Maps SDK for JavaScript 5.1 gallery.

## c. What I changed
I moved the map from Japan to Nepal by changing the center, zoom, and the bounding box in `customParameters`. I deleted the sample's Japan-only `definitionExpression` and its custom blurred basemap, and I switched to the `dark-gray-vector` basemap. I replaced the alert-level renderer with markers whose size and color both scale with magnitude. I replaced the alert radio buttons with time-window and magnitude filters that call `layer.refresh()`, and I removed the end date so the rolling window always reaches the present. I also added summary cards, a click-to-analyze proximity tool, a Nepal boundary layer, and an event spotlight that loads two USGS event records with `fetch()`. Finally, I added a page title, an "About this map" paragraph, and a 75vh map height. To reuse the code, change the bounding box, the center, and the event IDs.

## d. Data source
The main layer uses the [USGS Earthquake Catalog API](https://earthquake.usgs.gov/fdsnws/event/1/) at `https://earthquake.usgs.gov/fdsnws/event/1/query` through a `GeoJSONLayer`. I picked this layer type because the API returns GeoJSON directly and accepts filters as URL parameters, which fits `customParameters` and `refresh()`. The event spotlight uses `fetch()` on two USGS event records (`us7000tbwb` and `us7000tc90`) and draws them as graphics. The Nepal outline is a `FeatureLayer` from Esri's World Countries (Generalized) feature service.

## e. Component I added
I added the Basemap Toggle (`<arcgis-basemap-toggle>`), which switches between the dark vector basemap and satellite imagery. I chose it because USGS maps this kind of event by comparing satellite images from before and after, so imagery gives useful context. The Legend was already part of the sample.

## f. Problems and what I'd improve next
The USGS API only accepts a rectangle, so my bounding box includes parts of India and China. The 100 km ring is a straight-line reference, not the real flow path, which followed the Lende Khola and Trishuli Khola. The event information is preliminary and may change. Next I would add the inundation extent once USGS publishes it, plus river, road, and settlement layers to estimate exposure.

## g. Credits
Earthquake and event data come from the U.S. Geological Survey, and the event background comes from the [USGS Landslide Hazards Program](https://www.usgs.gov/programs/landslide-hazards/science/2026-nepal-debris-avalanche-and-flash-flood). The starting sample and the boundary service are from Esri. I used Claude (Sonnet 5.5) to help edit the sample code, debugging it, and then I tested the app and checked the content myself.
