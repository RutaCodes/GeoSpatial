# Assessing Flood Depth

Vectors (points, lines, polygons) are useful for analyzing discrete units, but to understand geographic phenomena that exist as a field or a surface, we use the raster model. Instead of storing information as attributes associated with a vector shape, rasters store information as a series of cells that are continuous. Each cell can only have one attribute and it must be a numeric value. Raster data is highly dependent on resolution, or, the ratio of the cell size to the area it would cover "on the ground" (like scale). For example, a LANDSAT image of the Earth is a raster, as are all images. It has a 30m resolution, meaning that each cell is equivalent to a square area on the earth that is 30m x 30m. Resolution defines the information captured in the raster.

In this example we will overlay two raster datasets. Then we will reclassify the resulting dataset. Finally, we will convert the raster layer to a vector layer. The two rasters for this example include an elevation surface for the vicinity of Mud Run (a stream in Akron, OH) and a surface that will represent the heights of a 100-vear flood. To assess flood depth the elevation surface is subtracted from the flood surface. Those areas with positive cell values are considered flooded by a storm producing a 100-year flood and those areas with negative cell values are considered not flooded by a 100-year flood.

<img width="519" alt="Screen Shot 2023-06-07 at 2 20 31 PM" src="https://github.com/RutaCodes/GeoSpatial/assets/111301407/4007432f-58fc-4299-8a65-834e0b6ddde4">

