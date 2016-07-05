Kontrolflow kan ses her:[[Fil:Kontrolflow.pptx]]

==Projektkontrol==
Se også [[Time_Schedule#Deliverables|Time Schedule]].a
===Flight Plan===
Kontrolflow til projektkontrol kan ses her: [[Fil:Kontrolflow_projektplan.pptx]]

MatchWare version: [[Fil:ProjectControl_v0 01.zip]] (se også [[Pseudokode: Project Control|pseudokode]])
# Pre-Flight
## Survey method [[Product_Specification#Req._1._Survey_Method|(Req.1)]]
## Collection Area [[Product_Specification#Req._5._Collection_Area|(Req.5)]]
## GCP placering (JVF. projektplan)
## Block størrelse (JVF. projektplan)
## Tværstribeplacering [[Product_Specification#Req._10._Vertical_Accuracy |(Req.10)]]
## Scan angle [[Product_Specification#Req._8._Swath_Overlap|(Req.8)]]
Pre-Flight accepteres fra GST inden for 5 arbejdsdage ([[Time_Schedule#Flight_planning_2|Flight Planning]])
# Post-Flight
## Atmospheric Conditions [[Product_Specification#Req._2._Atmospheric_Conditions|(Req.2)]]
## Ground Conditions [[Product_Specification#Req._3._Ground_Conditions|(Req.3)]]
## Vegetation Conditions [[Product_Specification#Req._4._Vegetation_Conditions|(Req.4)]]
## Tidevand [[Product_Specification#Req._6._Time_of_Flight|(Req.6)]]
## Overlap (10 %) [[Product_Specification#Req._8._Swath_Overlap|(Req.8)]]
## Cross line (pr. 20 km) [[Product_Specification#Req._9._Cross_Lines|(Req.9)]]
## Collection Report [[Product_Specification#Req._36._Collection_Report|(Req.36)]]
# Post-Production
## Processing Report [[Product_Specification#Req._38._Processing_Report|(Req.38)]]

===Daglig Kontrol===
(se også [[Pseudokode: Daglig kontrol|pseudokode]])

Udkast til Excel dokument til daglig kontrol kan ses her: [[File:DHM_flyvebod.xlsx]]:
# Flyver der er i brug
# Vejrforhold

===Ugentlig Rapport (hver tirsdag)===
(se også [[Pseudokode: Ugentlig Rapport|pseudokode]])

# Benyttede flyver
# Indsamlede swaths
# Placering af flyverne

===Rapportering af Trajectories===
10 dage efter den sidste lift

(See [[Product_Specification#Req._41._Trajectories|Req. 41]])

==Modtagekontrol==
(Accept af preliminary point cloud efter '''15 arbejdsdage''')

(Accept af final delivery efter '''40 arbejdsdage''')

# Dataspecifikke manuelle kontroller
#* Sensor mechanics [[Product_Specification#Req._16._Sensor_mechanics|(Req.16)]]
#* Multiple discrete returns [[Product_Specification#Req._14._Multiple_Discrete_Returns|(Req.14)]]
#* Scanner artefakter [[Product_Specification#Req._16._Sensor_mechanics|(Req.16)]]
<!--  -->
# Projektspecifikke manuelle kontroller
#* Survey Report [[Product_Specification#Req._37._Survey_Report|(Req.37)]]
#* Leverancemedia [[Product_Specification#Req._34._Data_media|(Req.34)]]
#* Genleverancer
<!--  -->
# Generiske simple automatiske kontroller (se også [[Pseudokode: Generiske simple automatiske kontroller|pseudokode]]).
#* Filnavne [[Product_Specification#Req._33._Naming_of_the_Tiled_Data|(Req.33)]]
#* Fuldstændighed - dækning, tilhørende filer, navne [[Product_Specification#Req._7._Data_Voids|(Req.7)]] NB: denne pind skal undersøges nærmere og nok splittes op. Req. 7 delen falder ikke under feltet "simple automatiske kontroller"
<!--  -->
# ESRI ASCII simple automatiske kontroller (se også [[Pseudokode: ESRI ASCII simple automatiske kontroller|pseudokode]]).
#* Headerkonsistens m. Data - navne [[Product_Specification#Req._33._Naming_of_the_Tiled_Data|(Req.33)]]
#* ASCII raster header corner/center [[Product_Specification#Req._31._Digital_Terrain_Model_DTM|(Req.31)]],[[Product_Specification#Req._32._Digital_Surface_Model_DSM|(Req.32)]]
<!--  -->
# LAS simple automatiske kontroller (se også [[Pseudokode: LAS simple automatiske kontroller|pseudokode]]).
#* Data Format [[Product_Specification#Req._22._Data_Format|(Req.22)]]
#* Point Cloud Format LAS 1.3, record type 1, 3 or 5 (Req.27 - hvor vi har glemt type 1)
#* Headerkonsistens m. Data - navne [[Product_Specification#Req._33._Naming_of_the_Tiled_Data|(Req.33)]]
#* Waveform format ok [[Product_Specification#Req._30._Point_Cloud_Waveform|(Req.30)]]
<!--  -->
# Kontrol af navigations og kalibreringsdata
#* Control and calibration points (Req.39)
#* GPS/IMU data (Req.40)
#* Trajectories (Req.41)
#* Dataextent - swath-extents (Req.35)
<!--  -->
# Mere vanskelige kontroller  (se også [[Pseudokode: Mere vanskelige  kontroller|pseudokode]]).
#* Holme å øer - fuldstændighed (Req.7)
#* Overlap (10 %) (Req.8)
#* Swath Identification (Req.23) 
#* Swaths multiple return Handling (Req.24)
#* Geometrisk sammenligning (*** Hvad mener vi med det? ***)

==Geometrisk kontrol==
[[Geometrisk kontrol - Pseudokode]]

[[DHM_Højdekontrol_-_Pseudokode]]

# Coordinate Reference System (CRS)
## Projection (Req.17)
## Datum (Req.18)
## Point Cloud Height System (Req.19)
## Derived gridded Products Height System (Req.20)
# Præcision overlap
## Højde (Req.11)
## Plan (Req.11)
# Nøjagtighed GCP 
## Højde (Req.10)
## Plan (Req.12)
# Nøjagtighed ift. 2007
# Rå DSM/DTM - 2007
# Global Positioning System (GPS) Times (Req.21)
# Point Density and distribution (Req.13)
# Grid->punkt afstand (Req.13)
# Tile overgange - Plan 
# Block, strip, tile og optionsovergange - Højde (Req. 11)
# Scan angle - max 32 (Req.8)
# Intensity values (Req.15)
# Præcision/scanner artefakter (Req.16)
# Overlap (10 %)(Req.8)
# Tværstribecheck (Req.9)

==Klassifikationskontrol==

# Point Classification Consistency (Req.25)
#* Det skal undersøges, om der er urealistisk mange/få punkter i udvalgte klasser. 
#** Tiles køres igennem, og der laves statistik for hver tile (summering af antal punkter indenfor hver klasse). 
#** Ses der et mønster af tiles, som ikke kan forklares ud fra omgivelserne (f.eks. vandområder), skal producenten svare på hvad der gør sig gældende for disse tiles.
#*** Klasse 32 (manually excluded). Store områder uden manuelle ekskluderinger bør rejse et flag
#*** Klasse 07 (outliers, low points and noise). For få/ingen punkter - er der noget som skjules? For mange punkter... Noget galt?
#* [[Klassifikationskontrol - Pseudokode]]
# Point Classification Classes (Req.26)
#* Som ved req 25, dannes statistik for hver tile. Alle klassifikationsklasser bør være tilstede i filen.
#* [[Klassifikationskontrol - Pseudokode]]
# Brokontrol
#* Der bør være klassificerede bropunkter i umiddelbar nærhed af 
#** Tilpasningslag, koderne "Horse shoe bridge at road", "Horse shoe bridge at railway", "Horse shoe bridge misc"
#** Polygoner fra leverance til sidste DHM (ikke komplet)
#** Hvor udvalgte FOT-objekter skærer ude af niveau
#*[[Brotjek - Pseudokode]]
# Overgangskontrol
#* Forudsat at leverandøren arbejder tile-baseret (1km) kan der være forskelle i klassificering ved overgang fra én tile til en anden. Erfaringsmæssigt kan det være høje afgrøder (f.eks. majs, raps), som ikke er klassificeret korrekt. Derfor vil et simpelt højdetjek langs kanten mellem to tiles, som støder op til hinanden kunne afsløre nogle mønstre. 
#* [[Overgangskontrol - Pseudokode]]
# Overlap klassificering
#* TBD. Der skal ske et tjek for om klassificeringen er sket ens i overlapsområder. Dette kan være både mellem striber og mellem blokke. Det er imidlertid ikke ligetil - f.eks. vil træer have punkter på jord og ikke-jord, og der kan godt være en vis afstand (x,y) mellem punkterne. En mulighed kunne være at regne indenfor celler (f.eks 5x5 m) og summere punkter sammen. Hvis antallet passer indenfor en vis tolerance, er alt (måske?) ok. 
# Arealbaseret kontrol
# DSM til klassifikationskontrol
# Outliers/Spikes
# Diger
# Klassifikation ift. DHM 2007
# Klassifikationsklasser

==Undersøgelse af kvalitet/kvalitetskontrol af afledte==
# Terræn i skov
# Egen DSM
# Egen DTM

==[[Product Specification]]==

==[[Time Schedule]]==
