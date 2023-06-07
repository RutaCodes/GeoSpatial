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

The expression above was then simplified to represent a multiplier for each contaminant. For example:

![Screen Shot 2023-06-07 at 1 54 35 PM](https://github.com/RutaCodes/GeoSpatial/assets/111301407/e6ac7084-5c34-4342-bbe2-0bfd37765142)

Once simplification was done for all  contaminants, the values received were entered into the raster calculator to perform raster overlay and obtain a layer combining AQI values from all six contaminants and providing raster layer with cumulative AQI levels throughout the state. The final formula used in the raster calculator was as follows:

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/b03933bd-8377-417f-bab4-8b36cbea174c)
Figure 3. Raster calculator input

The layer created by raster calculator was the final output.

**3.	RESULTS**

*3.1 Ozone*

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/e4a89f4a-2ade-4a9d-b23e-3e40b9cbdf9f)
Figure 4. Ozone distribution

Ozone levels in New York state are considerably high. Concentration values fall in two AQI categories: Moderate and Unhealthy for sensitive groups. Parts of the Lower Hudson Valley, NYC and Long Island are exposed to higher levels of O3 concentration compared to the rest of the state. People living in this area are at a higher risk of experiencing health problems caused by air pollution (especially those who’s respiratory system is more sensitive to ambient air quality compared to general public). Living in the environment with this level of pollution increase the risk of experiencing short-term health effects like eye, nose, throat irritations, allergic reactions, headaches and various respiratory infections. 

*3.2 Sulfur Dioxide*

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/633527ec-d372-4534-83ce-d7b90da32eaa)
Figure 5. Sulfur Dioxide distribution

Sulfur dioxide concentration levels are very low. AQI equivalent for the concentration is equal to 1 which is at the very low end of the Good AQI Category representing very low sulfur dioxide concentration throughout the state. Two areas that are exposed to the highest levels of SO2 are Western New York and Long Island alongside New York City and Lower Hudson Valley.

*3.3 Nitrogen Dioxide*

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/5f5aa996-c667-4fff-a2da-38731025b8b5)
Figure 6. Nitrogen dioxide distribution

Nitrogen dioxide concentrations fall in the lower half of the Good AQI Category. Lower Hudson Valley, NYC and Long Island areas are exposed to higher NO2 concentration, however concentration levels are not at risk to cause any observable health effects.

*3.4 Carbon Monoxide*

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/62fdcc71-4311-4fc1-9b9f-6ccdebe87e38)
Figure 7. Carbon monoxide distribution

Similar to sulfur dioxide, highest air pollutant concentration levels are focussed in western and south-east side of the state affecting Western New York, New York City and part of Lower Hudson Valley regions. Meanwhile north side of Western Finger Lakes area have the lowest CO levels in the state.

*3.5 Particulate Matter 2.5*

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/dd35eb10-c61a-4cd7-b82e-037d5088b592)
Figure 8. Particulate matter 2.5 distribution

Areas experiencing the highest PM2.5 concentration levels are similar to SO2 and CO but effecting a wider area in the Western New York region.

*3.6 Particulate Matter 10*

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/a53d3874-1276-4b7e-8f41-b0ef4ad45659)
Figure 9. Particulate matter 10 distribution

PM10 concentration levels are relatively even throughout the state. Only Western New York region is exposed to higher level of concentration corresponding to Moderate AQI Category. The rest of the state can be classified by Good AQI Category. 

*3.7 Cumulative Air Pollution*

Combining all previous air contaminant distributions into a singular map, cumulative air pollution can be observed.

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/84659750-2ce3-41e4-8c5f-420f7fcb143d)
Figure 10. Cumulative air pollution

After adding separate distributions, one conclusive map was produced determining the areas where the state has the highest cumulative air pollutant concentrations. Cumulative distribution pattern is similar to SO2, CO and PM2.5 distribution affecting Western New York, Lower Hudson Valley, NYC and Long Island regions. Niagara, Erie, Chautauqua, Cattaraugus, Ulster, Orange, Dutchess, Rockland, Westchester, Bronx, New York, Queens, Kings, Richmond, Nassau and Suffolk counties have the highest air pollution levels in the state. Whereas northern side of the state has relatively low air pollution levels.

**4.	DISCUSSION** 

Areas with the highest air pollutant levels should be implementing significant air emission reduction programs to prevent any possible future damage for the population health. According to multiple studies done relating air pollution and health problems, areas with the highest air pollutant concentration levels are at the uppermost risk of experiencing short-term and long-term health concerns.

![image](https://github.com/RutaCodes/GeoSpatial/assets/111301407/30dcc2d1-82d9-4bac-8950-cf8c7958a219)
Figure 11. Possible health issues related to air pollution

Moreover, air pollution has a significant impact on the environment and ecosystems. Due to increased levels of ozone and PM10 concentrations in specific areas, it is safe to assume that corresponding areas will be experiencing greater environmental and health effects caused by those air pollutants.  

Generally, ozone particles are not emitted from a direct source. These particles are formed by chemical reactions between nitrogen oxides (NOx) and volatile organic compounds (VOC) in the presence of sunlight and are harmful outside the ozone layer. Ozone affects sensitive vegetation and ecosystems, including forests, parks and wilderness areas. Also, inhaling ozone can trigger a variety of problems like chest pain, airway inflammation. It can even damage lung tissue reducing lung function and worsening respiratory conditions including bronchitis, emphysema, and asthma, leading to increased medical care.

Particulate matter pollution can occur from natural (volcanoes, dust storms etc.) and man-made sources (burning of fossil fuels, operating power plants etc.).  Atmospheric aerosols (particulate-air mixture) affect the amount of incoming solar radiation. Due to that, aerosol climate effects cause the biggest uncertainty towards future climate predictions. Moreover, inhalation of particulate matter has been widely studied and proven to cause health problems like asthma, lung cancer, respiratory and cardiovascular diseases, premature delivery, birth defects, low birth weight, and even premature death.

EPA’s national and regional rules as well as Clean Air Act help to regulate emissions of certain air pollutants including setting threshold values for specific air contaminants that are applicable anywhere in the United States.

*4.2 Limitations*

First of all, any interpolation method is bound to the area of its sample points. For this study, it would have been not efficient to minimize the study area according to the region covered by sample points.  In order to get the distribution throughout the entire state, the original interpolation results were extended to fit the state boundaries. However, in doing so some uncertainty was introduced to the results. 

Furthermore, a limited amount of sample points were available for this analysis. Therefore, results have some inaccuracies that could have affected overall results. To achieve more accurate results, more sample point should be used for interpolation. In that way errors would be minimized and conclusive results could be made in order to make any future suggestions for pollutant emission control.

In addition, possible environmental and health effects caused by a specific air contaminant could be analyzed to examine any correlations. Numerous health conditions could be linked to air contaminant type if any positive correlation could be proven. For example, analyzing if there is any relationship between annual rates of asthma discharge as well as asthma emergency visits and distribution of air pollution concentrations. Geospatial Analyst tool could be used to calculate correlation coefficient determining any patterns between air pollution and asthma cases. Moreover, the same principle could be applied to various health concerns as well as any environmental effects that are even remotely linked to air pollution.
 
**5.	CONCLUSIONS**

New York State Ambient Air Quality Report for 2015 was used as a data source for this project. Data was configured and analyzed. Surface distribution was implemented for six air pollutants: ozone, sulfur dioxide, nitrogen dioxide, carbon monoxide, particulate matter 2.5 and 10. Spatial interpretation for concentration levels of each pollutant was achieved using Kriging interpolation tool. After distribution for each pollutant was determined and conversion from concentration data into AQI values was done, all six contaminant contributions were combined resulting in cumulative pollution levels in New York state concluding Western New York, Lower Hudson Valley, NYC and Long Island regions as the highest risk zones for possible health effects caused by air pollution. 


**References**

1.	http://www.air-n-water.com/air-pollution.htm
2.	https://en.wikipedia.org/wiki/Air_pollution
3.	https://en.wikipedia.org/wiki/Air_quality_index
4.	http://www.dec.ny.gov/chemical/8406.html
5.	https://www.esri.com/news/arcuser/0704/files/interpolating.pdf
6.	https://www3.epa.gov/airtoxics/3_90_022.html
7.	https://en.wikipedia.org/wiki/Particulates
8.	Int. J. Environ. Res. Public Health 2014, 11(5), 4845-4869; doi:10.3390/ijerph110504845

Raw data retrieved from:
http://www.dec.ny.gov/docs/air_pdf/2015airqualrpt.pdf
