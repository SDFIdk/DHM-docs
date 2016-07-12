**This document is in Danish**
___


# Vejledning i gridding (DTM/DSM) fra master


Efter at filer er lagt i master-biblioteket <LINK>, kan der laves ny DTM og DSM. 


## Step 1 - tildel søhøjder. 


Kræver: 
        
* Las-filer med ellipsoide-højder (ellers skal køres med -nowarp)
* Tabel med nyeste FOT-søer. Ekstra attributter:
   * burn_z (real)
   * n_used (integer)
   * is_invalid (integer eller shortint)
   * has_voids (integer eller shortint)
   * reason (varchar)
   * version (integer)

```
qc_wrap.py -testname set_lake_z dbconnection tabelnavn -tiles ora_connectionstring -tilesql (“select file_location….)
```

F.eks.

```
python qc_wrap.py -testname set_lake_z -tiles "OCI:<USER>/<PASSWORD>@<ORACLE_CONNECTION_STRING>" -tilesql "select FILE_LOCATION from DISTR_ADM.V_PKTSKY_AKTIVE where ORIG_BLOCK ='B06'" -targs "'host=c1200038 user=<USER> password=<PASSWORD> dbname=grundkort' public.burn_lakes"
```

**NB PGconnection er uden PG:, da det ikke er ogr!**



## Step 2 - generer DTM/DSM med søer.


Brug job i DHMqc_params, f.eks. job_dem_gen_master_b01.py

```
#This is a template for gridding from a local tiledb. Control varoius options in the TARGS.
import os
import json
#OUTDIR=os.environ["DHMQC_DEMS"]
OUTDIR=r"\\kms.adroot.dk\dhm2007-server\DHM-D\test\b01\dems"
#TILE_DB=os.environ["ORA_CONNECTION"]
TILE_DB="OCI:<USER>/<PASSWORD>@<ORACLE_CONNECTION_STRING>"
INPUT_TILE_CONNECTION=TILE_DB
INPUT_LAYER_SQL="select file_location from distr_adm.v_pktsky_aktive where ORIG_BLOCK ='B01'"  #<-- Change here!!
MAPS="PG: host='<SERVER>' dbname='grundkort' user='<USERNAME>' password='<PASSWORD>'"
BBOX="where ST_Intersects(wkb_geometry,ST_GeomFromText(WKT_EXT,25832))"
LAYERS={
"RIVER_LAYER":(MAPS,"select ST_Buffer(wkb_geometry,3) from geodk.vandloebsmidte_brudt "+BBOX+" and synlig='1' and midtbredde!='0-2.5'"),
"BUILD_LAYER":(MAPS,"select wkb_geometry from geodk.bygning "+BBOX),
"LAKE_LAYER":(MAPS,"select wkb_geometry from geodk.soe "+BBOX),
"LAKE_Z_LAYER":(MAPS,"select wkb_geometry,burn_z from public.burn_lakes "+BBOX+" and is_invalid=0 and burn_z is not null and has_voids=1"),
"SEA_LAYER":(MAPS,"select wkb_geometry from hav.hav_tiled "+BBOX),
"LAKE_Z_ATTR":"burn_z"
}

TESTNAME="dem_gen_new"
TARGS=[TILE_DB,OUTDIR,
"-dtm","-dsm",
"-overwrite",
"-hsys","dvr90",
"-triangle_limit","2.5",
"-zlim","0.4",
"-flatten",
"-burn_sea",
"-layer_def",json.dumps(LAYERS),
"-rowcol_sql","select mrow,mcol from distr_adm.v_pktsky_aktive where tile_name='{TILE_NAME}'","-tile_sql",
"select file_location,ground_classes,surface_classes,height_system from distr_adm.v_pktsky_aktive where abs(mrow-({ROW}))<2 and abs(mcol-({COL}))<2"]
```

Når beregningen af DTM/DSM er foretaget, kan filerne indlæses i Geodatabanken. 
