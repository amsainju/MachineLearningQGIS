# Machine Learning Tutorial: Classification on Satellite Imagery in QGIS

- [Introduction to Satellite Images](#introduction-to-satellite-imagery)
- [QGIS](#qgis)
- [Installation](#installation)
- [Flood Mapping in QGIS](#flood-mapping)

# Introduction to Satellite Imagery

Our planet is continuously being observed by satellites. Sattelite Imagery consists of pixels. Each pixel is defined by 3 main values: intensity of redness, greenness and bluness. In terms of sattelite images, these values are know as band. Based on the type of satellite image, we can have multiple bands. For example, LandSat_8 satellile images has 8 different bands.
More information on Landsat_8 is provided in follwoing link:
https://landsat.gsfc.nasa.gov/satellites/landsat-8/

![Satellite view of MTSU](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/MTSU.png?raw=true#center)
Satellite view of Middle Tennessee State University

In this tutorial we are interested in the follwoing bands:
- Red Band   
- Green Band
- Blue Band

Each of the color band has intensity range of 0 to 255. The value 0 represents lowest intensity and the value of 1 represents highest intensity.
You can play with the following link to see how changing the intensity of these bands changes the resulting color.
https://www.colorspire.com/rgb-color-wheel/

# QGIS
GIS refers to the Geographical Inforamtion System. QGIS is a free open-source tool that has the capabilities to handle and process geographical data such as sattelite imagery. In this tutorial, we will use QGIS with another open-source library called Orfeo ToolBox to perform classification task in satellite images. Orfeo Toolbox provides machine learning capbalilities to QGIS.

# Installation
This section provides QGIS installation guide and integrating Orfeo toolbox in QGIS.
#### Installing QGIS
- QGIS Download Link: [QGIS-3.22.3](https://qgis.org/downloads/QGIS-OSGeo4W-3.22.3-1.msi/)
- Orfeo ToolBox download Link: https://www.cs.mtsu.edu/~asainju/AIWorkshop/OTB-6.6.1-Win64.zip

#### Steps:
1. Download GQIS and Orfeo ToolBox
2. Run the QGIS installer and follow the prompt.
3. Setting up Orfeo ToolBox
    1. unzip OTB-6.6.1-Win64.zip (Say C:\OTB-6.6.1-Win64)
    2. Open QGIS and Goto Setting->Options
![QGIS](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/QGIS_OTB_Setting1.png?raw=true#center)
    3. Next, click on the Processing Tab and expand Providers -> OTB as shown in the image below:
![QGIS](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/QGIS_OTB_Setting2.png?raw=true#center)
    4. Provide the path to the OTB application folder in "OTB application folder" textbox.
    5. Provide the path th the OTB in "OTB folder" textbox.
    6. Press "OK".
4. You have sucessfully integrated OTB in QGIS. To verify this, check the "Processing Toolbox". You should see various tools under OTB such as Callibration, Image Filtering, Learning and so on.
![QGIS](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/QGIS_OTB_Setting3.png?raw=true#center)

# Flood Mapping in QGIS
Given an earth observation imagery, flood mapping refers to finding the extent of the flood water in the given area. Flood extent mapping plays a crucial role in addressing grand societal challenges such as disaster management, national water forecasting, as well as energy and food security. For example, during Hurricane Harvey floods in 2017, first responders needed to know where floodwater was in order to plan rescue efforts. In national water forecasting, detailed flood extent maps can be used to calibrate and validate the NOAA National Water Model (National Oceanic and Atmospheric Administration 2018). Mannually generating such flood maps by sending a field crew on the ground to mark down the floodwater extent on a map can be time-consuming and expensive.

In this tutorial, we will learn to generate flood maps using machine lerning method in QGIS. First, we need to get the flood dataset. You can download the dataset using the following link:  [Flood Data](https://www.cs.mtsu.edu/~asainju/AIWorkshop/Projects/Flood.zip).

The zip file includes:
1. QGIS Project file: OpenProject.qgz
2. data folder that includes:
    1. aerialImagery.tif (satellitle imagery of the flooded area in North Carolina)
        - satellite imagery (raster data) are usually stored in tif file format.
    2. aerialImageryWithElevation.tif (Satellitle image with Elevation data)
    3. traingPolygons files (A shapefile to store polygon data)
3. model folder
    - currently empty
    - we can use it store the model file learnt using QGIS and OTB.
4. results folder
    - currently empty
    - we can use it to store the predicted flood extent result

### Steps to generate flood extent map:
1. Open "OpenProject.qgz" by double clikcing it.
2. It opens QGIS with the 3 data from the data folder, each as a seperate layer. You should be able to see the data in the "Layers" section as shown in the image below.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping1.png?raw=true#center)
3.
