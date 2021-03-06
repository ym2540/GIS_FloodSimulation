# GIS-based Subdivision-Redistribution Simulation (GISSR)

![LM_NoProtect_Sandy+slr2100](https://user-images.githubusercontent.com/73183529/99480327-dd675e80-2925-11eb-89a7-c49b22791233.jpg)

### Table of Contents<br><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**1. Summary**](#1-Summary)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**2. Main Files and Jupyter Notebooks**](#2-Main-Files)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**3. Data**](#3-Data-Folder)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**4. Sample Results**](#4-Sample-Results)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**5. Flowchart of Processes**](#4-Processes-Flowchart)<br><br>

## 1. Summary

A storm surge induced flood simulation methodology, called GIS-based Subdivision-Redistribution (GISSR) methodology, is proposed for coastal urban environments. The methodology combines Geographical Information Systems (GIS) with Manning’s equation to calculate the volume of water flowing into the geographical area under consideration, and then redistributes it appropriately over that area. It uses as input the time histories of the storm surge height and of the tides along the coastline. It is capable of incorporating a variety of protective measures along the coastline, such as seawalls. For flood simulations in the future, it is straightforward to account for a prescribed value of sea level rise. The GISSR methodology is extremely efficient from the computational point of view, compared to existing flood simulation tools such as GeoClaw or ADCIRC that take several orders of magnitude more computing time because of the underlying complexity of their physical models. The methodology is found to be highly accurate by comparing its results to the actual extent of flooding that was observed during Hurricane Sandy in New York City (NYC), USA. Several examples demonstrating its capabilities are provided involving different protective measures in Lower Manhattan, NYC. The GISSR methodology is ideal for determining the optimal protective strategy for a coastal city because of its high computational efficiency since optimization requires a very large number of flood simulations.
This flooding model of Lower Manhattan was developed after this area experienced extreme flooding and devastation from Hurricane Sandy in 2012. Using historical trends of hurricanes in the area, elevation data and surface roughness, these files generate the extent of following throughout Lower Manhattan (south of 34th Street). The model also considers the increasing severity of storms and flooding due to climate change and projected sea level rise by 2050 and 2100. Code modelling the flooding of the subway system is avaiable upon request.


## 2. Main Files
The order to run the data to generate flood heights is Surface Volume CSV Processor.ipynb, Flood_Estimate.ipynb, then Flood Height to Raster Processor.ipynb. All the data needed to run each notebook without running the previous notebooks are already included in the Data and Sample_Output folders..
### Surface Volume Processor
To preprocess data for the Flood_Estimate code, Surface Volume CSV Processor should be run first to generate the surface volume csv files.
|     |     |
| --- | --- |
**Surface Volume CSV Processor.ipynb** | This code generates Surface Volume .csv files that are used in the Flood Estimate code, taking digital elevation model files (.TIFF) of the LMN’s division. The resulting .csv files contain the volume of water above the surface of the DEM at different heights in increments of 0.25m between 0-3m and in increments of 0.5m from 3.5-6.5m. Note, the user must have arcpy installed on their device for this code to run.
### Flood Height Estimator
The main code in this repository are the Flood Estimate notebooks, which generate flood height csv files that can be used to calculate damage. The code calculates surface volume functions that can relate the volume of water to the flood height at a given division. Using Manning's equation, it takes topographic data and storm parameter data to find the velocity and subsequently the volume of the water. These flood volumes are then redistributed by propagating to the nearby divisions, and the final flood heights for each division are determined.
|     |     |
| --- | --- |
**Flood_Estimate.ipynb** | Uses Sandy storm surge heights and time history as input values. 
**Flood_Estimate_from_Surge_Height.ipynb** | Uses surge height as an input value and artificially generates a time history for the storm for calculations.
**Flood_Estimate_Multiple_Storms.ipynb** | Uses warm and cold storm generated storms with time history as input values to perform calculations for multiple storms at once.
### Raster Processor
Finally, run Flood Height to Raster Processor to post process the flood heights and create a raster visualization of the flooding. 
|     |     |
| --- | --- |
**Flood Height to Raster Processor.ipynb** | To visualize the flood height results from Flood_Estimate.ipynb, this code processes the csv data into raster data (.TIFF). These .TIFF files can be inputted into ArcGIS to create a map of the area and corresponding flooding (see image above). Note, the user must have arcpy installed on their device for this code to run.


## 3. Data Folder
This folder includes files needed to run the Flood Estimate.ipynb
|     |     |
| --- | --- |
**LM_div18** | DEM files for Lower Manhattan divided into 18 divisions
**LM_div18_grouped** | DEM files grouped with the two divisions adjacent
**NewSurfaceVolume** | Surface volume csv files generated from the Surface Volume CSV Processor
**Surge_Data** | Storm parameters to calculate storm surge
**BigU_LES_all.csv** | Numbered segments of coastline corresponding to BigU placement
**LMN_Roughness.csv** | Surface roughness of Lower Manhattan
**LMN_Slope.csv** | Ground slope of Lower Manhattan
**LMN_div_low19.csv** |Adjusted division elevation for Lower Manhattan

## 4. Sample Results
This folder contains sample output files produced by running the notebooks in the repository.
|     |     |
| --- | --- |
**single_storm_flood_heights_\*.csv** | flood heights generated by single runs of Flood_Estimate.ipynb for cold and warm storms under unprotected and BigU conditions
**multiple_flood_heights_\*.csv** | flood heights for multiple storms generated by Flood_Estimate_Multiple_Storms.ipynb for cold and warm storms under unprotected and BigU conditions
**Flood_Rasters_\* folders** | raster files created by Flood Height to Raster Processor.ipynb showing locations of inundation

## 4. Processes Flowchart
See the flowchart below for the inputs and outputs of the notebooks and flood calculation processes.
![Storm-Copy of Copy of Page-1](https://user-images.githubusercontent.com/73183529/112877634-03033200-9095-11eb-831f-3562d6323854.jpg)
