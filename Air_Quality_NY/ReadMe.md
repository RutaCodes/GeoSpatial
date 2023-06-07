# Cumulative Air Pollution Analysis Using ArcGIS

1. INTRODUCTION
- 1.1 Significance of the problem 
2. METHODS
- 2.1 Raw data
- 2.2 Data modifications
- 2.3 Spatial interpretations
3. RESULTS
- 3.1 Ozone
- 3.2 Sulfur Dioxide
- 3.3 Nitrogen Dioxide
- 3.4 Carbon Monoxide
- 3.5 Particulate Matter 2.5
- 3.6 Particulate Matter 10 
- 3.7 Cumulative Air Pollution
4. DISCUSSION
5. CONCLUSIONS \
References
---
**1.	INTRODUCTION**

*1.1 Significance of the problem*

Air pollution is a serious problem damaging ecosystems, contributing to global warming and endangering human health. It is caused by harmful chemicals and substances entering and contaminating the atmosphere. Significant levels of contaminants in the air can cause adverse health effects on people of all ages. Exposure to air pollutants has been linked to asthma exacerbation, reduced lung function, cardiovascular and respiratory diseases. Therefore, it is important to study and monitor air contamination levels. In general, there are two types of air quality standards. First, environmental agencies enact regulations with target levels of atmospheric concentration for each specific pollutant. Second, individual air contaminant is classified in several categories according to threshold concentrations that correspond to health risk level. Each of those threshold values correspond to Air Quality Index (AIQ) which is used to inform the public about the relative risk of outdoor activities. In the USA, these threshold values are set by Environmental Protection Agency (EPA). 

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/2d1a2626-1884-489d-ae82-891f617bd17c)
Figure 1. EPA's table of breakpoints

Generally, air quality statistics reflect the levels of six air pollutants: ozone, nitrogen dioxide, sulfur dioxide, carbon monoxide, lead and particulate matter. Particulate matter measures microscopic solid or liquid particles suspended in the atmosphere and affecting climate and precipitation that impact human health. Inhalable coarse particles with a diameter of 2.5 and 10 micrometers correspond to PM2.5 (fine particulate) and PM10 category respectively.

New York State Department of Environmental Conservation measures air pollutant concentration using continuous or/and manual instrumentation at more than fifty sites across the state. Monitoring the ambient air quality is essential for protecting humans and the environment by helping develop programs targeting appropriate source categories for emission reduction.

**2.	METHODS**

*2.1 Raw data*

Every year New York State Department of Environmental Conservation release a summary of ambient air monitoring data with annual or running concentration averages for various air pollutants. New York State Ambient Air Quality Report for 2015 was used to obtain air pollutant concentration information across the New York state. In the report, data is presented in multiple tables dividing air monitoring stations into nine regions (Long Island, New York City, Lower Hudson Valley, Capital Region/Northern Catskills, Eastern Adirondacks/Lake Champlain, Western Adirondacks/Eastern Lake Ontario, Central New York, Western Finger Lakes, Western New York) and separating data according to air pollutant type. Each air contaminant is presented with unique set of data varying from annual averages (SO2), maximum and percentile values (PM2.5), 8-hr running average (03) and 24-hr concentration (PM10). However, some of the monitoring stations do not measure certain pollutants.

Six air contaminants were selected for further analysis: O3, SO2, NO2, CO, PM2.5, PM10.

*2.2 Data modifications*

First, consistent concentration measurement was selected for each pollutant since unified measurement was not available due to different concentration monitoring techniques applied to specific contaminants. The second step was to transfer the data from the report into the excel in order to be able to import the data into ArcGIS software. Excel file contained concentration data corresponding to a specific monitoring station represented by a site number.

Spatial representation of the monitoring stations was needed. File with spatial information about all monitoring stations used by New York State Department of Environmental Conservation was downloaded from NYS GIS Clearing house. Shapefile contained x-y data representing coordinates of each station. 

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/16618233-8842-4547-823b-15bd18c6a831)
Figure 2. Air monitoring stations

Another shapefile was used containing a polygon representing New York state. 

Both shapefiles used the same projection and therefore no spatial errors were observed that could be caused by different projection systems used. After that both files were combined to spatially represent location of monitoring stations within the state boundaries.

After importing the excel file with concentration data into ArcGIS, table joining was performed to combine monitoring station shapefile with concentration data in the excel file. Site number was used as a common field in both attribute tables.

Once table joining was achieved, a shapefile containing monitoring station location and concentration data was created which was used as a main file for further analysis. This shapefile will be called as ‘Air Monitoring layer’ throughout any descriptions in following sections of this report.

*2.3 Spatial interpretation*

Air monitoring layer contained point data and it needed spatial configurations to achieve a continuous representation of New York state air pollutant distribution. ‘Select by attributes’ command was used to select stations that measured air concentration of a specific pollutants and were transferred into a separate layer. In that way, six layers were created containing information about specific air contaminant containing monitoring station location and air concentration data. Since layers contained only positive concentration measurement values, it did not affect interpolation analysis that would have been influenced by values equal to zero (in case that specific air contaminant was not measured in that monitoring station).

To create surface representation in ArcGIS, Spatial Analyst extension was implemented in order to perform any spatial data manipulation. For spatial distribution analysis, interpolation tool was chosen to predict the values at locations that lack sampled points within the area covered by existing observations.  It is based on the principle of spatial dependence, which measures degree of relationship between close and distant points creating a statistical surface. Geostatistical interpolation techniques use statistics to produce advanced prediction surface including measures of accuracy of predictions. Kriging was chosen as an appropriate interpolation method for this project due to its ability to assume that the distance between sample points reflect a spatial correlation that can be used to justify variations in the surface. The predictions are derived from advanced weighted average technique to measure the relationship between the points. Generally, interpolation tool converts point data into raster format. Cell values generated by advanced statistical analysis can exceed the value range of sample points resulting in more realistic surface representation.

Kriging interpolation was used to analyze the data from six contaminant layers and model the results in a form of continuous surface representing concentration distribution throughout the area specified (in this case New York state). 

After six raster files were created, reclassification was performed to highlight the area that represent higher health risk category according to EPA’s breakpoint table compared to the rest of the state. Only two of the contaminants qualified for two AQI categories: ozone and PM10. Therefore, classification was performed only for these two pollutants using a threshold values from AQI table. For ozone, threshold value is equal to 70 ppm, meanwhile PM10 threshold value is 54 g/m3. 

In order to analyze the cumulative air pollution levels, the measurement units for each specific air pollutants had to be unified. For this purpose, a formula to convert concentration measurement values to AQI equivalents was used and it is expressed as follows:

![Screen Shot 2023-06-07 at 1 54 23 PM](https://github.com/RutaCodes/GeoSpatial/assets/111301407/1c4254dc-4e12-4fdb-ada7-e6c8be32d554)






