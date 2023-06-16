# Displaying, Classifying and Symbolizing Data

**Symbolizing Features**
- Polygons - fill and outlines (color, pattern, thickness of boarder)
- Point symbology - shape, size and color
- Lines - line style, width, color

**Styles**\
Styles are great when you are responsible for creating a lot of maps for the same organization. Businesses, governments, and anyone else who produces information in map form has (or should have) basic cartographic standards. That is, the symbology for map features (roads, rivers) and map elements (scale bars, north arrows, titles) should be consistent. ESRI includes quite a few styles in ArcGIS -- for forestry, geology, urban planning, and other common uses. You can also create your own.

**Maps**\
A **choropleth map** is a map in which polygons, lines and points are colored or shaded to represent attribute values; areas of same value are the same color. It is used to show the intensity of some quantity.
A **proportional symbol map** uses discrete symbols and is used for count data.

**Labels**\
It is necessary to include a label that tells the map reader what the data represent, e.g, if have a graduated symbol map, it is necessary to label what the symbols represent (including units, which generally are not included in a map title), and then for each different sized symbol have the appropriate value. All information necessary to make sense of the map needs to be on the map.

---
Example: **Choropleth and Proportional Map**

<img width="717" alt="Screen Shot 2023-06-16 at 2 31 35 PM" src="https://github.com/RutaCodes/GeoSpatial/assets/111301407/06861c10-7aa6-46d5-8770-e79a1f0e8ef6">

Population per square mile was selected converting count data into intensity data. That data was split into intervals. 8 classes were chosen to accuratety represent the distribution, making sure data is not split into too many intervals as it would be difficult to distinguish between shades of colour and what they represent.

Proportional symbols are sized according to the data value. It suits to present city population data very well since it can represent small objects accordingly to the size of the value and display a proportional symbol to represnt it. 5 classes were selected in order to accurately represent the population distribution without overcrowding the map with too many different sized circles.
