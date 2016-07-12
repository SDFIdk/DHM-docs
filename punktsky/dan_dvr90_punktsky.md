#Dan DVR90 punktsky

Forvaltningssystemet indeholder data med højder i ellipsoidehøjder. Til den brede offentlighed (også internt) er punktsky i ortografiske højder langt mere anvendelige. Derfor sker et udtræk til DVR90 (Dansk Vertikal Reference 1990). 

Eftersom udtrækket sker vha forvaltningssystemets Oracle database, skal der dannes en SQL-forespørgsel, som er tilpasset det område, som ønskes udtrukket. 

Udtrækket kan passende køres med en parameterfil, f.eks. ved tilretning af "job_extract_dvr90_xxx-py" i dhmqc_params mappen: 

```
#This is a template for gridding from a local tiledb. Control varoius options in the TARGS.
import os
import json
MP=4
OUTDIR=r"H:\dvr90_201"

TILE_DB="OCI:<USER>/<PASSWORD>@<ORACONNECTION>"
INPUT_TILE_CONNECTION=TILE_DB
INPUT_LAYER_SQL="select file_location from distr_adm.v_pktsky_aktive where (NEEDS_DEM=1234 or NEEDS_DEM=4) and HEIGHT_SYSTEM='E'"
MAPS="PG: host='c1200038' dbname='grundkort' user='<USER>' password='<PASSWORD>'"
BBOX="where ST_Intersects(wkb_geometry,ST_GeomFromText(WKT_EXT,25832))"

TESTNAME="dvr90_wrapper"
TARGS=[OUTDIR]
```

De udtrukne filer indlæses i geodatabanken, se <LINK>
