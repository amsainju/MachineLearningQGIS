# Machine Learning Tutorial: Classification on Satellite Imagery in QGIS

- [Introduction to Satellite Images](#introduction-to-satellite-imagery)
- [QGIS](#qgis)
- [Installation](#installation)
- [Flood Mapping in QGIS](#flood-mapping)

# Introduction to Satellite Imagery

Our planet is continuously being observed by satellites. Satellite Imagery consists of pixels. Each pixel is defined by 3 main values: intensity of redness, greenness and blueness. In terms of satellite images, these values are know as band. Based on the type of satellite image, we can have multiple bands. For example, LandSat_8 satellite images has 8 different bands.
More information on Landsat_8 is provided in following link:
https://landsat.gsfc.nasa.gov/satellites/landsat-8/

![Satellite view of MTSU](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/MTSU.png?raw=true#center)
Satellite view of Middle Tennessee State University

In this tutorial we are interested in the following bands:
- Red Band   
- Green Band
- Blue Band

Each of the color band has intensity range of 0 to 255. The value 0 represents lowest intensity and the value of 1 represents highest intensity.
You can play with the following link to see how changing the intensity of these bands changes the resulting color.
https://www.colorspire.com/rgb-color-wheel/

# QGIS
GIS refers to the Geographical Information System. QGIS is a free open-source tool that has the capabilities to handle and process geographical data such as satellite imagery. In this tutorial, we will use QGIS with another open-source library called Orfeo Toolbox to perform classification task in satellite images. Orfeo Toolbox provides machine learning capabilities to QGIS.

# Installation
This section provides QGIS installation guide and integrating Orfeo toolbox in QGIS.
#### Installing QGIS
- QGIS Download Link: [QGIS-3.22.3](https://qgis.org/downloads/QGIS-OSGeo4W-3.22.3-1.msi/)
- Orfeo Toolbox download Link: https://www.cs.mtsu.edu/~asainju/AIWorkshop/OTB-6.6.1-Win64.zip

#### Steps:
1. Download GQIS and Orfeo Toolbox
2. Run the QGIS installer and follow the prompt.
3. Setting up Orfeo Toolbox
    1. unzip OTB-6.6.1-Win64.zip (Say C:\OTB-6.6.1-Win64)
    2. Open QGIS and Go to Setting->Options
![QGIS](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/QGIS_OTB_Setting1.png?raw=true#center)
    3. Next, click on the Processing Tab and expand Providers -> OTB as shown in the image below:
![QGIS](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/QGIS_OTB_Setting2.png?raw=true#center)
    4. Provide the path to the OTB application folder in "OTB application folder" textbox.
    5. Provide the path to the OTB in "OTB folder" textbox.
    6. Press "OK".
4. You have successfully integrated OTB in QGIS. To verify this, check the "Processing Toolbox". You should see various tools under OTB such as Calibration, Image Filtering, Learning and so on.
![QGIS](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/QGIS_OTB_Setting3.png?raw=true#center)

# Flood Mapping in QGIS
Given an earth observation imagery, flood mapping refers to finding the extent of the flood water in the given area. Flood extent mapping plays a crucial role in addressing grand societal challenges such as disaster management, national water forecasting, as well as energy and food security. For example, during Hurricane Harvey floods in 2017, first responders needed to know where floodwater was in order to plan rescue efforts. In national water forecasting, detailed flood extent maps can be used to calibrate and validate the NOAA National Water Model (National Oceanic and Atmospheric Administration 2018). Manually generating such flood maps by sending a field crew on the ground to mark down the floodwater extent on a map can be time-consuming and expensive.

In this tutorial, we will learn to generate flood maps using machine learning method in QGIS. First, we need to get the flood dataset. You can download the dataset using the following link:  [Flood Data](https://www.cs.mtsu.edu/~asainju/AIWorkshop/Projects/Flood.zip).

The zip file includes:
1. QGIS Project file: OpenProject.qgz
2. data folder that includes:
    1. aerialImagery.tif (satellite imagery of the flooded area in North Carolina)
        - satellite imagery (raster data) are usually stored in tif file format.
    2. aerialImageryWithElevation.tif (Satellite image with Elevation data)
    3. trainingPolygons files (A shapefile to store polygon data)
3. model folder
    - currently empty
    - we can use it store the model file learnt using QGIS and OTB.
4. results folder
    - currently empty
    - we can use it to store the predicted flood extent result

### Steps to generate flood extent map:
1. Open "OpenProject.qgz" by double clicking it.
2. It opens QGIS with the 3 data from the data folder, each as a separate layer. You should be able to see the data in the "Layers" section as shown in the image below.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping1.png?raw=true#center)
3. The training polygon contains two different type of polygons: Dry and Flood.
4. You can right click on the polygon and select "Open Attribute Table".
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping2.png?raw=true#center)
5. It will then open an attribute table that shows you the information on the polygons. There are two attributes: "id" and 'label'. Each polygon has an id and a label.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping3.png?raw=true#center)
6. Polygons on top of the flooded area are provided the label "1"(one) whereas polygons on the top of the dry area labeled "0" (zero).  

# Adding training Polygon

7. You can create more training polygon by clicking on the "Toggle Editing" button. Make sure you are selecting the "trainingPolygon" layer.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping5.png?raw=true#center)
8. After you click the "Toggle Editing" button, "Add Polygon Feature" button will get activated. Click on it and you can draw new polygon on top of the satellite image.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping6.png?raw=true#center)
9. To draw the new polygon: left click on the satellite image to create a vertex of new polygon. You can create as many vertex as you like. After you are done perform right click. A dialogue box will appear that will ask you the id and label of the new polygon as shown in the image above.
10. Provide the new id and label. For example id-> 5 and label-> 0 (to indicate dry polygon).
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping7.png?raw=true#center)
11.Finally after you press "Ok". A new polygon will be added.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping8.png?raw=true#center)
12. Similarly, you can add new polygon in the flooded area.
13. After you are done adding the new polygons. YOU MUST SAVE THE CHANGES. To do that press the save layer edit button (floppy disk icon).
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping9.png?raw=true#center)
14. Click the "Toggle Editing" button again to get out of the edit mode.

# Training a Decision Tree Model
15. To train a decision tree model, we will be using the OTB tool. In the "Processing Toolbox" expand OTB->Learning and double click "TrainImageClassifier" tool as shown below.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping10.png?raw=true#center)
16. In the "Input Image List" click on "..." button and select "aerialImagery" and press "OK". "aerialImagery" layer is a satellite image with Red, Green and Blue channel/band.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping11.png?raw=true#center)
17. Next, in the "Input Vector Data List" click on "..." button and select "trainingPolygon" and press "OK" (similar to step 16). Training polygons are the vector data.
18. Skip all the inputs fields that are indicated optional.
19. In the "Field Name" type "label" (without quotation marks). Remember from step 9 and 10, each polygon has a attribute called label to indicate dry or flood.
20. In "Classifier to use for training" field, select "dt" from the dropdown menu. "dt" indicates decision tree.
21. In the "Output model" file provide the full path and the model name. Example: "C:/AIWorkshop/Flood/model/decisionTree.model"
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping12.png?raw=true#center)
22. Finally, press "run" button at the button right.
23. You may see something like this if the training was successful:
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping13.png?raw=true#center)
24. Check the location where decisionTree.model should be create. In our example it is "C:/AIWorkshop/Flood/model/". It should contain the file decisionTree.model.

# Running the Decision Tree Model
25. To use the trained decision tree model for classifying the sattelite image, we will use another OTB tool.
26. In the "Processing Toolbox" expand OTB->Learning and double click "ImageClassifier" tool as shown below.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping14.png?raw=true#center)
27. In the "Input Image" field select "aerialImagery".
28. In the "Model file" field provide the path to the model (i.e: "C:/AIWorkshop/Flood/model/decisionTree.model")
29. skip all the section that are indicated as optional.
30. In the "Output Image" field provide the full path of the Output Image (name with location). Example: "C:/AIWorkshop/Flood/result/decisionTreePredicted.tif". Satellite image are store in ".tif" file format.
31. Unthe the check box (open output file after running algorithm) for "Confidence map" field. We can leave it blank. The final parameters will look like this:
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping15.png?raw=true#center)
32. Press the "run" button. You may see a log output like this:
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping16.png?raw=true#center)
33. We can ignore the warning. Close the "ImageClassifer" window.
34. You should see a new layer "DecisionTreePredicted". It is the classification result on the satellite image based on decision tree model.
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping17.png?raw=true#center)
Decision Tree prediction result on "aerialImagery.tif" file
# Training Decision Tree model with "aerialImagerywithElevation"
35. We can notice that the decision tree predicted result does not look good. It maybe because of various reasons:
a. The training polygon were well selected.
b. There maybe some ambiguous area where the model is not performing well. For example, pixel color of tree on top of flooded area looks very similar to tree on dry area.
36. To reduce this ambiguity, we introduce a elevation as a feature. Due to gravity, flood water will always flow down to the lowest elevation.
37. You redo step 15 to 34 again but replace "aerialImagery" with "aerialImagerywithElevation".
38. You should be able to see the following result:
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping18.png?raw=true#center)
39. You can observe the prediction is much better now.
40. You can also change the color coding of flood and dry pixel. Right click predicted layer. Click on properties. Click on Symbology tab. On Render type, select "Paletted/Unique values". Click on "Classify" button. Select your desire color and press "OK".
![FLoodMapping](https://github.com/amsainju/MachineLearningQGIS/blob/main/images/FloodMapping19.png?raw=true#center)
