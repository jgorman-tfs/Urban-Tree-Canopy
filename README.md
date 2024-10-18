# Urban-Tree-Canopy
This repository contains information related to creating the Urban Tree Canopy for cities in Texas. The web application is located here: https://texasforestinfo.tamu.edu/utc/ <br>

## Purpose
The Urban Tree Canopy project takes available public data and outlines tree canopy that exists within the Extraterritorial Jurisdiction (ETJ) and normal boundary of a munincipality. It also identifies and calculates areas "To Grow" using the CHHD layer, showing areas that could benefit from tree planting. The final shapefiles are uploaded to the website. 

## Key Components
Primary data includes the data that is used to identify tree canopy. This is primarily derived from publically available LiDAR data or from classified raster NAIP rasters using Deep Learning. <br>
Secondary data can be [downloaded](https://texasforestservice.sharepoint.com/sites/Share-ForestAnalytics/Documents/Forms/AllItems.aspx?viewpath=%2Fsites%2FShare%2DForestAnalytics%2FDocuments%2FForms%2FAllItems%2Easpx&id=%2Fsites%2FShare%2DForestAnalytics%2FDocuments%2FGeospatial%20Systems%2FJGorman%2FUrban%20Tree%20Canopy%20%28UTC%29&viewid=ce165790%2D6a2b%2D4d01%2Dae26%2Dde16078cd176) and includes the layers and tables used to define city boundaries and growth. <br>

## Methodology
The methods for this project are divided into two parts: (1) Data processing into tree canopy and  (2) further processing after QA/QC has been done. The best method for extracting tree canopy is with LiDAR, however pubicly available data is limited. The other method is by utilizing a trained deep learning model. The model has an F1 recall of 86% for tree canopy, however 300 points accuracy assessments show 90 - 98 accuracy depending on the city. Future improvements could be re-training the model depending on the area. 
## Part 1
### LiDAR
Texas Geographic Information Office (TxGIO) hosts an amazon web services bucket that is linked to each LiDAR dataset. The LiDAR Extractor script iterates through the selected cities of the ETJ, selects the appropriate LiDAR tiles, and downloads them from the bucket. <br>
1.) Download the LiDAR Index of the selected dataset and import the shapefile into ArcGIS Pro<br>
2.) Select ETJ boundaries that intersect the LiDAR tiles and export the selected ETJ's to the UTC gdb. <br>
3.) Change the names of the variables in the first cell. <br>
4.) run the second and third cells to execute the code<br>
5.) A newly created GDB will appear in your folders with the processed.<br>
6.) Download the most recent NAIP imagery <br>
7.) Start the QA/QC process, ensuring the polygons match up correctly with the NAIP imagery, deleting polygons as needed.<br>

### Raster Classification 
TxGIO also hosts NAIP imagery the same way throguh amazon s3 buckets. The Deep Learning Tree Canopy script will take the ETJ layer and iterate through the cities, downloading the appropriate NAIP tile using the NAIP Index, and applying the deep learning model. Pro tip: The NAIP tiles are always 4 band, JP2 Compressed rasters. The compressed county mosaics are MrSID 3 band, sometimes 4 band rasters. <br>
1.) Create a new ETJ layer from the cities you want to process and add to the map <br>
2.) Ensure the NAIP Index is loaded into the map<br>
3.) Update the variables to the appropriate file paths<br>
4.) The script will end with with 300 points for accuracy assessment<br>
5.) Perform the accuracy assessment and update the Accuracy spreadsheet<br>
6.) IF the accuracy is > 90%, that city can be used. <br>
7.) There's a couple improvements that need to be made : redirect the final polygons to a single, separate GDB ; some points (50 - 100) are put outside the raster ; need to improve the cleanup for temp files<br>

## Part 2
### UTC Processing
With the polygons QA/QC'd, you can now run the UTC Processing script. This script is slightly different than the previous because it operates on the feature classes within the GDB instead of the layers within the map. So make sure the Polygons from the previous step are in one geodatabase, and they are the names of the Cities with no spaces. <br>

That's it! 


