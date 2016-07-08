# Modtagekontrol af mange data #

Modtagekontrollen af data relateret til det hydrologiske tilpasningslag udføres ved hjælp af en samlings python scripts, 
der kan findes på [BitBucket](https://bitbucket.org/GSTudvikler/dhym_tilpasningslag).
Hvis du ikke allerede har koden, så hent den med:

```
C:\dev> hg clone https://kevers@bitbucket.org/GSTudvikler/dhym_tilpasningslag
```

Derudover benyttes [DHMQC](https://bitbucket.org/GSTudvikler/gstdhmqc) til at beregne hillshades af de tilpassede højdemodeller.

## Vektordata ##

Selve tilpasningslaget udgøres af to vektordatasæt: Hestesko og linjer. På disse skal der køres et attribut check og et geometri check.

### Attribut check ###

De to attributcheck køres med:
```
C:\dev\dhym_tilpasningslag> python check_attributes.py C:\data\dhym_niras\etape2\Tilpasninglaget\Horseshoe.shp horseshoe
C:\dev\dhym_tilpasningslag> python check_attributes.py C:\data\dhym_niras\etape2\Tilpasninglaget\Line.shp line
```

Ved kørsel af de to scripts oprettes der en række ekstra attributter i shape-filen hvor til fejl rapporteres.
For attribut checket er de relevante felter  ```attr_err``` og ```attr_descr```, som angiver om der er fundet en fejl, og en beskrivelse af fejlen.

Der checkes om attributterne for de enkelte tilpasningsobjekter bryder med datamodellen.
Datamodellen er blandt andet beskrevet i kontrakten med NIRAS (2016).

Indlæs shapefilerne i QGIS og påfør dem stilarten ```tilpasning.qml``` der også ligger i ```dhym_tilpasningslag```.
Når stilarten er påført vises de objekter der har fejl med en anden farve end de resterende objekter.
Man kan med fordel også søge efter fejl i attributtabellen.


### Geometri check ###

Geometrichecket køres med følgende kommandoer:
```
C:\dev\dhym_tilpasningslag>python check_geometries.py C:\data\dhym_niras\etape2\Tilpasninglaget\Horseshoe.shp horseshoe
C:\dev\dhym_tilpasningslag>python check_geometries.py C:\data\dhym_niras\etape2\Tilpasninglaget\Line.shp line
```

Der kontrolleres om der er fejl de enkelte geometrier.
For hesteskoenes vedkommende checkes primært om geometrien udgøres af præcis fire punkter, og at linjen ikke skærer sig selv.
I kontrollen af linjerne checkes det om der er mere end et punkt i linjen, og om der findes z-værdier der hvor attributterne angiver at de børe være der.

De fundne fejl rapporteres i shape-filerne, på samme måde som det gøres under attribut checket.

## Raster data ##

I det følgende vises kun for DHM/Nedbør (rain) - proceduren er tilsvarende for DHM/Havstigning (searise).

### DTM check ###

Lav først tile coverage over de hydrologisk tilpassede DTM'er:
```
c:\dev\gstdhmqc>python tile_coverage.py create F:\dhm\dhym\etape2\HydroDTM_Rain tif F:\dhm\dhym\etape2\coverage
Creating coverage table.
F:\dhm\dhym\etape2\HydroDTM_Rain
Done: 200
Done: 400
...
Done: 4400
Done: 4600
Inserted/updated 4782 rows
Encountered 0 'dublet' tilenames
Encountered 0 bad tile-names.
```

Tile coverage for ikke-tilpassede DTM'er genereres fra Geodatabanken med ```ogr2ogr```.
Bemærk at PASSWORD i nedenstående skal erstattes med det korrekte password.
Spørg Thorbjørn eller Kristian hvis du ikke kender det.
```
C:\dev\dhym_tilpasningslag>ogr2ogr -f sqlite C:\data\dhym_niras\etape2\dtm_coverage.sqlite -nln coverage "OCI:RASTER_PUNKTSKY_KATALOG_L1/PASSWORD@gst-orarac.prod.sitad.dk:1521/geobank.prod.sitad.dk:DTM" -sql "SELECT filnavn tile_name, sti path, mrow \"row\", mcol \"col\" FROM dtm WHERE registreringtil IS NULL"
```

Herefter køres ```check_dtms.py``` fire gange, da alle kombinationer af hestesko, linjer, DHM/Nedbør og DHM/Havstigning skal testes.
Her vises kun for DHM/Nedbør - proceduren er tilsvarende for DHM/Havstigning.

DHM/Nedbør og linjer:
```
C:\dev\dhym_tilpasningslag>python check_dtms.py F:\dhm\dhym\etape2\coverage_dhym_rain.sqlite C:\data\dhym_niras\etape2\dtm_coverage.sqlite C:\data\dhym_niras\etape2\Tilpasninglaget\Line.shp line rain --verbose
```

DHM/Nedbør og hestesko:
```
C:\dev\dhym_tilpasningslag> python check_dtms.py F:\dhm\dhym\etape2\coverage_dhym_rain.sqlite C:\data\dhym_niras\etape2\dtm_coverage.sqlite C:\data\dhym_niras\etape2\Tilpasninglaget\Horseshoe.shp horseshoe rain --verbose
```

### Hillshades ###

Hillshades bruges til at lave en visuel inspektion af de hydrologisk tilpassede højdemodeller.
Til beregning af hillshades bruges de samme tile coverage filer som foregående afsnit.
Hillshades laves med DHMQC og sættes i gang med kommandoen:
```
c:\dev\dhmqc> python qc_wrap.py -testname hillshade -mp 4 -tiles F:\dhm\DHyM\etape2\coverage_dhym_rain.sqlite -targs "-tiledb F:/DHM/DHyM/etape2
/coverage_dhym_rain.sqlite F:/dhm/dhym/etape2/HydroDTM_Rain_HS"
Defining INPUT_TILE_CONNECTION: u'F:\\dhm\\DHyM\\etape2\\coverage_dhym_rain.sqlite'
Defining TESTNAME: 'hillshade'
Defining TARGS: ['-tiledb', 'F:/DHM/DHyM/etape2/coverage_dhym_rain.sqlite', 'F:/dhm/dhym/etape2/HydroDTM_Rain_HS']
Defining MP: 4
Validating arguments for hillshade
Getting tiles from ogr datasource: F:\dhm\DHyM\etape2\coverage_dhym_rain.sqlite
No SQL defined. Assuming we want the first layer and attribute is called 'path'
Found 4782 tiles.
Running qc_wrap at Thu Jul 07 14:50:23 2016
Starting 4 process(es).
Using process db: hillshade_1467895823.sqlite
[qc_wrap - hillshade]: Done: 0.0 pct, tiles left: 4782, estimated time left: unknown, active: 4
[qc_wrap - hillshade]: Done: 0.4 pct, tiles left: 4764, estimated time left: 5309.74 s, active: 4
...
[qc_wrap - hillshade]: Done: 99.6 pct, tiles left: 20, estimated time left: 35.85 s, active: 4
[qc_wrap - hillshade]: Done: 99.9 pct, tiles left: 6, estimated time left: 10.74 s, active: 4
Running time 8561.98 s
[qc_wrap]: Did 4782 tile(s).
qc_wrap finished at Thu Jul 07 17:16:52 2016
```

**Komprimering til distribution**

Hillshade filerne _kan_ i yderste konsekvens godt distribueres som 1km-filer med vrt og eksterne overviews. Dette er af flere årsager ikke det mest praktiske (mange filer via ftp kan gå galt - vrt filen kan blive stor og dermed længere søgetid). Derfor er det bedste at lave én tiff-fil med enten internt eller eksternt overviews. I det følgende beskrives eksternt, da dette tager kortere tid at producere, og har vist sig at være en gangbar metode. 

Start med at kopiere filerne til en maskine med en SSD disk. 

Kør herefter kommandoerne: 

```
gdalbuildvrt filnavn.vrt mappe-med-1km-filer
```
og
```
gdal_translate -of GTiff -CO COMPRESS=DEFLATE vrt-fil-navn.vrt tif-fil-navn.tif
```
gdalbuildvrt går ret hurtigt, gdal_translate kan godt tage nogle timer.

Overviews dannes efterfølgende med kommandoen: 

```
gdaladdo -ro --config COMPRESS_OVERVIEW LZW -r gauss tif-fil-navn.tif 4 8 16 32
```




