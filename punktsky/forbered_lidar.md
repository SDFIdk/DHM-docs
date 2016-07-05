# Forbered Lidar

_Denne proces håndterer alle arbejder, som leder op til at styrelsen modtager data fra producent._

* Pre-mission
* Mission Management
* Flight checks


_Structure of data_

_Data to/from Aerodata is stored on a common accessible location (presently stored on the m-drive)_

_The sub-folders “FromSupplier” and “ToSupplier” works as inbox and outbox for all data delivered from/to the supplier. In this way it can always be seen when and what data has been delivered. All subfolders starts with a data in the iso format (YYYYMMDD) so the can be sorted by date._ 

_From here the data is later on copied to the relevant blocks_

 

## Pre-mission

Before the data acquisition mission can commence it is important to check that the mission plan made by the contractor will result in usable data. This check covers a number of different aspects, which result in the following list of things to be checked:

* Survey method

  Method: Manual procedure
  
  Description: It is checked that the mission has been planned using LiDAR equipment matching the contract
  
* Collection Area

  Method: Manual Procedure
  
  Description: It is checked that the planned mission covers the entire area. Strips are transformed into swath-polygons that are checked against the tiles delivered to the contractor
  
* Placement of ground control points/patches (GCP)

  Method: Manual Procedure
  
  Description:It is check that there is an adequate number and placement of vertical ground control points and control patches
  
* Block size

  Method: Manual Procedure
  
  Description:It is checked that block sizes only in special cases exceed 40/40 km e.g. an island that is slightly longer than 40 km
  
* Placement of cross strips

  Method: Manual Procedure
  
  Description:It is checked that every flight strips has at least two cross strips. There may be examples of blocks where two cross strips is not possible or does not make sense. In this case only one cross strip is required.

* Scan angle and overlap

  Method: Manual Procedure
  
  Description:It is checked that there are no gaps in between the flight strips. 


## Mission Management

* Atmospheric Conditions
  
  Method: Semi-automatic, module METAR_logger
  
  Description: LiDAR is a fairly robust mapping technology able to acquire data when other technology have trouble. LiDAR works well both at nights and also with cloud cover, but there are atmospheric conditions that do hamper good data acquisition. Such conditions are strong winds that disturb flight paths and clouds or rain between the aircraft and the ground. These conditions are logged throughout the data acquisition period.   

  Athmospheric data for the relevant flight days are extracted from the database and evaluated 

* Ground Conditions

  Method: Manual Procedure
  
  Description: Ground conditions are very important for securing good and usable data. Unacceptable ground conditions are basicly water or snow on the ground. It is also the ground conditions that dictate when data acquisition can commence. The contract states a date at which data acquisition can start but if the ground conditions are deemed free of snow and water GST may choose to allow the contractor to commence the acquisition period
  
  