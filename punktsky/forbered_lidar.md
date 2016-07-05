# Lidar preparations

_This process handles following inhouse works...:_ 

* Pre-mission
* Mission Management
* Flight checks

_Structure of data: Data to/from the supplier is stored on a common accessible location (presently stored on the m-drive). The sub-folders “FromSupplier” and “ToSupplier” works as inbox and outbox for all data delivered from/to the supplier. In this way it can always be seen when and what data has been delivered. All subfolders starts with a date in the iso format (YYYYMMDD) so the can be sorted by date. From here the data is later on copied to the relevant blocks_

_The result of this check is a screening of the dataset to ensure that it is worthwhile to proceed with further evaluation_

**Pre-mission**

Before the data acquisition mission can commence it is important to check that the mission plan made by the contractor will result in usable data. This check covers a number of different aspects, which result in the following list of things to be checked:

**Survey method**

Method: Manual procedure

It is checked that the mission has been planned using LiDAR equipment matching the contract
  
**Collection Area**

Method: Manual Procedure

It is checked that the planned mission covers the entire area. Strips are transformed into swath-polygons that are checked against the tiles delivered to the contractor
  
**Placement of ground control points/patches (GCP)**

Method: Manual Procedure
  
It is checked that there is an adequate number and placement of vertical ground control points and control patches
  
**Block size**

Method: Manual Procedure
  
It is checked that block sizes only in special cases exceed 40/40 km e.g. an island that is slightly longer than 40 km
  
**Placement of cross strips**

Method: Manual Procedure
  
It is checked that every flight strips has at least two cross strips. There may be examples of blocks where two cross strips is not possible or does not make sense. In this case only one cross strip is required.

**Scan angle and overlap**

Method: Manual Procedure
  
It is checked that there are no gaps in between the flight strips. 


## Mission Management

**Atmospheric Conditions**
  
Method: Semi-automatic, module METAR_logger
  
LiDAR is a fairly robust mapping technology able to acquire data when other technology have trouble. LiDAR works well both at nights and also with cloud cover, but there are atmospheric conditions that do hamper good data acquisition. Such conditions are strong winds that disturb flight paths and clouds or rain between the aircraft and the ground. These conditions are logged throughout the data acquisition period.   

Athmospheric data for the relevant flight days are extracted from the database and evaluated 

**Ground Conditions**

Method: Manual Procedure
  
Ground conditions are very important for securing good and usable data. Unacceptable ground conditions are basicly water or snow on the ground. It is also the ground conditions that dictate when data acquisition can commence. The contract states a date at which data acquisition can start but if the ground conditions are deemed free of snow and water GST may choose to allow the contractor to commence the acquisition period
  
**Tidal conditions**

Method: Semi-automatic, module: TIDAL_logger

Tidal conditions are observed. This is somewhat more easy since tidal shifts are very regular and easily found in tidal charts. But it is important to note that tidal conditions needs to be observed in conjunction with the atmospheric conditions and this especially for low-lying coastal areas where strong winds can change the sea level.

Tidal conditions are determined by the time of flight. If the data reveals problems regarding tidal conditions data will be retrieved from Kystdirektoratet. 

## Flight Checks

_Flight checks are introduced at an early state to ensure that obvious errors are found before they can delay production. Findings and dates are noted in the production spread sheet and deliveries are rejected or approved._

**Overlap**

Method: Semi-automatic, module: TrjOLap

Trajectories are displayed in a GIS program and visually inspected. Buffers are generated (determined by the used scanner equipment). If lines are missing or does not have sufficient overlap trajectories are not approved.

**Density (calculated)** 

Method: Semi-automatic, module: TrjDense

From the trajectories the (theoretic) density is calculated.

**Visual Inspection**

Method: Manual Procedure

Data is viewed upon at a glance. Does anything look out of the ordinary? Any irregularities are noted in process sheet. 

**GPS / IMU plot check**

Method: Manual Procedure

Plots from the GPS/IMU processing software are checked for suspicious behaviour. 

## Pont Cloud Receival Checks

**LAS format**

Method: Semi-automatic, module: LAScheck (LAStools)

The LAS files must be formatted properly. 

**File naming and count**

Method: Semi-automatic. Module: QGIS, GST_DIS (Tile_check), ScanDir

"Tile_check" checks delivered tiles against a tileindex shp file. The result is reviewed. Accepted when all tiles in a block are delivered.

**Density and Data Voids**

Method: Automatic, qc_wrap/density

The module "qc_wrap/density" reports the 100m cells within a 1km tile with the lowest point density that does not intersect lakes or sea. Accepted when all 1km tiles have no 100m cells with less than 4ppm2. 100m2 with lower ppm2 may be accepted if the cell is coinciding with wetlands or equivalent. 

**Visual sensor inspection**

Method: Manual procedure

These checks are very focused on the specific sensors used for the project. For this reason these are not checks done on the entire data set but more random samples done on each sensor to ensure that the sensors used are working within specified parameters.

* Sensor mechanics
* Multiple discrete
* Scanner artefacts

The sensor is evaluated against the agreement with the supplier

**GCP accuracy** 

Control report from supplier is checked to see if it meets specification

