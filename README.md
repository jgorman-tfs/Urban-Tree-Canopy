# Urban-Tree-Canopy
This repository contains information related to creating the Urban Tree Canopy for cities in Texas. The final web application is located here: https://texasforestinfo.tamu.edu/utc/ <br>

## Purpose
The Urban Tree Canopy project takes available public data and outlines tree canopy that exists within the Extraterritorial Jurisdiction (ETJ) and normal boundary of a munincipality. It also identifies and calculates areas "To Grow" using the CHHD layer, showing areas that could benefit from tree planting. The final shapefiles are uploaded to the website. 

## Key Components
Primary data includes the data that is used to identify tree canopy. This is primarily derived from publically available LiDAR data or from classified raster NAIP rasters (method coming soon). <br>
Secondary data can be [downloaded](https://texasforestservice.sharepoint.com/sites/Share-ForestAnalytics/Documents/Forms/AllItems.aspx?viewpath=%2Fsites%2FShare%2DForestAnalytics%2FDocuments%2FForms%2FAllItems%2Easpx&id=%2Fsites%2FShare%2DForestAnalytics%2FDocuments%2FGeospatial%20Systems%2FJGorman%2FUrban%20Tree%20Canopy%20%28UTC%29&viewid=ce165790%2D6a2b%2D4d01%2Dae26%2Dde16078cd176) and includes the layers and tables used to define city boundaries and growth. <br>

## Methodology
The methods for this project are divided into two parts: Data processing into tree canopy and further processing after QA/QC has been done. The best method for extracting tree canopy is with LiDAR, however pubicly available data is limited. The other method is by training a raster classifier (usually Random Trees or Support Vector Machine). The issue with this method is that accuracy results are extremely variable, the training process can be time consuming, and there are automation limitations.
## Part 1
### LiDAR
TxGIO hosts an amazon web services bucket that is linked to each LiDAR dataset. The LiDAR Extractor script iterates through the selected cities of the ETJ, selects the appropriate LiDAR tiles, and downloads them from the bucket. <br>
1.) Download the LiDAR Index of the selected dataset and import the shapefile into ArcGIS Pro<br>
2.) Select ETJ boundaries that intersect the LiDAR tiles and export the selected ETJ's to the UTC gdb. <br>
3.) Change the names of the variables in the first cell. <br>
4.) run the second and third cells to execute the code<br>
5.) A newly created GDB will appear in your folders with the processed.<br>
6.) Download the most recent NAIP imagery <br>
7.) Start the QA/QC process, ensuring the polygons match up correctly with the NAIP imagery, deleting polygons as needed.<br>

### Raster Classification 
Coming Soon!<br>

## Part 2
### UTC Processing
With the polygons QA/QC'd, you can now run the UTC Processing script. The only thing you need to do here is assign the final gdb location and run the cells. <br>

That's it! 


