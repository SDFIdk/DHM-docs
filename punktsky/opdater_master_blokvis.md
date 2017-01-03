# Opdater punktsky master

Med opdatering af punktsky master, menes der at punktskyen opdateres i Geodatabanken.
Det indebærer at koordinaterne i filerne fra forvaltningssystemet transformeres fra
ellipsoidehøjder til DVR90-højder. Derefter skal filerne indlæses i Geodatabanken.

## Transformation til DVR90 højder

Først dannes en tile coverage fil ud fra indholdet af forvaltningssystemet:
```
C:\> ogr2ogr -f sqlite C:\data\walter_coverage.sqlite -nln coverage "OCI:<USER>/<PASSWORD>@gst-orarac.prod.sitad.dk:1521/gstdb12.prod.sitad.dk:V_TILE_COVERAGE" -sql "select FILE_LOCATION as path, TILE_NAME, MROW as row, MCOL as col, GEOM from V_TILE_COVERAGE" -dialect SQLITE -a_srs EPSG:25832
```

Dernæst køres ```dhmqc.reproject```:

```
C:\dev\dhmqc\> python qc_wrap.py -testname reproject -tiles C:\data\walter_coverage.sqlite -targs "-in_srs EPSG:25832 -out_srs \"+init=epsg:25832 +geoidgrids=C:/data/dvr90.gtx\" -a_srs 7416 F:/DHM/temp/dhm_dvr90"
```

Her er det vigtigt at bemærk at ```dvr90.gtx``` er at finde på computeren.
Har du den ikke, så kan den findes på ```F:\DHM\Software\dvr90.gtx```
