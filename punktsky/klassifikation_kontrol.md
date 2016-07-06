#Classification checks

Some of the tests listed below are similar to tests performed earlier. This is because the suggested workflow for larger contracts contains a two-step delivery where geometric adjusted blocks are deliverd first for geometry control and while the Agency is checking the geometry, the provider can continue with the classification. 

**LAS format**
Methos: See LAS check under <link til geometri-dokument>

The LAS files must be formatted properly
Does it contain R,G,B values (if flown at daytime)?

**File naming and file count**
Method_ See LAS check under <link til geometri-dokument>
Accepted when: 
Description:


**Classification count**
Method: Automatic, module: qc_wrap/xxxx
All classes should be present in the received material. Classes not in the specification should not be present. The module reports the amount of points in each class for a tile. The result is reported to the database. All classes for a block should be present. Distribution across tiles should be homogeneous. 

**Bridge control**
Method: Semi-automtic

Class 17 (bridge) should be present in proximity to bridges. Therefore points where we expect a bridge to be present based on available database material are extracted and compared with the point cloud (e.g. where two roads intersect at different height levels, where road intersect railroad, where road intersect river/stream etc. Also points from the 2007 dataset coded as “bridge” are used).

Test is run on a tile level. Tiles with a to-be-determined percentage of "good" bridge-compares are accepted. The remainder will be checked manually or if a large pattern is spotted, the delivery is rejected.

**Edge control**

Method: Manual, spotwise manual check for the delivery

Classification errors have previously been spotted along the tile edges. Therefore a check is done between tiles along the edge to see if terrain meets terrain and no systematic slope is detected. When encountered this has proven to be a systematic error type, therefore only spot wise checks needed. 

**Road delta check**

Method: Semi-automatic

The road centre lines are used. If there is a sudden z-difference along the road it should be investigated. The module reports the result to a database to be visualised in a GIS system. There will be a lot of false positives (road work, roads close to slopes) so if no systematic patterns are seen advise is to do on ly spotwise test.

**Spike check**

Method: Automatic, module: qc_wrap/spike_check

Checks for spikes (sinks, high points). The result is reported to a database. Unusual patterns are investigated. 

Expected patterns are 

* Inside forrests
* Along side breakwaters
* On rocky surfaces
 
If no unusual patterns are reported the data is accpeted. *NB! The result of this test is used to remove the spikes reported in the DEM generation process* <indsæt link til dok>

**Vegetation below building polygon**

Method: Semi-automatic, module: qc_wrap/Xxx

High, medium and low vegetation is counted for each building polygon, but only those points with z below the building polygon’s average z. If many points are classified as vegetation (inside buildings) there is reason to investigate further. 

**Visual check, Fugro Viewer**

Method: Manual procedure (Fugro Viewer)

* Check for at least one classified bridge outside delivered bridge point file.
* Check that class low veg., medium veg. and high veg. are in e.g. forest
* Check that buildings are properly classified

**Visual check, QGIS**

Method: Manual procedure (QGIS, GDAL)

* Calculate hillshade for both DTM and DSM with gdal. 
* For DSM, Add high tension lines from FOT and look for “barriers” cutting through the landscape. 
* Check at a glance for artifacts (spikes, steps, sinks, etc.)
* Look specifically along tile borders for steps.
* Check that no ringing point are within the used classes.
* No artifacts are present.

**Classification check**

Method semi-automatic, module: qc_wrap/classification_check

* A certain amount of terrain points inside building polygons are expected but the majority should be classified as “building”. Check that this is the case. 
* Unclassified points in building polygons can occur but not in large numbers.

**Compare derived terrain grid with 2007 data**

Method semi-automatic, module: qc_wrap/diff

The grid model from 2007 and 2014/15 are compared (subtracted). Areas with known/expected difference (open pit mining areas) are excluded from the comparison. Larger areas with deviations are isolated and inspected.
