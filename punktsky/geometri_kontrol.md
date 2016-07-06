#Geometry Checks

This process ensures that the received data meets the expectations set forth in the agreement with the supplier. 

Experience has shown that data which has been geometrically poorly adjusted is difficult to classify correctly. 


##Geometry checks (Strip adjustments)

**CRS (Coordinate Reference System)**
Method: Manuel check (using LAS check)
All files delivered must be in the right projection, datum and height system. While this requirement is not checked explicitly, non compliance will be revealed by the geometric control procedures.


##Precision

**Height Precision (overlap, on road surface)**

Method: Automatic check, module: z_precision_roads (qc_wrap.py road)

Neighboring strips are interpolated onto each other on flat surfaces and relevant statistics are reported. To identify areas which can be assumed to be flat, road centre lines are used. Road centre lines are stored in database with relevant statistics as attributes. The centre lines are colorised using a suitable legend highlighting problematic areas. Accepted when specs according to contract are met

**Planimetric precision on building ridges**

Method: Automatic check, module: z_precision_buildings (qc_wrap.py roof_strips)

Neighboring strips are interpolated onto each other based on building roof ridges. the difference between strips are calculated. If a shift (X,Y) has occurred it will show as significantly worse statistic.Building polygons are stored in database with relevant statistics as attributes.
 
**planimetric precision on building corners**

Module: z_precision_buildings (qc_wrap.py xy_precision)

Neighboring strips are interpolated onto each other on building polygons. If a shift (X,Y) has occured it will show as significantly worse statistic values as the z_check_roads check. Building polygons are stored in database with relevant statistics as attributes. 

##Accuracy

**FOT Building roof ridges**
 
Method: Automatic, module: roof_ridge_alignment

Roof ridges are estimated by intersecting detected surfaces within building polygons. These roof ridges are intersected with the containing polygon - ideally in the center of a polygon edge. The distance from the center of of the polygon edge to the intersection is reported. This yields a combined accuracy estimate of a) the building polygon b) the lidar point cloud and c) the geometric integrity of the building. Estimated (calculated) roof ridges are stored in database with relevant statistics as attributes which can be visualised and evaluated in a GIS system.
 
**FOT Building corners** 

Method: Automatic, module: xy_accuracy_buildings

Building edges and building corners are estimated from the point cloud. These points are transformed onto the photogrametrically measured polygon. The result of the transformation is reported. Building polygons are stored in database with relevant statistics as attributes.

**GCP Building roof ridges**
Method: Semi automatic, module: Find_planes (New name: roof_ridge_alignment)

The find_planes module is run with a custom data set prepared specifically from surveyed data. Accepted when the spec/contract conditions are met.

**GCPs checked against point cloud**

Method: Automatic, module: Z_check_abs (New name: z_accuracy)

Z_check_abs interpolates features in the point cloud. Result of the interpolation is reported as GCPs stored in database with relevant statistics as attributes. Accepted when the spec/contract conditions are met.

**Road centre lines (FOT) checked against point cloud.**

Method: Automatic, module: z_accuracy

As above

**Road centre lines GCP (concept - to be tested) **

Method: Automatic check, module:z_accuracy

Surveryors measurement of road centre lines. These stretches are measured automatically and can be used as above. 

---

NB! Dette dokument er en lættere omskrivning fra originalen [hér](https://docs.google.com/document/d/1L5Bj4IGPBinCyzcHFO4n7pemHKG-DdtMz3xG3NMcVq4/edit#heading=h.8h3hjk9j9ytk)


