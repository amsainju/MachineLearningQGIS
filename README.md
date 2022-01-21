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
3.
